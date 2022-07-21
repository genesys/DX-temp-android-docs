
## Quick start quide

Use this Quick start guide to set up a working messaging client hosted by your App.   

### System Requirements  

* Android Studio version Arctic Fox 2020.3.1 or higher
* Gradle version 7.2 or higher (Gradle plugin 7.1.0 and higher)
* Kotlin plugin version 1.6.21 and higher
* Java 8 or higher
* Android 5.0 (API level 21) or higher 


### Set up chat SDK on your App.

1. **Import SDK's artifacts**
        
    To use the SDK, add the following imports to your App's build.gradle file.

    ```gradle
    implementation 'com.genesys.cloud:core:[Version_Number]'
    implementation 'com.genesys.cloud:chatintegration:[Version_Number]'
    implementation 'com.genesys.cloud:ui:[Version_Number]'

    // optional:
    implementation 'com.genesys.cloud:accessibility:[Version_Number]'
    ```

    [Check SDK's release notes for the latest available version](./release-notes#dependencies) 

    
2. **Extra configurations on build.gradle**
   
    Add the following to the _`android{...}`_ block definition

    ```gradle
    android {
        kotlinOptions {
            freeCompilerArgs = ['-Xjvm-default=compatibility'] or ['-Xjvm-default=all']
            jvmTarget = "1.8"
        }

        //The following should be added in case build fail with the error: "More than one file was found with OS independent path..."
        packagingOptions {
            resources {
                pickFirsts += ['META-INF/DEPENDENCIES', 'META-INF/main_debug.kotlin_module', 'META-INF/main_release.kotlin_module', 'META-INF/main_sdktesting.kotlin_module', 'META-INF/ui_debug.kotlin_module', 'META-INF/ui_release.kotlin_module']
            }
        }
    }
    ```

    > If your app is configured with the `minifyEnabled` set to `true`, please read [Shrink and Obfuscattion support](./shrink-and-obfuscate.md') to make sure that the relevant rules are provided on the proguard file.
    
---

### Create and start a basic messaging conversation  

Follow the next steps to have a basic working messaging integrated to your App.

1. Create or set the activity in which the conversation will be displayed.

2. **Create Messenger account**
    Create a [`MessengerAccount`](./messenger-chat#messengeraccount) and configure it with a predefined [`Messenger Deployment`](https://help.mypurecloud.com/articles/deploy-messenger/) details.
     
    ```kotlin
    val messengerAccount = MessengerAccount([Deployment_Id], [Domain]).apply {
            tokenStoreKey = [Token_Key]
            logging = [true/false]
        }
    ```  
     
3. **Create ChatController instance**
    
    The [`ChatController`](./chatcontroller.md) is the interaction point with the SDK. You need it to create a chat.

    ```kotlin
    val chatController = ChatController.Builder(context)
                                          .build(messengerAccount, ChatLoadedListener)
    ```

4. **Display the Messenger on your activity**

    If the ChatController build was successful, it creates a fragment on which the messenger UI will be displayed. The created fragment should be added to your app's activity.

    To get the chat fragment, implement the `ChatLoadedListener` interface and pass the implementation to `ChatController.Builder` `build` method.   
    `ChatLoadedListener:onComplete` will be called with the messenger creation outcome as a `ChatLoadResponse` instance.    
    `ChatLoadResponse` will contain the messenger fragment if the messenger was created properly.   
    
    ```kotlin
    ChatController.Builder(context).build(account, object : ChatLoadedListener {
            override fun onComplete(result: ChatLoadResponse) {
                result.error?.let {
                  // report Chat loading failed
                } ?: let {
                  // add result.fragment to your activity.
                  supportFragmentManager.beginTransaction().replace(R.id.chat_container, result.fragment, tag).commit()
                }
            }
        })
    ```

    > Verify that there is no existing chat fragment added to your activity if there is, make sure to remove it before adding the newly provided fragment.

5. **Release chat resources on activity destroy** 
- Activate `ChatController.destruct()` when the [`ChatController`](./chatcontroller.md) instance is no longer needed. Destruct will release referenced open resources.

---

### [Code Sample](https://github.com/genesys/)
