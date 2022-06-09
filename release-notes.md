
# Android Chat SDK Release Notes


<details open markdown="block">
<summary> Version 5.0.3 </summary>

# Version 5.0.3
#### `pre-release`   
Release date: 
___

### What's new 
- Basic history support. History fetched when returning to previos started chats and on network connection recovery.
- Automatic connection to current open messenger chat, once network connection recovery identified on the device.
- Addition of configurable `System message` UI component.
- Chat state tracking improvement.
- Integrating with Transport SDK version `cloud.genesys:messenger-transport-mobile-sdk:1.2.1`
- `ChatAvailability.checkAvailability` API available for messenger chat. Allows hosting Apps to verify wether messenger chat activation is feasible.
 
### Bug fixes
- Incoming messages buffering until history fetched messages are loaded.
- Ignoring event typed messages to prevent empty messages.

### Breaking changes
- ChatHandler manages the chat configurations with `ConfigurationRepository` instead of the dismissed `ConfigurationProvider`.
- Dening access to `ConfigurationRepository` and `ChatEngine` from the `ChatController` instance.
- Separate chat configuration maintained for each active chat session.

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
- Chat configurations maintenance improvements. Seperating logic settings from UI related configurations.
- Loading messenger chat configurations and applying basic UI configurations on displayed messages.
- Enable chat configurations alternation by the hosting App before chat starts, with `ConfigurationsProvider` implementation. 
- Chat start can be prevented using `ChatSettings::enabled` property.
Failure to load chat configurations, fails the chat creation.
- Messenger chat engine support.
- Configurable UI components for `Fast scroll` button and `Datestamp` headers, were added to `ChatUIProvider`.
- UI configurations for `Timestamp` and `Readmore`, were added to `ChatUIProvider`.
- Integrating with Transport SDK version `cloud.genesys:messenger-transport-mobile-sdk:1.1.14`.

### Bug fixes
- Fast scroll button visibility after voice recording.
- Double display of fast scroll button after configuration update.
- State and error events are now passed to the hosting App on the `main thread`.

### Breaking changes
- `Timestamp` UI configuration, `textStyleConfig` and `readMoreThreshold`, were relocated to `ChatUIProvider`. 
- `ChatScroller` renamed to `ChatFastScrollConfig` and is now available on `ChatUIProvider::FastScrollUIProvider`.
- `ChatUIProvider` instance can't be set over the `ChatController` instance. `ConfigurationsProvider` implementation should be used instead.
- `ConversationSettings` were dismissed, use `ConfigurationsProvider` instead.

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
Release date: 13 Dec 2021

### What's new 
- Chat engine support for the available chat types. The chat engine enables creation and control of chats not related to the displayed chat UI.  
- Javadoc and KDoc, technical documentation addition.  
- Integrating with Transport SDK version `cloud.genesys:messenger-transport-mobile-sdk:1.1.12`.

### Breaking Changes
- namespacing and packages renaming to `com.genesys.cloud` prefix. 
- `engine` module removal. Content moved to `chatintegration` module.

---

### Dependencies 

> 👉  Artifacts are now located under JFrog artifactory

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