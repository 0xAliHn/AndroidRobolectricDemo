## Android Studio Robolectric Test Sample
This example project shows how to use robolectric, junit and assertJ with your gradle-based Android Studio projects.

### To set up from a new Android Studio Project: 
Add test dependencies on assertj-android and Robolectric to your module's build.gradle file. Your app module's app/build.gradle file would look something like this:
  
    testCompile 'com.squareup.assertj:assertj-android:1.1.0'
    testCompile 'org.robolectric:robolectric:3.0'
```

1. Select "Unit Tests" under "Build Variants"
 <img src="https://www.evernote.com/shard/s313/sh/560c4b5f-e70b-4800-b46f-bc1968618338/89c1e740e7134316961a103021daf1cb/deep/0/MyActivityTest.java---android-studio-robolectric-example------code-android-studio-robolectric-example-.png" width="600">

2.Update default JUnit working directory. Select *Run/Debug Configurations*, then *Defaults*, then *JUnit*, then *Configurations* tab, then *Working directory*, and finally *MODULE_DIR*.: ![default JUnit working directory](readme_images/junit_default_working_dir.png)

5. ctrl + click on the test and select Run MyActivityTest. ![run test menu item](readme_images/run_test.png)

6. Create your unit test in src/test/java/com.example.joshskeen.myapplication/MyActivityTest.java:
```java
@RunWith(RobolectricGradleTestRunner.class)
@Config(constants = BuildConfig.class, sdk = 21)
public class MyActivityTest {

    private MyActivity mActivity;

    @Before
    public void setup() {
        mActivity = Robolectric.buildActivity(MyActivity.class).create().get();
    }

    @Test
    public void myActivityAppearsAsExpectedInitially() {
        assertThat(mActivity.mClickMeButton).hasText("Click me!");
        assertThat(mActivity.mHelloWorldTextView).hasText("Hello world!");
    }

    @Test
    public void clickingClickMeButtonChangesHelloWorldText() {
        assertThat(mActivity.mHelloWorldTextView).hasText("Hello world!");
        mActivity.mClickMeButton.performClick();
        assertThat(mActivity.mHelloWorldTextView).hasText("HEY WORLD");
    }

}
```

Now write Robolectric tests! For more intel on how to write tests using robolectric + assertJ, check out [http://blog.bignerdranch.com/2583-testing-the-android-way/](http://blog.bignerdranch.com/2583-testing-the-android-way/)


