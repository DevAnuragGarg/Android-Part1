# Android-Part1

View and ViewGroup
1) View objects are the basic building blocks of User Interface(UI) elements in Android. ViewGroup is the invisible container. It holds View and ViewGroup
2) View is a simple rectangle box which responds to the user's actions. Examples are EditText, Button, CheckBox etc. LinearLayout is the ViewGroup that contains Button(View), and other Layouts also.
3) View refers to the android.view.View class, which is the base class of all UI classes. ViewGroup is the base class for Layouts.

======
URI: A URI (Uniform Resource Identifier) is a sequence of characters that identifies a logical or physical resource. URL: In computing, a Uniform Resource Locater (URL) is a subset of the Uniform Resource Identifier (URI) that specifies where an identified resource is available and the mechanism for retrieving it. The URL shows you where you can find the database on the Internet and which protocol you should use.

======
Projection and Selection: Projection means choosing which columns (or expressions) the query shall return. Selection means which rows are to be returned. In sqlite the query is written like Cursor cursor = sqLiteDatabase.query(tableName, tableColumns, whereClause, whereArgs, groupBy, having, orderBy);

======
No to Nested Linear Layout: Nested weights of Linear layout will hit the performance badly. Layout weights require a widget to be measured twice. When a LinearLayout with non-zero weights is nested inside another LinearLayout with non-zero weights, then the number of measurements increase exponentially. When using ConstraintLayout, you should not use match_parent. Instead, set the dimension to 0dp to enable a special behavior called "match constraints," which is generally the same as what you expect from match_parent.

======
MipMap folder: It’s best practice to place your app icons in mipmap- folders (not the drawable- folders) because they are used at resolutions different from the device’s current density. When referencing the mipmap-folders ensure you are using the following reference: android:icon="@mipmap/ic_launcher". The reason they use a different density is that some launchers actually display the icons larger than they were intended. Because of this, they use the next size up.

======
Device configuration: When you declare your activity to handle a configuration change, you are responsible for resetting any elements for which you provide alternatives. If you declare your activity to handle the orientation change and have images that should change between landscape and portrait, you must re-assign each resource to each element during onConfigurationChanged().

======
Realm is a mobile database and a replacement for SQLite. Although is an OO database it has some differences with other databases. Realm is not using SQLite as it’s engine. Instead it has own C++ core and aims to provide a mobile-first alternative to SQLite. Realm store data in a universal, table-based format by a C++ core. This is what allows Realm to allow data access from multiple languages as well as a range of ad hoc queries.
Below are the advantages of Realm over SQLite:
> faster than SQLite (up to 10x speed up over raw SQLite for normal operations)
> easy to use
> object conversion handled for you
> convenient for creating and storing data on the fly
> very responsive team

======
Activity, AppCompatActivity, FragmentActivity and ActionBarActivity. How are they related:
- Activity is the base class. 
- FragmentActivity extends Activity: FragmentActivity is used for fragments. Since the build version 22.1.0 of the support library
- AppCompatActivity extends FragmentActivity with AppCompatCallback implemented: AppCompatActivity is the base class of the support library. It has come up with many new features like ToolBar, tinted widgets, material design color pallets. It provides backward compatibility for other material design components till SDK version 7
- ActionBarActivity extends AppCompatActivity: ActionBarActivity is deprecated. It was the base class of appcompat-v7

======
RecyclerView vs ListView
1) A RecyclerView recycles and reuses cells when scrolling. This is a default behavior. It’s possible to implement the same in a ListView too but we need to implement a ViewHolder there
2) A RecyclerView decouples list from its container so we can put list items easily at run time in the different containers (linearLayout, gridLayout) by setting LayoutManager
3) Animations of RecyclerView items are decoupled and delegated to ItemAnimator

======
Handler: Typically it is used to perform an action on a different thread than your own. It is also used to schedule messages and runnable to be executed at some point in the future.

======
When does the system directly call “onDestroy()” after it called “onCreate(Bundle)”? (without calling onStart(), onResume(), onStop(), onPause()). By calling finish() within the onCreate(Bundle) method, the system does not call any further lifecycle methods except onDestroy().

======
Why isn’t it a good idea to start a thread when a BroadcastReceiver receives an Intent in its onReceive() method? How can you solve this issue: As soon as the execution of onReceive() is finished, the system may kill the process at any time (and that will also kill the spawned thread): A good way is to use a JobService/WorkManager instead of a thread. By doing so, the system knows that the process is still needed.

======
What is the difference between px, dp and sp?
- px (Pixel): corresponds to actual pixels on the screen
- dp (Density-independent Pixel): abstract unit that is based on the physical density of the screen. One dp is one pixel on a 160 dpi screen (the unit is relative to a 160 dpi screen), but one dp equals two hardware pixels on a 320 dpi screen
- sp (Scale-independent Pixel): same as dp but it is also scaled by the user’s font size preference. This unit is used to specify font sizes.

======
What happens with your app if the device goes into “Doze Mode”: Scheduled alarms (via AlarmManager), jobs (via JobScheduler), and syncs (via SyncManager) will be ignored by default, except during occasional “idle maintenance windows”.

======
What about show/hide: FragmentTransaction does have two additional methods - show and hide. No lifecycle methods are called, and every aspect of the fragment instance is held in memory (including the view hierarchy). If you create a lot of fragments, hide them, and add new ones on top (why you would do this I do not know), you will run out of memory sooner or later.

======
What would you use to interact with Activity from Service: Create a bound service, Use RxJAVA, Event Bus, Broadcast Receiver

======
Why cannot you run standard Java bytecode on Android: A: It's Because Java(on you computer) and Android use separate environment to run the code. Android has been modified to run on small devices with exhaustion of less computing power. Android uses the Dalvik VM, instead of the Java VM. Additionally, Android programs are supported by various XML files like the Android Manifest, layout files, resource files etc. The Android Manifest is especially important, as it contains information on which part of the app can be launched, which is a service or a receiver, what permissions the apps needs, what hardware and software features the app needs, which version of Android is compatible with it etc.

======
How much is the android' bundle size limit: It depends on the purpose of the bundle. The bundle itself is only limited by the amount of memory. The total size for all binder transactions in a process is 1MB. If you exceed this limit you will receive this fatal error "!!! FAILED BINDER TRANSACTION !!!"

======
There are four Java classes related to the use of sensors on the Android platform. List them and explain the purpose of each.
1.Sensor: Provides methods to identify which capabilities are available for a specific sensor.
2.SensorManager: Provides methods for registering sensor event listeners and calibrating sensors.
4.SensorEvent: Provides raw sensor data, including information regarding accuracy.
5.SensorEventListener: Interface that defines callback methods that will receive sensor event notifications.

======
Which dialog boxes can you use in your Android application?
1) AlertDialog : An alert dialog box supports 0 to 3 buttons and a list of selectable elements, including check boxes and radio buttons. Among the other dialog boxes, the most suggested dialog box is the alert dialog box.
2) ProgressDialog : This dialog box displays a progress wheel or a progress bar. It is an extension of AlertDialog and supports adding buttons.
3) DatePickerDialog : This dialog box is used for selecting a date by the user.
4) TimePickerDialog : This dialog box is used for selecting time by the user.

======
What is required to have the parallel working of the AsyncTasks
Async task with executors
@TargetApi(Build.VERSION_CODES.HONEYCOMB) // API 11
public static <T> void executeAsyncTask(AsyncTask<T, ?, ?> asyncTask, T... params) {
    if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB)
        asyncTask.executeOnExecutor(AsyncTask.THREAD_POOL_EXECUTOR, params);
    else
        asyncTask.execute(params);
} 
When first introduced, AsyncTasks were executed serially on a single background thread. Starting with DONUT, this was changed to a pool of threads allowing multiple tasks to operate in parallel. After HONEYCOMB, it is planned to change this back to a single thread to avoid common application errors caused by parallel execution. If you truly want parallel execution, you can use the executeOnExecutor(Executor, Params...) version of this method with THREAD_POOL_EXECUTOR.

======
Memory Leak causing issues
- Registering listeners
- Android Memory Monitor and get Dump Java Heap
- Inner classes
- Anonymous classes
- A BroadcastReceiver hasn't finished executing within 10 seconds.
Favor static inner classes over non-static. Each non-static inner class will have an implicit reference to its outer class instance which may result in unwanted behaviors. Instead define these classes as static and store life cycle references needed as WeakReferences. Memory leaks happen when you hold on to an object long after its purpose have been served. Garbage collection is a heavy process, so the less the garbage collector runs, the better for your app. As the app is being used and the heap memory keeps on increasing, a short GC will kick off and try to clear up immediate dead objects. Now these short GCs run concurrently (on a separate thread) and doesn’t slow down your app (2–5 ms pause) at all.

======
Context means context of the current state of the application/object. Context is a handle to the system, it provides services like resolving resources, obtaining access to databases and preferences, and so on. An Android app has activities. It’s like a handle to the environment your application is currently running in. The activity object inherits the Context object. It allows access to application specific resources and class and information about the application environment. 
Application Context: It is an instance which is the singleton and can be accessed in an activity via getApplicationContext(). This context is tied to the lifecycle of an application. The application context can be used where you need a context whose lifecycle is separate from the current context or when you are passing a context beyond the scope of an activity.

======
Surface view Vs view: SurfaceViews contain a nice rendering mechanism that allows threads to update the surface's content without using a handler (good for animation).
- Surface views cannot be transparent, they can only appear behind other elements in the view hierarchy.
- they are much faster for animation than rendering onto a View.
- The main difference is that SurfaceView can be drawn on by background threads
- They are not hardware accelerated.
- Normal views are rendered when you call the methods invalidate or postInvalidate(), but this does not mean the view will be immediately updated. The SurfaceView can be immediately updated.
- A SurfaceView has an allocated surface buffer, so it is more costly

======
IllegalStateException: Signals that a method has been invoked at an illegal or inappropriate time. In other words, the Java environment or Java application is not in an appropriate state for the requested operation.

======
Difference between v4 and v7: v4 Support Library: This library is designed to be used with Android 1.6 (API level 4) Android 2.3 (API level 9) and higher. It includes the largest set of APIs compared to the other libraries, including support for application components, user interface features, accessibility, data handling, network connectivity, and programming utilities.
v7 Libraries: There are several libraries designed to be used with Android 2.1 (API level 7) Android 2.3 (API level 9) and higher. These libraries provide specific feature sets and can be included in your application independently from each other.
v7 appcompat library: This library adds support for the Action Bar user interface design pattern.

======
Nine patch image vs png: A: It is a re-sizable bitmap resource that can be used for backgrounds or other images on the device. NinePatch class permits drawing a bitmap in nine sections. The nine patch images have extension as.9.png. It allows extension in 9 ways, i.e. 4 corners that are unscaled, 4 edges that are scaled in 1 axis, and the middle one that can be scaled into both axes.

======
ADB: stands for Android Debug Bridge. It is a command line tool that is used to communicate with the emulator instance. ADB can control your device over USB from a computer, copy files back and forth, install and uninstalled apps, run shell commands, and more. It is a client-server program that includes three components:
• A client, which runs on your development machine. You can invoke a client from a shell by issuing an ADB command. Other Android tools such as DDMS also create ADB clients.
• A server, which runs as a background process on your development machine. The server manages communication between the client and the ADB daemon running on an emulator or device.
• A daemon, which runs as a background process on each emulator or device instance.

======
How two Android apps share same Linux ID and share same VM? The applications must sign with the same certificate in order to share same Linux user ID and share same VM.

======
Can you deploy executable JARs on Android? Which packaging is supported by Android? No, Android platform does not support JAR deployments. Applications are packed into Android Package (.apk) using Android Asset Packaging Tool (AAPT) and then deployed onto Android platform.

======
What is the maximum size of the payload in notifications? 4KB

======
Observer and Observable: They are part of java util class. Observer is a class and Observable is a interface. Observer maintains which observer has been added or removed and provide call back to all the observers on data changes. Classes implementing Observable addToObserver their instance and get callback if any data set is changed. They can get data with callback too.

======
What is attachToRoot in inflating the layout in onCreateView for fragment: If set to true then when your layout is inflated it will be automatically added to the view hierarchy of the ViewGroup specified in the 2nd parameter as a child. Attaches the views to their parent (includes them in the parent hierarchy), so any touch event that the views recieve will also be transfered to parent view. Now it's upto the parent whether it wants to entertain those events or ignore them. if set to false, they are not added as direct children of the parent and the parent doesn't recieve any touch events from the views.
Also the container which is the second argument: The ViewGroup to be the parent of the inflated layout. Passing the container is important in order for the system to apply layout parameters to the root view of the inflated layout, specified by the parent view in which it's going.

======
Difference between getSupportFragmentManager() and getFragmentManager(): Use getSupportFragmentManager() instead of getFragmentManager(). AppCompatActivity is v4 library therefore required to use v4 functions and to use it in Activity instead of Activity change it to FragmentActivity. Then you can use getSupportFragmentManager()requestWindowFeature() is not supported in AppCompatActivity thats why you could not use that method with AppCompatActivity. Also if you are using AppCompatActivity you need to use SupportFragment and if you use Activity then use Fragment.

======
What are the features of FragmentManager?
1) Get fragments that exist in the activity, with findFragmentById() (for fragments that provide a UI in the activity layout) or findFragmentByTag() (for fragments that do or don't provide a UI).
2) Pop fragments off the back stack, with popBackStack() (simulating a Back command by the user).
3) Register a listener for changes to the back stack, with addOnBackStackChangedListener().

======
What is required to have menu options in Fragment: setHasOptionsMenu(). You can also register a view in your fragment layout to provide a context menu by calling registerForContextMenu(). When the user opens the context menu, the fragment receives a call to onCreateContextMenu(). When the user selects an item, the fragment receives a call to onContextItemSelected().

======
ANR: Android will display the ANR dialog for a particular application when it detects one of the following conditions: No response to an input event (such as key press or screen touch events) within 5 seconds. A BroadcastReceiver hasn't finished executing within 10 seconds.

======
MinifyEnabled vs ShrinkResources: minify runs ProGuard. shrink remove resources that ProGuard flagged as unused. ProGuard shrinks CODE ONLY; shrinkResources it's just the stuff from the /res/ folder. shrinkResources depends on the log output from ProGuard to run. ProGuard is the one who actually analyses the code to know what is unused.

======
SNAPDEAL: Reducing the size of APK: 
- Android Studio APK Analyzer: APK Analyzer will tear down your application and let you know which component in your .apk file is taking the larger amount of space
- Enabling Proguard which is replaced by R8, will reduce the apk size by removing unused methods and classes.
- we can remove the unused resources from our application by mentioning shrinkResources true
- also mentioning resConfigs "en" in the release buildTypes will remove all other localized resources while building the application
- use of svg images in place of using images separately for different densities. The average amount of space that images use in these top apps is over 44% of the download size.
- Use apk splits
- No need to put the fonts files in the asset folder. Now there is a feature called Down-loadable Fonts in Android API 26 (Oreo) and Support Library 26. No longer need to package a font with your application, and a user will only have to download a font once, and it’ll be reused in different applications. 
- to gain immediate app size savings when publishing to Google Play is by uploading your app as an Android App Bundle, which is a new upload format that includes all your app’s compiled code and resources, but defers APK generation and signing to Google Play
- minimize usage of libraries unnecessarily. Like whole google play services package should not be used but to use a specific feature of google play services is recommended.
- Avoid enumerations: A single enum can add about 1.0 to 1.4 KB of size to your app's classes.dex file.
- Avoid extracting native libraries: When building the release version of your app, package uncompressed .so files in the APK by setting android:extractNativeLibs="false" in the <application> element of your app's manifest. Disabling this flag prevents PackageManager from copying .so files from the APK to the file system during installation and has the added benefit of making updates of your app smaller.
- Your APK might contain content that users download but never use, like additional language or per-screen-density resources. To ensure a minimal download for your users, you should upload your app to Google Play using Android App Bundles. Uploading app bundles let's Google Play generate and serve optimized APKs for each user’s device configuration, so they download only the code and resources they need to run your app. You no longer have to build, sign, and manage multiple APKs to support different devices, and users get smaller, more optimized downloads.

======
Back up user data with Auto Backup: Auto Backup for Apps automatically backs up a user's data from apps that target and run on Android 6.0 (API level 23) or later. Android preserves app data by uploading it to the user's Google Drive—where it's protected by the user's Google Account credentials. The amount of data is limited to 25MB per user of your app and there's no charge for storing backup data. By default, Auto Backup includes files in most of the directories that are assigned to your app by the system:
- Shared preferences files.
- Files saved to your app's internal storage, accessed by getFilesDir() or getDir(String, int).
- Files in the directory returned by getDatabasePath(String), which also includes files created with the SQLiteOpenHelper class.
- Files on external storage in the directory returned by getExternalFilesDir(String).
Auto Backup excludes files in directories returned by getCacheDir(), getCodeCacheDir(), or getNoBackupFilesDir().
- Backup data is stored in a private folder in the user's Google Drive account, limited to 25MB per app. The saved data does not count towards the user's personal Google Drive quota. Only the most recent backup is stored. When a backup is made, the previous backup (if one exists) is deleted. The backup data can't be read by the user or other apps on the device.

You can leverage auto backup in your Android app so that your users can more quickly recover their data if they ever switch phones or reinstall your app after having uninstalled it. If the user deletes the app in any way, including via a factory reset of their device, the data for the app will still be available when the user re-downloads the app and the .apk is installed. Auto Backup also works across devices, meaning that when your user gets a new phone, they won’t lose key information from your app.
Users are first prompted to enable Auto Backup when setting up their phone for the first time. If they need to do so after the fact, they can enable back ups of their data by navigating to Settings -> Backup & Reset, and opting in to having their data stored on their Google Drive.

======
What is difference between include tag and merge tag
<include>: Inside the layout to which you want to add the re-usable component, add the <include/> tag. You can also override all the layout parameters (any android:layout_* attributes) of the included layout's root view by specifying them in the <include/> tag. However, if you want to override layout attributes using the <include> tag, you must override both android:layout_height and android:layout_width in order for other layout attributes to take effect.

<merge>: The <merge /> tag helps eliminate redundant view groups in your view hierarchy when including one layout within another. For example, if your main layout is a vertical LinearLayout in which two consecutive views can be re-used in multiple layouts, then the re-usable layout in which you place the two views requires its own root view. However, using another LinearLayout as the root for the re-usable layout would result in a vertical LinearLayout inside a vertical LinearLayout. The nested LinearLayout serves no real purpose other than to slow down your UI performance. To avoid including such a redundant view group, you can instead use the <merge> element as the root view for the re-usable layout. Now, when you include this layout in another layout (using the <include/> tag), the system ignores the <merge> element and places the two buttons directly in the layout, in place of the <include/> tag.

======
Does BroadcastReceiver.onReceive always run in the UI thread? Yes.

======
If a new activity or dialog appears in the foreground, taking focus and partially covering the activity in progress, the covered activity loses focus and enters the Paused state. Then, the system calls onPause() on it.

======
The Binder transaction buffer has a limited fixed size, currently 1MB, which is shared by all transactions in progress for the process. Since this limit is at the process level rather than at the per activity level, these transactions include all binder transactions in the app such as onSaveInstanceState, startActivity and any interaction with the system. When the size limit is exceeded, a TransactionTooLargeException is thrown.

======
Saved instance state bundles persist both configuration changes and process death, but are limited by amount of storage and speed because onSavedInstanceState() serializes data to disk. Serialization can consume a lot of memory if the objects being serialized are complicated. Because this process happens on the main thread during a configuration change, serialization can cause dropped frames and visual stutter if it takes too long. Do not use store onSavedInstanceState() to store large amounts of data, such as bitmaps, nor complex data structures that require lengthy serialization or deserialization. Instead, store only primitive types and simple, small objects such as String. 

======
NAGARRO, URBANCLAP
Compared to Volley, Retrofit's REST API code is brief and provides excellent API documentation and has good support in communities. It is provided from square. Moreover now, google sites also mention about the retrofit. We can also use Retofit with RX creating observables. Also, retrofit is a wrapper written on the okhttp having many more feautures like dynamic url generation. Also, difference from volley is it automatically can provide the response object using GSON converter library.

======
Retrofit vs. OkHttp The reason is simple: OkHttp is a pure HTTP/SPDY client responsible for any low-level network operation, caching, request and response manipulation, and many more. In contrast, Retrofit is a high-level REST abstraction build on top of OkHttp. Retrofit 2 is strongly coupled with OkHttp and makes intensive use of it.

OkHttp Functions: Connection pooling, gzipping, caching, recovers from network problems, sync, and async calls, redirects, retries … and so on.

Retrofit Functions: URL manipulation, requesting, loading, caching, threading, synchronization... It allows sync and async calls.

======
How two applications can share data?
- Content providers
- The Android system provides signature-based permissions enforcement, so that an application can expose functionality to another application that is signed with a specified certificate. By signing multiple applications with the same certificate and using signature-based permissions checks, your applications can share code and data in a secure manner.

======
Gravity vs LayoutGravity
android:gravity sets the gravity of the contents (i.e. its subviews) of the View it's used on.
android:layout_gravity sets the gravity of the View or Layout relative to its parent.

======
FrameLayout is designed to block out an area on the screen to display a single item. Generally, FrameLayout should be used to hold a single child view, because it can be difficult to organize child views in a way that's scalable to different screen sizes without the children overlapping each other. You can, however, add multiple children to a FrameLayout and control their position within the FrameLayout by assigning gravity to each child, using the android:layout_gravity attribute. Child views are drawn in a stack, with the most recently added child on top. The size of the FrameLayout is the size of its largest child (plus padding), visible or not

======
View is attached to the window manager when the activity is visible. We generally get "View not attached to window manager crash". We can reproduce, enable this option on your device: Settings -> Developer Options -> Don't keep Activities. Press Home button while the AsyncTask is executing and the ProgressDialog is showing.
The Android OS will destroy an activity as soon as it is hidden. When onPostExecute is called the Activity will be in "finishing" state and the ProgressDialog will be not attached to Activity. Resolving this issue, by checking the activity state by using method "isDestroyed()". Also, dismiss the ProgressDialog in onDestroy method. Otherwise, android.view.WindowLeaked exception will be thrown. This exception usually comes from dialogs that are still active when the activity is finishing.
