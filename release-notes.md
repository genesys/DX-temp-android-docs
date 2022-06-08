

# Android Mobile SDK Release Notes


<details open markdown="block">
<summary> Version 5.0.3 </summary>

## Version 5.0.3
Release date: 

___

### Features
- Basic history fetching on chat start and network reconnection.
- Configurable `System message` UI component.
- Chat state tracking on chat engine.
- Integrating with Transport SDK version `cloud.genesys:messenger-transport-mobile-sdk:1.2.1`
- Exposing `ChatAvailability.checkAvailability` API to allow hosting Apps to verify wether messenger chat activation is feasible.

### Fixes
- Incoming messages buffering while chat loads and reconnects.
- Ignoring event typed messages prevents empty messages.

### Breaking changes
- ConfigurationProvider was replaced with ConfigurationRepository managed by ChatHandler.
- Dening access to `ConfigurationRepository` and `ChatEngine` from `ChatController`.

---

### Dependencies 

```gradle
repositories {
  ...

  maven {url "https://genesysdx.jfrog.io/artifactory/genesysdx-android.dev"}
}

implementation("com.genesys.cloud:core:5.0.+") { changing = true }
implementation("com.genesys.cloud:chatintegration:5.0.+") { changing = true }
implementation("com.genesys.cloud:ui:5.0.+")
```

</details>



</details>
<details close markdown="block">
<summary> Version 5.0.2 </summary>

# Version 5.0.2
Release date: 

### Features
- Messenger chat engine support. 
- Chat configurations maintenance improvements. Seperating logic settings from UI related configurations.
- Loading messenger chat configurations and applying basic UI configurations on displayed messages.
- Enable chat configurations alternation by the hosting App before chat starts, with `ConfigurationsProvider` implementation. 
- Chat start can be prevented using `ChatSettings::enabled` property.
Failure to load chat configurations, fails the chat creation.

### Fixes
- Fast scroll button visibility after voice recording
- Double injected fast scroll button after configuration update
- State and error event pass to the hosting App on the main thread.

### Breaking changes
- Timestamp UI configuration moved from ChatSettings to the SDKs UI components configuration. 
- UI related configurations were moved from the ChatSettings and are now available on `ChatUIProvider`.
- Applying `ChatUIProvider` to `ChatController` was dismissed, `ConfigurationsProvider` should be used instead.
- `ConversationSettings` were dismissed, use `ConfigurationsProvider` instead.

---

### Dependencies 

```gradle
repositories {
  ...

  maven {url "https://genesysdx.jfrog.io/artifactory/genesysdx-android.dev"}
}

implementation("com.genesys.cloud:core:5.0.+") { changing = true }
implementation("com.genesys.cloud:chatintegration:5.0.+") { changing = true }
implementation("com.genesys.cloud:ui:5.0.2.rc4")
```

</details>



<details close markdown="block">

<summary> Version 5.0.1 </summary>

# Version 5.0.1
Release date: 

### Features
- Adding chat engine to supported chats. The chat engine enables creation and control of chats not related to the displayed chat UI.  
- Adding technical documentation using Javadoc and kDoc 
- Integrating with Transport SDK version `cloud.genesys:messenger-transport-mobile-sdk:1.1.12`

### Breaking Changes
- namespacing and packages renaming to `com.genesys.cloud` prefix 

---

### Dependencies 

```gradle
repositories {
  ...

  maven {url "https://genesysdx.jfrog.io/artifactory/genesysdx-android.dev"}
}

implementation("com.genesys.cloud:core:5.0.1.rc3") { changing = true }
implementation("com.genesys.cloud:chatintegration:5.0.1.rc3") { changing = true }
implementation("com.genesys.cloud:ui:5.0.1.rc3")
```
---

</details>


<details close markdown="block">

<summary> Version 5.0.0 </summary>

# Version 5.0.0
Release date: 14 Nov 2021

### Features
- **Support basic messenger chat.** 
- Basic error handling for messenger chat.
- Integration with Transport SDK version `com.genesys.sdk:transport:1.0.0.rc4`

---

### Dependencies 

```gradle
repositories {
  ...

  maven {url "https://genesysdx.jfrog.io/artifactory/genesysdx-android.dev"}
}

implementation("com.genesys.cloud:core:5.0.0.rc2") { changing = true }
implementation("com.genesys.cloud:chatintegration:5.0.0.rc1") { changing = true }
implementation("com.genesys.cloud:ui:5.0.0.rc4")
```
---

</details>

---