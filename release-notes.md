
# Android Messenger SDK Release Notes


<details open markdown="block">
<summary> Version 5.0.3 </summary>

# Version 5.0.3
#### `pre-release`   
Release date: 
___

### What's new 
- Basic history support. History is fetched when returning to previously started chats and on network connection recovery.
- Once the network connection recovery identified on the device, connection is automatically established to the current open messenger chat.
- Addition of configurable `System message` UI component.
- Improved chat state tracking.
- Integration with Transport SDK version `cloud.genesys:messenger-transport-mobile-sdk:1.2.1`
- `ChatAvailability.checkAvailability` API is available for messenger chat, which allows hosting Apps to verify whether the messenger chat activation is feasible.
 
### Bug fixes
- Incoming messages buffering until history fetched messages are loaded.
- Ignoring event type messages to prevent empty messages.

### Breaking changes
- ChatHandler manages the chat configurations with `ConfigurationRepository` instead of the dismissed `ConfigurationProvider`.
- Denying access to `ConfigurationRepository` and `ChatEngine` from the `ChatController` instance.
- Separate chat configuration is maintained for each of the active chat sessions.

---

### Dependencies 

```gradle
repositories {
  ...
  maven {url "https://genesysdx.jfrog.io/artifactory/genesysdx-android.dev"}
}

dependencies {
  ...
  implementation 'com.genesys.cloud:core:5.0.3.rc4'
  implementation 'com.genesys.cloud:chatintegration:5.0.3.rc3'
  implementation 'com.genesys.cloud:ui:5.0.3.rc4'
}
```

</details>

---

</details>
<details close markdown="block">
<summary> Version 5.0.2 </summary>

# Version 5.0.2
#### `pre-release`
Release date: 20 Feb 2022

### What's new 
- Chat configurations maintenance improvements. Separated logic settings from UI related configurations.
- Loaded messenger chat configurations and applied basic UI configurations on displayed messages.
- Enabled chat configurations alternation by the hosting App before chat starts, with `ConfigurationsProvider` implementation. 
- Chat start can be prevented with the use of `ChatSettings::enabled` property.
Failure to load chat configurations makes the chat creation fail.
- Messenger chat engine support.
- Configurable UI components for `Fast scroll` button and `Datestamp` headers, were added to `ChatUIProvider`.
- UI configurations for `Timestamp` and `Readmore`, were added to `ChatUIProvider`.
- Integration with Transport SDK version `cloud.genesys:messenger-transport-mobile-sdk:1.1.14`.

### Bug fixes
- Fast scroll button visibility after voice recording.
- Double display of fast scroll button after configuration update.
- State and error events are now passed to the hosting App on the `main thread`.

### Breaking changes
- `Timestamp` UI configuration, `textStyleConfig` and `readMoreThreshold`, were relocated to `ChatUIProvider`. 
- `ChatScroller` was renamed to `ChatFastScrollConfig` and is now available on `ChatUIProvider::FastScrollUIProvider`.
- `ChatUIProvider` instance can't be set over the `ChatController` instance. Use `ConfigurationsProvider` implementation should be used instead.
- `ConversationSettings` were dismissed. Use `ConfigurationsProvider` instead.

--- 

### Dependencies 

```gradle
repositories {
  ...
  maven {url "https://genesysdx.jfrog.io/artifactory/genesysdx-android.dev"}
}

dependencies {
  ...
  implementation 'com.genesys.cloud:core:5.0.2.rc1'
  implementation 'com.genesys.cloud:chatintegration:5.0.2.rc2'
  implementation 'com.genesys.cloud:ui:5.0.2.rc4'
}
```

</details>

---

<details close markdown="block">

<summary> Version 5.0.1 </summary>

# Version 5.0.1
#### `pre-release`
Release date: 13 Dec 2021

### What's new 
- Chat engine support. Provides the functionality to creat and control chats.  
- Technical documentation generation with Javadoc and KDoc comments.  
- Integration with Transport SDK version `cloud.genesys:messenger-transport-mobile-sdk:1.1.12`.

### Breaking Changes
- Modules namespacing and packages were renamed with `com.genesys.cloud` prefix. 
- Module `engine` was removed. Classes can be found under `chatintegration` module.

---

### Dependencies 

> 👉  Artifacts are available on JFrog artifactory

```gradle
repositories {
  ...
  maven {url "https://genesysdx.jfrog.io/artifactory/genesysdx-android.dev"}
}

dependencies {
  ...
  implementation 'com.genesys.cloud:core:5.0.1.rc3'
  implementation 'com.genesys.cloud:chatintegration:5.0.1.rc3'
  implementation 'com.genesys.cloud:ui:5.0.1.rc3'
}
```

</details>

---

<details close markdown="block">

<summary> Version 5.0.0 </summary>

# Version 5.0.0
#### `pre-release`
Release date: 14 Nov 2021

### What's new 
- Basic messenger chat support. 
- Basic error handling for messenger chat.
- Integration with Transport SDK version `com.genesys.sdk:transport:1.0.0.rc4`.

---

### Dependencies 

```gradle
repositories {
  ...
  maven {url "https://bold360ai-mobile-artifacts.s3.amazonaws.com/dx/android/dev/"}
}

dependencies {
  ...
  implementation 'com.nanorep.devcore:sdkcore:5.0.0.rc2'
  implementation 'com.nanorep.devconversation:engine:5.0.0.rc1'
  implementation 'com.nanorep.devconversation:chatintegration:5.0.0.rc1'
  implementation 'com.nanorep.devconversation:ui:5.0.0.rc4'
  implementation 'com.nanorep.devcore:accessibility:5.0.0.rc1'
}
```

</details>

---
