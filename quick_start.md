
## Quick start

Use this Quick Start guide to get you up and running with a working chat hosted by your App.   

### System Requirements  

* Android Studio version Arctic Fox 2020.3.1 or higher.
* Gradle version 7.2 or higher. (gradle plugin 7.1.0 and higher)
* Kotlin plugin version 1.6.21 and higher
* Java 8 or higher
* Android 5.0 (API level 21) or higher. 


### Set up chat SDK on your App.

1. **Import SDK's artifacts**
        
    In order to be able to use the SDK adds the following imports to your App's build.gradle file.

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

    > If your app is configured with shrink and minify turned on, please read [Shrink and Obfuscattion support](./shrink-and-obfuscate') and make sure the relevant rules are provided on the proguard file.
    
---

### Create and start a basic chat  

Follow the next steps in order to have a basic working chat integrated to your App.

1. Create or set the activity in which the chat will be displayed.

2. **Create chat account**
    Create a [`MessengerAccount`](./messenger-chat#messengeraccount) and configure it with a predefined [`Messenger Deployment`](https://help.mypurecloud.com/articles/deploy-messenger/) details.
     
    ```kotlin
    val messengerAccount = MessengerAccount([Deployment_Id], [Domain]).apply {
            tokenStoreKey = [Token_Key]
            logging = [true/false]
        }
    ```  
     
3. **Create ChatController instance**
    
    The [`ChatController`](./chatcontroller) is the interaction point with the SDK. You need it to create a chat.

    ```kotlin
    val chatController = ChatController.Builder(context)
                                          .build(messengerAccount, ChatLoadedListener)
    ```

4. **Display the chat on your activity**

    ChatController build, if was successfull, creates a fragment on which the chat UI will be displayed. The created fragment should be added to your app's activity.

    In order to get the chat fragment, implement the `ChatLoadedListener` interface and pass the implementation to `ChatController.Builder` `build` method.   
    `ChatLoadedListener:onComplete` will be called with the chat creation outcome as `ChatLoadResponse` instance.    
    `ChatLoadResponse` will contain the chat fragment if the chat was created properly. 

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

    > Verify that a chat fragment was not already been added to your activity. If one was added, make sure to remove it before adding the newly provided fragment.

5. **Release chat resources on activity destroy** 
- Activate [`ChatController.destruct()`](./chatcontroller#destructandrelease) when the `ChatController` instance is no longer needed. Destruct will release referenced open resources.

---

### [Code Sample](https://github.com/genesys/)
