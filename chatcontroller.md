
# ChatController

## Overview
Bridging interface between the hosting App and the chat SDK. The ChatController provides APIs to enable hosting Apps to create and manage chats.

## How to use
The `ChatControler` is created with a builder class. The builder can be configured with providers and listeners, that will be used by the ChatController during the chat progress, to pass events and notifications to the hosting App and to trigger App's actions in some cases.   
ChatController creation also triggers the creation and start of the chat indicated by the `AccountInfo` parameter. 
The ChatController instance may be used for multiple chats creation.  

> 👉 First chat starts with the ChatController creation, <u>no need to call </u>`startChat`<u> to activate it.</u>   


### Start chats
After ChatController instance creation, chats can be started with `startChat`, which defines a new chat, or with `restoreChat` that can be used to continue a previous ongoing chat (as long as the chat is still active).

### Keep chat active while UI is off
As long as the ChatController is still alive and the active chat was not terminated, the ChatHandler is still active and maintain connection to the BE. The chat fragment can be destroyed and recreated later on by the App, so the chat can be restored as was never closed.
This can be done using `restoreChat`, with the newly created fragment as it's first parameter.

```kotlin
chatController.restoreChat(MyFragment) // restore the current active chat
```

I there is no active chat available an error will be thrown through `ChatEventListener`. 

> 👉  If an account is passed on this method, the chat will be recreated.


### End chats
With the ChatController instance, the hosting App can end active chats.

- Use `endChat`, to end the current active chat.   
  
  `forceClose = true` can be passed, for fast chat closure. When force closing live chat, postchat form will not be activated.
  
- Use `terminateChat`, to end **all** current active chats. 
  
  e.g., Bot chat was escalated to live chat. In order to close both bot and escalated chats we use `chatController.terminateChat()`
  
- Once the ChatController has no more active chats, it passes a `StateEvent.Idle`, to its attached `ChatEventListener` implementation.

### Destruct and release
In order to release the ChatController's resources, use `ChatController.destruct()`.  
Destructed `ChatController` instance **can no longer be used to create/manage chats**. Any usage attempt 
will end with `IllegalStateException`.

> ChatController destruction, releases resources and listeners, but does not ends the open chats. Ending active chats (`terminateChat`) should be activated by the hosting App prior to ChatController destruction.   

### Listening to events and updates
Using the ChatController you can set listeners to chat states and data updates.
The following can be set on the ChatController creation or later on.
`ChatElementListener` - listens to chat messages changes
`ChatEventListener` - listens to chat state changes and to user actions that needs to be handled by the App. 
`ConfigurationsProvider` - Enables changing chat configurations.

### Controlling chat UI
Chat UI is controlled by `ChatUIProvider` class. This class defines the configurable UI components available on the chat.
In order to be able to change some of the configurations or override UI components with your own, 


### Other ChatController APIs
The ChatController provides some APIs to the hosting App enables it to interact with the active chat.

- `post` - Adds a message into the chat. Use `SystemStatement`, `OutgoingStatement` or `OutgoingStatement` to create a message. 
  ```kotlin
  chatController.post(SystemStatement("This is a system message"))
  ```
- `subscribeNotifications` and `unsubscribeNotifications` - Subscribes to be notified of specific `Notification` events.
  Declare the `Notification` types you would like to be notified of. Available notifications defined by `ChatNotifications` and `Notifications`.

  ```kotlin
  chatController.subscribeNotifications(object: Notifiable {
    override fun onNotify(notification: Notification, dispatcher: DispatchContinuation) {...}
  }, ChatNotifications.LanguageChanged, Notifications.UploadEnd)
  ```

- `uploadFile` - In case the current active chat allows files upload, this will trigger the upload process.

- `onChatInterruption` - Should be activated when the chat progress may fault due to some action done by the phone.
like in case of an incoming call while the speech services is in use by the chat.

- `isEnabled` - Check if a feature is enabled on the active chat.

- `hasOpenChats` - Returns true if there are currently chats on the ChatController stack.

- `getScope` - returns the current active chat `StatementScope` value.
