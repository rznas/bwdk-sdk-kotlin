# BWDK Kotlin SDK — Integration Guide for Agents

You are integrating **BWDK (Buy With DigiKala)** into a Kotlin project (Spring / Ktor / Micronaut / Android-server) via this SDK. Read this file **first**, then consult the companion references below.

## BWDK constants

- **Host:** `https://bwdk-backend.digify.shop`
- **Auth scheme:** `MerchantAPIKeyAuth` — header `Authorization: <api_key>`.
- **Main API class:** `bwdk_sdk.apis.DefaultApi`.
- **Package root:** `bwdk_sdk` (models under `bwdk_sdk.models`, infra under `bwdk_sdk.infrastructure`).
- **Build:** Gradle 8.14, Kotlin 2.2.20.

## Companion references

| File                 | When to read                                                 |
|----------------------|--------------------------------------------------------------|
| `README.md`          | Build/publish instructions (`gradle wrapper`, `./gradlew check assemble`) plus feature notes. |
| `FLOWCHART.md`       | Canonical order state machine. All callback/webhook branching MUST match these state names. |
| `docs/DefaultApi.md` | Exact method names and signatures per endpoint.              |
| `docs/*.md`          | Per-model reference (e.g. `docs/OrderCreate.md`).            |

Do **not** duplicate build or method-signature details here — fetch `README.md`.

## Install

Since this SDK is not published to Maven Central yet, either:

1. **Build locally:** clone the tag and run `./gradlew publishToMavenLocal`, then depend on it in the host project via `mavenLocal()` + `implementation("org.openapitools:bwdk_sdk:<version>")`.
2. **Include as source:** vendor the `src/` tree under the host project and depend on it as a subproject.

See `README.md` for the exact publish/build commands.

## Minimal wrapper pattern

```kotlin
import bwdk_sdk.apis.DefaultApi
import bwdk_sdk.infrastructure.ApiClient

ApiClient.apiKey["Authorization"] = System.getenv("BWDK_API_KEY")
val api = DefaultApi(basePath = "https://bwdk-backend.digify.shop")

val order = api.orderApiV1CreateOrderCreate(payload)
```

Method names are camelCase and OpenAPI-generated. Look them up in `docs/DefaultApi.md`; do **not** guess.

## Integration invariants

1. **SDK only.** Never call BWDK with ktor-client (standalone), Retrofit (standalone), or OkHttp.
2. **Callback flow.** After payment, BWDK redirects the customer to your `callback_url`. Load the order (`orderApiV1ManagerRetrieve`), branch on `order.status` per `FLOWCHART.md`, then call `orderApiV1ManagerVerifyCreate` — `verify` is mandatory before `SHIPPED`.
3. **Errors.** The SDK throws `bwdk_sdk.infrastructure.ClientException` / `ServerException`. Inspect `statusCode` and `response`. Retry only on I/O errors, never on 4xx.
4. **Coroutines:** the generated client is synchronous (blocking). Wrap calls in `withContext(Dispatchers.IO)` when calling from coroutine code.
5. **Pinning.** Pin a concrete `<version>` (matching a `vX.Y.Z` tag).

## Project conventions

- **Spring Boot (Kotlin):** expose `DefaultApi` as a `@Bean` in a `@Configuration` class.
- **Ktor:** keep the SDK call inside a service class; do not mix it with `HttpClient` features.
- **Immutability:** generated `data class` models are good to pass around directly; copy them with `.copy(...)` when you need to mutate.
