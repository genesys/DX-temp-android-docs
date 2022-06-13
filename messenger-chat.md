
# Messaging chat 

## Overview
The SDK provides the tools to create and start a messaging chat which will be answered by either bot or agent.
As long as the chat session was not expires, users can return to the chat where it was left off. Users can brows through past messages.

Messaging chat creation relys on MessengerAccount, which contains the data needed to configure a chat session.   

---

## MessengerAccount

Use `MessengerAccount` to create messaging chat sessions with either bot or agent.   
MessengerAccount instance should be configured with the following details.

- `deploymentId` - A predefined messenger window deployment id, as configured and deployed on the Genesys Cloud Admin UI.
- `domain` - The regional base domain address for a Genesys Cloud Web Messaging service.
- `tokenStorageKey` - The key to access device local storage, where the user token is stored. (Different keys leads to different chat sessions)
- `logging` - Enables/Disables messaging extra logs.

```kotlin
val messengerAccount = MessengerAccount(deploymentId, domain).apply {
            tokenStoreKey = "someTokenKey"
            logging = true
        }
```  

---

## Start or resume a chat
{: .d-inline-block .mt-2}
The SDK provides a wide APIs that enables apps to control and interact with an ongoing chat.
Chats are created using a [`ChatController`]({{'/docs/chat-configuration/extra/chatcontroller' | relative_url}}) instance.    
`ChatController` instance can be recreated everytime the chat should be opened, or be used for multiple chat sessions creation.

- Start/Resume chat with new `ChatController` instance.

    ```kotlin
    val chatController = ChatController.Builder(context)                                                     
                                        .build(messengerAccount, ...)
    ```
    

- Start/Resume chat with an existing `ChatController` instance.
Call [`chatController.startChat`]({{'/docs/chat-configuration/extra/chatcontroller#start-chats' | relative_url}})/`chatController.restoreChat` with the configured `MessengerAccount`.

    ```kotlin
    chatController.startChat(messengerAccount)
    // or
    chatController.restoreChat(account = messengerAccount)
    ```

![]({{'/assets/diagrams/start_with_live.png' | relative_url}})
  
