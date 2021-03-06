### Riddle ### 
Riddle Logger:

[ ![Download](https://api.bintray.com/packages/vanlooverenkoen/maven/riddle/images/download.svg) ](https://bintray.com/vanlooverenkoen/maven/riddle/_latestVersion)

Riddle Network Interceptor:

[ ![Download](https://api.bintray.com/packages/vanlooverenkoen/maven/riddle-network-interceptor/images/download.svg) ](https://bintray.com/vanlooverenkoen/maven/riddle-network-interceptor/_latestVersion)

**What does it do?**

Riddle is a library you can import in your project to send your logs to the Riddle app. The Riddle app will be available soon. An overlay will be shown in Android where you can view all the logs by your app. You can also filter on certain parameters.

**How To Use**

Import in root gradle

    allprojects {
        repositories {
            ...
            maven { url "https://dl.bintray.com/vanlooverenkoen/maven" }
            ...
        }
    }

Apply the plugin by adding next command at the top of your app/build.gradle file

    dependencies {
        implementation "be.vanlooverenkoen:riddle:0.0.5"
        implementation "be.vanlooverenkoen:riddle-network-interceptor:0.0.2"
    }

***Setup Logger***

in your application file add the following. By default are all logTypes enabled. (Debug, Info, Verbose, Warn, Error, Assert). Make sure you only enable Riddle for debug builds.

        if (BuildConfig.DEBUG) {
            Riddle.with(this)
        }

***Configuration Logger***

If you want to enable or disable certain log types you need to pass only the logtypes you want to enable. The configuration below will enable logging for Debug, Error and Verbose. (Info, Warn and Assert will be disabled)

        if (BuildConfig.DEBUG) {
            Riddle.with(this)
                  .setLogTypes(RiddleLogType.DEBUG,
                               RiddleLogType.ERROR,
                               RiddleLogType.VERBOSE)
        }

***Usage Logger***

Just call the methods on Riddle:
 
        Riddle.d("Tag", "Debug Content")       
        Riddle.i("Tag", "Info Content")       
        Riddle.v("Tag", "Verbose Content")       
        Riddle.w("Tag", "Warn Content")       
        Riddle.a("Tag", "Assert Content")     
        Riddle.e("Tag", "Error Content")
        
        
 ***Setup Network Interceptor***

in your application file add the following. Make sure you only enable Riddle for debug builds.

        if (BuildConfig.DEBUG) {
            OkHttpClient.Builder()
                .addInterceptor(RiddleNetworkInterceptor(context, baseUrl))
                .build()
        }       
 
