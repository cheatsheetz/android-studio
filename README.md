# Android Studio Cheat Sheet

## Quick Reference

Android Studio is the official IDE for Android development, based on IntelliJ IDEA, providing tools for building, testing, and debugging Android applications.

### Installation and Setup

```bash
# Download from https://developer.android.com/studio

# System requirements:
# - 8 GB RAM minimum, 16 GB recommended
# - 4 GB disk space minimum
# - 1280 x 800 minimum screen resolution

# After installation, configure:
# 1. Android SDK location
# 2. JDK location (bundled or custom)
# 3. Emulator settings
# 4. Gradle settings
```

## Essential Keyboard Shortcuts

### Navigation
```
Ctrl+N / Cmd+N          - Go to class
Ctrl+Shift+N / Cmd+Shift+N - Go to file
Ctrl+Alt+Shift+N / Cmd+Alt+O - Go to symbol
Ctrl+E / Cmd+E          - Recent files
Ctrl+Shift+E / Cmd+Shift+E - Recent locations
Ctrl+B / Cmd+B          - Go to declaration
Ctrl+Alt+B / Cmd+Alt+B  - Go to implementation
Alt+F7 / Alt+F7         - Find usages
Ctrl+F12 / Cmd+F12      - File structure popup
```

### Editing
```
Ctrl+Space / Ctrl+Space     - Basic code completion
Ctrl+Shift+Space / Ctrl+Shift+Space - Smart code completion
Alt+Enter / Alt+Enter       - Show intention actions
Ctrl+/ / Cmd+/             - Comment/uncomment line
Ctrl+Shift+/ / Cmd+Shift+/ - Comment/uncomment block
Ctrl+D / Cmd+D             - Duplicate line
Ctrl+Y / Cmd+Delete        - Delete line
Ctrl+Shift+U / Cmd+Shift+U - Toggle case
```

### Refactoring
```
Shift+F6 / Shift+F6        - Rename
Ctrl+Alt+M / Cmd+Alt+M     - Extract method
Ctrl+Alt+V / Cmd+Alt+V     - Extract variable
Ctrl+Alt+F / Cmd+Alt+F     - Extract field
Ctrl+Alt+C / Cmd+Alt+C     - Extract constant
F6 / F6                    - Move
```

### Building and Running
```
Ctrl+F9 / Cmd+F9           - Build project
Shift+F10 / Ctrl+R         - Run
Shift+F9 / Ctrl+D          - Debug
Ctrl+F2 / Cmd+F2           - Stop
Ctrl+Shift+F10 / Ctrl+Shift+R - Run context configuration
```

## Project Structure

### Android Project Overview
```
MyApp/
├── .gradle/               # Gradle files
├── .idea/                 # IDE files
├── app/                   # Main application module
│   ├── build/            # Build outputs
│   ├── libs/             # Local libraries
│   ├── src/              # Source code
│   │   ├── androidTest/  # Instrumented tests
│   │   ├── main/         # Main source set
│   │   │   ├── java/     # Java/Kotlin source
│   │   │   ├── res/      # Resources
│   │   │   └── AndroidManifest.xml
│   │   └── test/         # Unit tests
│   └── build.gradle      # Module build file
├── gradle/               # Gradle wrapper
├── build.gradle          # Project build file
├── gradle.properties     # Gradle properties
└── settings.gradle       # Project settings
```

### Resource Structure
```
res/
├── drawable/             # Images, shapes, selectors
├── drawable-hdpi/        # High density images
├── drawable-mdpi/        # Medium density images
├── drawable-xhdpi/       # Extra high density images
├── drawable-xxhdpi/      # Extra extra high density images
├── drawable-xxxhdpi/     # Extra extra extra high density images
├── layout/               # UI layouts
├── layout-land/          # Landscape layouts
├── layout-sw600dp/       # Tablet layouts
├── menu/                 # Menu definitions
├── mipmap-*/            # App icons
├── raw/                  # Raw assets
├── values/               # Default values
├── values-night/         # Dark theme values
├── values-v21/           # API 21+ values
└── xml/                  # XML configurations
```

## IDE Features and Tools

### Code Generation

```kotlin
// Live templates (type and press Tab)
fun -> function template
psf -> public static final
fori -> for loop with index
iter -> enhanced for loop
inn -> if not null
ifn -> if null

// Generate code (Alt+Insert / Cmd+N)
// - Constructor
// - Getter/Setter
// - toString()
// - equals() and hashCode()
// - Override methods
```

### Layout Editor

```xml
<!-- Design view features -->
<!-- 1. Component Tree -->
<!-- 2. Design Surface -->
<!-- 3. Palette -->
<!-- 4. Attributes Panel -->

<!-- Constraint Layout example -->
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

### Code Analysis

```kotlin
// Code inspection highlights
// - Unused imports/variables
// - Potential null pointer exceptions
// - Performance issues
// - Code style violations

class MainActivity : AppCompatActivity() {
    
    // Suppress inspection
    @Suppress("UNUSED_PARAMETER")
    fun unusedMethod(param: String) {
        // Implementation
    }
    
    // Lint suppress
    @SuppressLint("SetTextI18n")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        textView.text = "Hello " + userName // Lint warning suppressed
    }
}
```

## Debugging Tools

### Debugger

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        val data = processData() // Set breakpoint here
        displayData(data)
    }
    
    private fun processData(): List<String> {
        val result = mutableListOf<String>()
        for (i in 1..10) {
            result.add("Item $i") // Conditional breakpoint: i == 5
        }
        return result
    }
}

// Debugger features:
// - Breakpoints (F9)
// - Step over (F8)
// - Step into (F7)
// - Step out (Shift+F8)
// - Evaluate expression (Alt+F8)
// - Watch variables
// - Call stack navigation
```

### Logcat

```kotlin
import android.util.Log

class LoggingExample {
    companion object {
        private const val TAG = "LoggingExample"
    }
    
    fun demonstrateLogging() {
        // Different log levels
        Log.v(TAG, "Verbose message")  // Verbose
        Log.d(TAG, "Debug message")    // Debug
        Log.i(TAG, "Info message")     // Info
        Log.w(TAG, "Warning message") // Warning
        Log.e(TAG, "Error message")   // Error
        
        // Log with exception
        try {
            riskyOperation()
        } catch (e: Exception) {
            Log.e(TAG, "Operation failed", e)
        }
    }
    
    private fun riskyOperation() {
        throw RuntimeException("Something went wrong")
    }
}

// Logcat filters:
// - by package name
// - by log level
// - by tag
// - custom regex filters
```

### Memory Profiler

```kotlin
// Memory leak detection
class MainActivity : AppCompatActivity() {
    
    // Potential memory leak - static reference
    companion object {
        private var staticContext: Context? = null
    }
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        // Bad practice - causes memory leak
        staticContext = this
        
        // Good practice - use application context
        val appContext = applicationContext
    }
    
    override fun onDestroy() {
        super.onDestroy()
        // Clean up references
        staticContext = null
    }
}

// Memory Profiler features:
// - Heap dumps
// - Memory allocation tracking
// - Garbage collection events
// - Memory leak detection
```

### Layout Inspector

```kotlin
// Use Layout Inspector to:
// 1. View the view hierarchy at runtime
// 2. Inspect view properties
// 3. Debug layout issues
// 4. Analyze view performance

// Access via: Tools -> Layout Inspector
// Or use adb command:
// adb shell am broadcast -a com.android.layoutinspector.ACTION_ACQUIRE_LAYOUT_DUMP
```

## Build System (Gradle)

### Module-level build.gradle

```kotlin
// app/build.gradle
android {
    namespace = "com.example.myapp"
    compileSdk = 34
    
    defaultConfig {
        applicationId = "com.example.myapp"
        minSdk = 21
        targetSdk = 34
        versionCode = 1
        versionName = "1.0"
        
        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
        
        // Build config fields
        buildConfigField("String", "API_URL", "\"https://api.example.com\"")
        buildConfigField("boolean", "DEBUG_MODE", "true")
    }
    
    buildTypes {
        debug {
            isDebuggable = true
            isMinifyEnabled = false
            applicationIdSuffix = ".debug"
            versionNameSuffix = "-debug"
            
            buildConfigField("String", "API_URL", "\"https://dev-api.example.com\"")
        }
        
        release {
            isMinifyEnabled = true
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
            
            buildConfigField("String", "API_URL", "\"https://api.example.com\"")
        }
    }
    
    productFlavors {
        create("free") {
            applicationIdSuffix = ".free"
            versionNameSuffix = "-free"
        }
        
        create("paid") {
            applicationIdSuffix = ".paid"
            versionNameSuffix = "-paid"
        }
    }
    
    buildFeatures {
        viewBinding = true
        dataBinding = true
        compose = true
    }
    
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_1_8
        targetCompatibility = JavaVersion.VERSION_1_8
    }
    
    kotlinOptions {
        jvmTarget = "1.8"
    }
}

dependencies {
    implementation("androidx.core:core-ktx:1.12.0")
    implementation("androidx.appcompat:appcompat:1.6.1")
    implementation("com.google.android.material:material:1.10.0")
    implementation("androidx.constraintlayout:constraintlayout:2.1.4")
    
    testImplementation("junit:junit:4.13.2")
    androidTestImplementation("androidx.test.ext:junit:1.1.5")
    androidTestImplementation("androidx.test.espresso:espresso-core:3.5.1")
    
    // Network
    implementation("com.squareup.retrofit2:retrofit:2.9.0")
    implementation("com.squareup.retrofit2:converter-gson:2.9.0")
    implementation("com.squareup.okhttp3:logging-interceptor:4.11.0")
    
    // Image loading
    implementation("com.github.bumptech.glide:glide:4.15.1")
    
    // Dependency injection
    implementation("com.google.dagger:dagger:2.47")
    kapt("com.google.dagger:dagger-compiler:2.47")
}
```

### Gradle Tasks

```bash
# Build tasks
./gradlew assembleDebug          # Build debug APK
./gradlew assembleRelease        # Build release APK
./gradlew bundleRelease          # Build release AAB
./gradlew installDebug           # Install debug build on device

# Testing tasks
./gradlew test                   # Run unit tests
./gradlew connectedAndroidTest   # Run instrumented tests
./gradlew testDebugUnitTest      # Run debug unit tests

# Cleanup tasks
./gradlew clean                  # Clean build directory
./gradlew cleanBuildCache        # Clean build cache

# Dependency tasks
./gradlew dependencies           # Show all dependencies
./gradlew dependencyUpdates      # Check for dependency updates

# Custom tasks
./gradlew tasks                  # List available tasks
```

## Testing Framework

### Unit Testing

```kotlin
// ExampleUnitTest.kt
import org.junit.Test
import org.junit.Assert.*
import org.junit.Before
import org.mockito.Mock
import org.mockito.Mockito.*
import org.mockito.MockitoAnnotations

class CalculatorTest {
    
    private lateinit var calculator: Calculator
    
    @Before
    fun setup() {
        calculator = Calculator()
    }
    
    @Test
    fun addition_isCorrect() {
        assertEquals(4, calculator.add(2, 2))
    }
    
    @Test
    fun division_byZero_throwsException() {
        assertThrows(ArithmeticException::class.java) {
            calculator.divide(10, 0)
        }
    }
}

// Mockito example
class UserServiceTest {
    
    @Mock
    private lateinit var userRepository: UserRepository
    
    private lateinit var userService: UserService
    
    @Before
    fun setup() {
        MockitoAnnotations.openMocks(this)
        userService = UserService(userRepository)
    }
    
    @Test
    fun getUserById_returnsUser() {
        // Given
        val userId = "123"
        val expectedUser = User(userId, "John Doe")
        `when`(userRepository.findById(userId)).thenReturn(expectedUser)
        
        // When
        val result = userService.getUserById(userId)
        
        // Then
        assertEquals(expectedUser, result)
        verify(userRepository).findById(userId)
    }
}
```

### Instrumented Testing

```kotlin
// ExampleInstrumentedTest.kt
import androidx.test.ext.junit.runners.AndroidJUnit4
import androidx.test.platform.app.InstrumentationRegistry
import androidx.test.ext.junit.rules.ActivityScenarioRule
import androidx.test.espresso.Espresso.onView
import androidx.test.espresso.action.ViewActions.*
import androidx.test.espresso.assertion.ViewAssertions.matches
import androidx.test.espresso.matcher.ViewMatchers.*
import org.junit.Rule
import org.junit.Test
import org.junit.runner.RunWith

@RunWith(AndroidJUnit4::class)
class MainActivityTest {
    
    @get:Rule
    val activityRule = ActivityScenarioRule(MainActivity::class.java)
    
    @Test
    fun useAppContext() {
        // Context of the app under test
        val appContext = InstrumentationRegistry.getInstrumentation().targetContext
        assertEquals("com.example.myapp", appContext.packageName)
    }
    
    @Test
    fun testButtonClick() {
        // Type text and click button
        onView(withId(R.id.editText))
            .perform(typeText("Hello World!"), closeSoftKeyboard())
            
        onView(withId(R.id.button))
            .perform(click())
            
        // Check if text appears
        onView(withId(R.id.textView))
            .check(matches(withText("Hello World!")))
    }
    
    @Test
    fun testRecyclerView() {
        // Test RecyclerView interactions
        onView(withId(R.id.recyclerView))
            .perform(RecyclerViewActions.actionOnItemAtPosition<RecyclerView.ViewHolder>(0, click()))
            
        // Verify navigation
        onView(withText("Detail Screen"))
            .check(matches(isDisplayed()))
    }
}
```

## Emulator and Device Management

### AVD Manager

```bash
# Command line tools
# List available AVDs
emulator -list-avds

# Start emulator
emulator -avd Pixel_4_API_30

# Start emulator with specific options
emulator -avd Pixel_4_API_30 -gpu host -memory 2048 -cores 4

# Create AVD from command line
avdmanager create avd -n "TestDevice" -k "system-images;android-30;google_apis;x86_64"
```

### Device Connection

```bash
# ADB commands
adb devices                    # List connected devices
adb connect 192.168.1.100:5555 # Connect via WiFi
adb disconnect                 # Disconnect all devices

# Install/Uninstall
adb install app-debug.apk      # Install APK
adb uninstall com.example.app  # Uninstall app

# File operations
adb push local.txt /sdcard/    # Push file to device
adb pull /sdcard/file.txt .    # Pull file from device

# Shell access
adb shell                      # Open shell
adb shell pm list packages     # List installed packages
adb shell am start -n com.example.app/.MainActivity  # Start activity

# Logging
adb logcat                     # View logs
adb logcat -c                  # Clear logs
adb logcat MyTag:D *:S         # Filter logs
```

## Performance Analysis

### CPU Profiler

```kotlin
class PerformanceExample {
    
    fun performHeavyTask() {
        // This will show up in CPU profiler
        repeat(1000000) {
            // Simulate heavy computation
            Math.sqrt(it.toDouble())
        }
    }
    
    // Use Trace API for custom profiling
    fun customProfiling() {
        Trace.beginSection("CustomOperation")
        try {
            // Your code here
            performCustomOperation()
        } finally {
            Trace.endSection()
        }
    }
    
    private fun performCustomOperation() {
        // Custom operation implementation
    }
}
```

### Network Profiler

```kotlin
// Network profiler automatically tracks:
// - HTTP requests
// - Response times
// - Data transfer
// - Connection states

class NetworkExample {
    
    fun makeNetworkCall() {
        // This will be tracked in Network Profiler
        val client = OkHttpClient()
        val request = Request.Builder()
            .url("https://api.example.com/data")
            .build()
            
        client.newCall(request).enqueue(object : Callback {
            override fun onResponse(call: Call, response: Response) {
                // Handle response
            }
            
            override fun onFailure(call: Call, e: IOException) {
                // Handle failure
            }
        })
    }
}
```

## Code Quality Tools

### Lint Configuration

```xml
<!-- lint.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<lint>
    <!-- Disable specific checks -->
    <issue id="HardcodedText" severity="ignore" />
    
    <!-- Make warning an error -->
    <issue id="UnusedResources" severity="error" />
    
    <!-- Ignore specific files -->
    <issue id="ContentDescription">
        <ignore path="src/debug/**" />
    </issue>
    
    <!-- Ignore specific resources -->
    <issue id="IconMissingDensityFolder">
        <ignore regexp="ic_launcher.*\.png" />
    </issue>
</lint>
```

### ProGuard/R8 Configuration

```pro
# proguard-rules.pro

# Keep application class
-keep class com.example.myapp.MyApplication

# Keep model classes for JSON serialization
-keep class com.example.myapp.model.** { *; }

# Keep Retrofit interfaces
-keepclasseswithmembers class * {
    @retrofit2.http.* <methods>;
}

# Keep Glide classes
-keep public class * implements com.bumptech.glide.module.GlideModule
-keep class * extends com.bumptech.glide.module.AppGlideModule {
 <init>(...);
}

# Remove logging in release builds
-assumenosideeffects class android.util.Log {
    public static *** d(...);
    public static *** v(...);
    public static *** i(...);
}
```

## Version Control Integration

### Git Integration

```bash
# Android Studio Git features:
# 1. VCS menu for all operations
# 2. Built-in diff viewer
# 3. Commit and push directly from IDE
# 4. Branch management
# 5. Merge conflict resolution
# 6. History and annotations

# Useful .gitignore for Android projects:
*.iml
.gradle
/local.properties
/.idea/
.DS_Store
/build
/captures
.externalNativeBuild
.cxx
local.properties
```

### Code Review

```kotlin
// Use Android Studio for code reviews:
// 1. Compare with branch
// 2. View file history
// 3. Annotate lines with blame
// 4. Create patches

// Best practices:
// - Follow Android coding standards
// - Use meaningful commit messages
// - Keep commits atomic
// - Review before merging
```

## Plugins and Extensions

### Essential Plugins

```
1. Kotlin Multiplatform Mobile
2. Flutter
3. Database Navigator
4. Rainbow Brackets
5. String Manipulation
6. Key Promoter X
7. GitToolBox
8. ADB Idea
9. Codota AI Autocomplete
10. SonarLint
```

### Plugin Development

```kotlin
// Create custom plugin for Android Studio
// File -> New -> Plugin Development -> IDE Plugin

// plugin.xml
<idea-plugin>
    <id>com.example.myplugin</id>
    <name>My Plugin</name>
    <version>1.0</version>
    <vendor>Your Name</vendor>
    
    <depends>com.intellij.modules.platform</depends>
    <depends>org.jetbrains.android</depends>
    
    <extensions defaultExtensionNs="com.intellij">
        <toolWindow id="MyToolWindow"
                   secondary="true"
                   anchor="right"
                   factoryClass="com.example.myplugin.MyToolWindowFactory"/>
    </extensions>
    
    <actions>
        <action id="MyAction"
               class="com.example.myplugin.MyAction"
               text="My Action"
               description="My custom action">
            <add-to-group group-id="EditorPopupMenu" anchor="first"/>
        </action>
    </actions>
</idea-plugin>
```

## Optimization Tips

### IDE Performance

```
# Optimize Android Studio performance:

# 1. Increase memory allocation
# studio.vmoptions:
-Xms2048m
-Xmx8192m
-XX:MaxPermSize=512m
-XX:ReservedCodeCacheSize=512m

# 2. Disable unused plugins
# File -> Settings -> Plugins

# 3. Exclude unnecessary folders from indexing
# File -> Settings -> Build -> Compiler -> Excludes

# 4. Use power save mode for better battery life
# File -> Power Save Mode

# 5. Configure Gradle daemon
# gradle.properties:
org.gradle.daemon=true
org.gradle.jvmargs=-Xmx4g -XX:+HeapDumpOnOutOfMemoryError
org.gradle.parallel=true
org.gradle.configureondemand=true
```

### Build Optimization

```kotlin
// build.gradle optimizations
android {
    // Enable build cache
    buildCache {
        local {
            enabled = true
        }
    }
    
    // Enable incremental compilation
    compileOptions {
        incremental = true
    }
    
    // Use parallel GC
    dexOptions {
        javaMaxHeapSize "4g"
        preDexLibraries = true
    }
}
```

## Official Resources

- [Android Studio User Guide](https://developer.android.com/studio/intro)
- [Android Studio Release Notes](https://developer.android.com/studio/releases)
- [IntelliJ IDEA Documentation](https://www.jetbrains.com/help/idea/)
- [Android Developer Documentation](https://developer.android.com/docs)
- [Gradle Build Tool](https://gradle.org/guides/)

## Community and Tools

- [Android Studio Tips & Tricks](https://developer.android.com/studio/intro/tips)
- [Android Studio Project Site](https://androidstudio.googleblog.com/)
- [Stack Overflow - Android Studio](https://stackoverflow.com/questions/tagged/android-studio)
- [Reddit r/androiddev](https://www.reddit.com/r/androiddev/)
- [Android Studio Shortcuts PDF](https://developer.android.com/studio/intro/keyboard-shortcuts)