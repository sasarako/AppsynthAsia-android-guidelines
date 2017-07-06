# READ ME 
I write this wiki because some part of our convention is not follow the google guideline in this [link](https://github.com/ribot/android-guidelines/blob/master/project_and_code_guidelines.md). and I put most of conventions in here because it easy to us to see all conventions in one place (no need to swap between 2 sites).

# 1. Project guidelines
## 1.1 Project structure
We will apply a part of clean architecture to our project structure.
Our project will consist of 3 main modules that are `data`, `domain` and `presentation` and other modules if necessary such as `extensions` and `utils`.

The project structure will be like this:

<pre>
    - <b>data</b>
        -- shared
        -- api
        -- entity
        -- repository
    - <b>domain</b>
        -- shared
        -- usecase
        -- manager
    - <b>presentation</b>
        -- shared
        -- feature1(MVP, MVVM)
        -- login
            --- LoginActivity
            --- LoginPresenter
            --- LoginAdapter
    - <b>extensions</b>
    - <b>utils</b>
</pre>

## 1.2 File naming

### 1.2.1 Class files

Class names are written in [UpperCamelCase](https://en.wikipedia.org/wiki/Camel_case).

For classes that extend an Android component, the name of the class should end with the name of the component; for example: `SignInActivity`, `SignInFragment`, `ImageUploaderService`, `ChangePasswordDialog`.

### 1.2.2 Resources files
Resources file names are written in **lowercase_underscore**.

**1.2.2.1 Drawable files**

Naming conventions for drawables:

| Asset Type      | Prefix       | Example                  | Note                                                 |
|-----------------|--------------|--------------------------|------------------------------------------------------|
| Action bar      | `ab_`          | `ab_stacked.9.png`         |                                                      |
| Button          | `btn_`         | `btn_send_pressed.9.png`   |                                                      |
| Dialog          | `popup_`       | `popup_top.9.png`          | Designer prefer to use popup_ instead of dialog_     |
| Divider         | `divider_`     | `divider_horizontal.9.png` |                                                      |
| Icon            | `ic_`          | `ic_star.png`              |                                                      |
| Menu            | `menu_`        | `menu_submenu_bg.9.png`    |                                                      |
| Notification    | `noti_`        | `noti_bg.9.png`            | Designer prefer to use noti_ instead of notification |
| Tabs            | `tab_`         | `tab_pressed.9.png`        |                                                      |
| Place holder    | `placeholder_` | `placeholder_image.9.png`  |                                                      |
| Banner          | `banner_`      | `banner_reward.9.png`      |                                                      |
| Any other image | `img_`         | `img_nonservice.9.png`     |                                                      |
| black ground    | `bg_`          | `bg_nonservice.9.png`      |                                                      |
| button blackground    | `bg_btn_`          | `bg_btn_nonservice.9.png`      |                                                      |
| radio    | `radio_`          | `radio_choise.9.png`      |                                                      |
| Checkbox    | `checkbox_`          | `checkbox_choise.9.png`      |                                                      |


Naming conventions for icons (taken from [Android iconography guidelines](https://material.io/guidelines/style/icons.html)):


| Asset Type                      | Prefix         | Example                  | Note                                    |
|---------------------------------|----------------|--------------------------|-----------------------------------------|
| Icons                           | `ic_`            | `ic_star.png`              |                                         |
| Launcher icons                  | `ic_launcher_`   | `ic_launcher_calendar.png` |                                         |
| Menu icons and Action Bar icons | `ic_menu`        | `ic_menu_archive.png`      |                                         |
| Status bar icons                | `ic_stat_notify` | `ic_stat_notify_msg.png`   | Either ic_stat_notify_ or noti_ is fine. |
| Tab icons                       | `ic_tab`         | `ic_tab_recent.png`        |                                         |
| Dialog icons                    | `ic_popup`       | `ic_popup_info.png`        |                                         |

**Note:** for any icon inside button, we don't use `ic_btn_` anymore. Either `ic_` or `btn_` is fine (but depend on what it's functional). 

Naming conventions for **selector** states:

| State    | Suffix      | Example                    |
|----------|-------------|----------------------------|
| Normal   | `_normal`   | `btn_order_normal.9.png`   |
| Pressed  | `_pressed`  | `btn_order_pressed.9.png`  |
| Focused  | `_focused`  | `btn_order_focused.9.png`  |
| Disabled | `_disabled` | `btn_order_disabled.9.png` |
| Selected | `_selected` | `btn_order_selected.9.png` |


**1.2.2.2 Layout files**

Layout files should match the name of the Android components that they are intended for but moving the top level component name to the beginning. For example, if we are creating a layout for the `SignInActivity`, the name of the layout file should be `activity_sign_in.xml`.

| Component        | Class Name              | Layout Name                  |
|------------------|-------------------------|------------------------------|
| Activity         | `UserProfileActivity `  | `activity_user_profile.xml`  |
| Fragment         | `SignUpFragment `       | `fragment_sign_up.xml`       |
| Dialog           | `ChangePasswordDialog ` | `dialog_change_password.xml` |
| AdapterView item | ---                     | `item_person.xml`            |
| Partial layout   | ---                     | `partial_stats_bar.xml`      |


**1.2.2.3 Menu files**

Similar to layout files, menu files should match the name of the component. For example, if we are defining a menu file that is going to be used in the `UserActivity`, then the name of the file should be `activity_user.xml`

A good practice is to not include the word menu as part of the name because these files are already located in the `menu` directory.

1.2.2.4 Values files

Resource files in the values folder should be **plural**, e.g. `strings.xml`, `styles.xml`, `colors.xml`, `dimens.xml`, `attrs.xml`

# 2 Code guidelines
## 2.1 Java language rules
### 2.1.1 Don't ignore exceptions

You **must never do** the following:
```java
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
}
```
_While you may think that your code will never encounter this error condition or that it is not important to handle it, ignoring exceptions like above creates mines in your code for someone else to trip over some day. You must handle every Exception in your code in some principled way. The specific handling varies depending on the case. - ([Android code style guidelines](https://source.android.com/source/code-style))_

See alternatives [here](https://source.android.com/source/code-style#dont-ignore-exceptions).

### 2.1.2 Don't catch generic exception
You should not do this:

```java
try {
    someComplicatedIOFunction();        // may throw IOException
    someComplicatedParsingFunction();   // may throw ParsingException
    someComplicatedSecurityFunction();  // may throw SecurityException
    // phew, made it all the way
} catch (Exception e) {                 // I'll just catch all exceptions
    handleError();                      // with one generic handler!
}
```

### 2.1.3 Fully qualify imports
This is bad: `import foo.*;`

This is good: `import foo.Bar;`

See more info [here](https://source.android.com/source/code-style#fully-qualify-imports)

## 2.2 Java style rules
### 2.2.1 Fields definition and naming
Fields should be defined at the **top of the file** and they should follow the naming rules listed below.

Private, non-static field names start with **m**.
Private, static field names start with **_s_**.
Other fields start with a lower case letter.
Static final fields (constants) are **ALL_CAPS_WITH_UNDERSCORES**.

Example:
```java
public class MyClass {
    public static final int SOME_CONSTANT = 42;
    public int publicField;                     //no 'm' on public modifier
    private static MyClass sSingleton;
    int mPackagePrivate;
    private int mPrivate;
    protected int mProtected;
}
```

### 2.2.2 Treat acronyms as words

| Good             | Bad               |
|------------------|-------------------|
| `XmlHttpRequest` | `XMLHTTPRequest ` |
| `getCustomerId`  | `getCustomerID `  |
| `String url`     | `String URL `     |
| `long id`        | `long ID`         |

### 2.2.3 Use spaces for indentation
Use **4 space** indents for blocks:
```java
if (x == 1) {
    x++;
}
```

Use **8 space** indents for line wraps:
```java
Instrument i =
        someLongExpression(that, wouldNotFit, on, one, line);
```

Braces around the statements are required unless the condition and the body fit on one line.

If the condition and the body fit on one line and that line is shorter than the max line length, then braces are not required, e.g.
```java
if (condition) body();
```
This is **bad**:
```java
if (condition)
    body();  // bad!
```

### 2.2.6 Annotations
**2.2.6.1 Annotations practices**

According to the Android code style guide, the standard practices for some of the predefined annotations in Java are:
* **`@Override`**: The `@Override` annotation **must be used** whenever a method overrides the declaration or implementation from a super-class. For example, if you use the `@inheritdocs` Javadoc tag, and derive from a class (not an interface), you must also annotate that the method `@Overrides` the parent class's method.

* **`@SuppressWarnings`**: The `@SuppressWarnings` annotation should only be used under circumstances where it is impossible to eliminate a warning. If a warning passes this **"impossible to eliminate"** test, the `@SuppressWarnings` annotation must be used, so as to ensure that all warnings reflect actual problems in the code.

More information about annotation guidelines can be found [here](https://source.android.com/source/code-style#use-standard-java-annotations).

**2.2.6.2 Annotations style**

**Classes, Methods and Constructors**

When annotations are applied to a class, method, or constructor, they are listed after the documentation block and should appear as **one annotation per line**.

```java
/* This is the documentation block about the class */
@AnnotationA
@AnnotationB
public class MyAnnotatedClass { }
```

**Fields**

Annotations applying to fields should appear as **one annotation per line**
```java
@Nullable 
@Mock 
DataManager mDataManager;
```

### 2.2.7 Order import statements
The ordering of import statements is:

1. Android imports
2. Imports from third parties (com, junit, net, org)
3. java and javax
4. Same project imports

To exactly match the IDE settings, the imports should be:

* Alphabetically ordered within each grouping, with capital letters before lower case letters (e.g. Z before a).
* There should be a blank line between each major grouping (android, com, junit, net, org, java, javax).

More info [here](https://source.android.com/source/code-style#limit-variable-scope)

### 2.2.8 Logging guidelines
Use the logging methods provided by the `Log` class to print out error messages or other information that may be useful for developers to identify issues:

* `Log.v(String tag, String msg)` (verbose)
* `Log.d(String tag, String msg)` (debug)
* `Log.i(String tag, String msg)` (information)
* `Log.w(String tag, String msg)` (warning)
* `Log.e(String tag, String msg)` (error)

As a general rule, we **use the class name as tag** and we define it as a `static final` field at the top of the file. For example:

```java
public class MyClass {
    private static final String TAG = MyClass.class.getSimpleName();

    public myMethod() {
        Log.e(TAG, "My error message");
    }
}
```

VERBOSE and DEBUG logs must be disabled on release builds. It is also recommended to disable INFORMATION, WARNING and ERROR logs but you may want to keep them enabled if you think they may be useful to identify issues on release builds. If you decide to leave them enabled, you have to make sure that they are not leaking private information such as email addresses, user ids, etc.

To only show logs on debug builds:

```java
if (BuildConfig.DEBUG) Log.d(TAG, "The value of x is " + x);
```

### 2.2.9 Class member ordering

There is no single correct solution for this but using a logical and consistent order will improve code learnability and readability. It is recommendable to use the following order:

1. Constants
2. Fields
3. Constructors
4. Override methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes or interfaces
8. Example:

```java
public class MainActivity extends Activity {

	private String mTitle;
    private TextView mTextViewTitle;

    public void setTitle(String title) {
    	mTitle = title;
    }

    @Override
    public void onCreate() {
        ...
    }

    private void setUpView() {
        ...
    }

    static class AnInnerClass {

    }

}
```
If your class is extending an **Android component** such as an `Activity` or a `Fragment`, it is a good practice to **order the override methods so that they match the component's lifecycle**. For example, if you have an `Activity` that implements `onCreate()`, `onDestroy()`, `onPause()` and `onResume()`, then the correct order is:

```java
public class MainActivity extends Activity {

    //Order matches Activity lifecycle
    @Override
    public void onCreate() {}

    @Override
    public void onResume() {}

    @Override
    public void onPause() {}

    @Override
    public void onDestroy() {}

}
```
### 2.2.10 Parameter ordering in methods

When programming for Android, it is quite common to define methods that take a Context. If you are writing a method like this, then the **Context** must be the **first** parameter.

The opposite case are **callback** interfaces that should always be the **last** parameter.

Examples:
```java
// Context always goes first
public User loadUser(Context context, int userId);

// Callbacks always go last
public void loadUserAsync(Context context, int userId, UserCallback callback);
```
### 2.2.11 String constants, naming, and values

Many elements of the Android SDK such as `SharedPreferences`, `Bundle`, or `Intent` use a key-value pair approach so it's very likely that even for a small app you end up having to write a lot of String constants.

When using one of these components, you must define the keys as a `static final` fields and they should be prefixed as indicated below.

| Element            | Field Name Prefix |
|--------------------|-------------------|
| SharedPreferences  | `PREF_ `          |
| `Bundle `          | `BUNDLE_ `        |
| Fragment Arguments | `ARGUMENT_ `      |
| Intent Extra       | `EXTRA_ `         |
| Intent Action      | `ACTION_`         |

Example:
```java
// Note the value of the field is the same as the name to avoid duplication issues
static final String PREF_EMAIL = "PREF_EMAIL";
static final String BUNDLE_AGE = "BUNDLE_AGE";
static final String ARGUMENT_USER_ID = "ARGUMENT_USER_ID";

// Intent-related items use full package name as value
static final String EXTRA_SURNAME = "com.myapp.extras.EXTRA_SURNAME";
static final String ACTION_OPEN_USER = "com.myapp.action.ACTION_OPEN_USER";
```

### 2.2.12 Arguments in Fragments and Activities
When data is passed into an `Activity` or `Fragment` via an `Intent` or a `Bundle`, the keys for the different values **must** follow the rules described in the section above.

When an `Activity` or `Fragment` expects arguments, it should provide a `public static` method that facilitates the creation of the relevant `Intent` or `Fragment`.

In the case of Activities the method is usually called **`getStartIntent()`**:
```java
public static Intent getStartIntent(Context context, User user) {
	Intent intent = new Intent(context, ThisActivity.class);
	intent.putParcelableExtra(EXTRA_USER, user);
	return intent;
}
```
For `Fragments` it is named **`newInstance()`** and handles the creation of the `Fragment` with the right arguments:

```java
public static UserFragment newInstance(User user) {
	UserFragment fragment = new UserFragment;
	Bundle args = new Bundle();
	args.putParcelable(ARGUMENT_USER, user);
	fragment.setArguments(args)
	return fragment;
}
```

***Note 1:** These methods should go at the **top of the class** before `onCreate()`.

***Note 2:** If we provide the methods described above, the **keys** for extras and arguments **should be private** because there is not need for them to be exposed outside the class.

### 2.2.13 Line length limit
Code lines should not exceed **100 characters**. If the line is longer than this limit there are usually two options to reduce its length:

* Extract a local variable or method (preferable).
* Apply line-wrapping to divide a single line into multiple ones.

There are two exceptions where it is possible to have lines longer than 100:
* Lines that are not possible to split, e.g. long URLs in comments.
* `package` and `import` statements.

**2.2.13.1 Line-wrapping strategies**

There isn't an exact formula that explains how to line-wrap and quite often different solutions are valid. However there are a few rules that can be applied to common cases.

**Break at operators**

When the line is broken at an operator, the break comes **before the operator**. For example:
```java
int longName = anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne
        + theFinalOne;
```

**Assignment Operator Exception**

An **exception** to the break at operators rule is the assignment operator **`=`**, where the line break should happen after the operator.

```java
int longName =
        anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne + theFinalOne;
```

**Method chain case**
When multiple methods are chained in the same line - for example when using Builders - every call to a method should go in its own line, breaking the line before the **`.`**
```java
Picasso.with(context).load("http://ribot.co.uk/images/sexyjoe.jpg").into(imageView);
```

```java
Picasso.with(context)
        .load("http://ribot.co.uk/images/sexyjoe.jpg")
        .into(imageView);
```

**Long parameters case**
When a method has many parameters or its parameters are very long, we should break the line after every comma **`,`**
```java
loadPicture(context, "http://ribot.co.uk/images/sexyjoe.jpg", mImageViewProfilePicture, clickListener, "Title of the picture");
```

```java
loadPicture(context,
        "http://ribot.co.uk/images/sexyjoe.jpg",
        mImageViewProfilePicture,
        clickListener,
        "Title of the picture");
```

### 2.2.14 RxJava chains styling
Rx chains of operators require line-wrapping. Every operator must go in a new line and the line should be broken before the **`.`**

```java
public Observable<Location> syncLocations() {
    return mDatabaseHelper.getAllLocations()
            .concatMap(new Func1<Location, Observable<? extends Location>>() {
                @Override
                 public Observable<? extends Location> call(Location location) {
                     return mRetrofitService.getLocation(location.id);
                 }
            })
            .retry(new Func2<Integer, Throwable, Boolean>() {
                 @Override
                 public Boolean call(Integer numRetries, Throwable throwable) {
                     return throwable instanceof RetrofitError;
                 }
            });
}
```

## 2.3 Kotlin style rules
Almost of Kotlin guidelines are the same as Java guidelines **except** following:

### 2.3.1 Fields definition and naming
Fields should be defined at the top of the file and they should follow the naming rules listed below.

* Private, non-static field names **no need** to start with **`m`**.
* Private, static field names **no need** to start with **`s`**.
* Other fields start with a lower case letter.
* Static final fields (`const`) are ALL_CAPS_WITH_UNDERSCORES.

```Kotlin
open class MyClass {
    val SOME_CONSTANT_IN_CLASS = 42
    var publicField: Int = 0                //public by default
    private var myClass: MyClass? = null
    private val member: Int = 0
    internal val moduleLevel = 0
    protected var protectedMember: Int = 0

    companion object {
        const val SOME_CONSTANT = 42       
    }
}
```
### 2.3.2 Getters and Setters
In Kotlin we **don't need** to create getters and setters method for property. It already has syntax for declaring a property is

```kotlin
var <propertyName>[: <PropertyType>] [= <property_initializer>]
    [<getter>]
    [<setter>]
```
just treat it like a public property in Java:

```Kotlin
class ClassA {
    var data: List<String> = listOf()
}

class ClassB {
    ...
    fun assignValue() {
        val clzA = ClassA()
        clzA.data = listOf("A", "B", "C")
    }
}
```
### 2.3.3 Apply
We will use `apply` when you have to interact with that object more than 3 times. 

Example:
```Kotlin
recyclerView.apply {
    layoutManager = horizontalLlm
    setHasFixedSize(false)
    adapter = cateAdapter
}
```

## 2.4 XML style rules
### 2.3.1 Use self closing tags
When an XML element doesn't have any contents, you **must** use self closing tags.

This is good:
```xml
<TextView
	android:id="@+id/text_view_profile"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content" />
```
This is **bad**:
```kotlin
<!-- Don\'t do this! -->
<TextView
    android:id="@+id/text_view_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" >
</TextView>
```
### 2.3.2 Resources naming

**2.3.2.1 Resources ID naming in Java**

Resource IDs are written in [**camelCase**](https://en.wikipedia.org/wiki/Camel_case) with **underscore**. The IDs should generally start with the **feature's name**, followed by a **view's name** (that you want) and end with **view type** and all of this part must separate by **underscore**.

Template: **`featureName_viewName_viewType`**. 

| Element     | Example                           |
|-------------|-----------------------------------|
| `TextView`  | `register_wellcomeTitle_textView` |
| `ImageView` | `login_appLogo_imageView`         |
| `Button`    | `coupon_redeem_button`            |
| `Menu`      | `home_aboutUs_menu`               |

**2.3.2.2 Resources ID in Kotlin**

Resource IDs are written in [camelCase](https://en.wikipedia.org/wiki/Camel_case). The IDs should generally start with the **feature's name**, followed by a **view own name** and end with full name of the **view type**.

Template: **`featureNameViewNameViewType`**:

| Element     | Example                         |
|-------------|---------------------------------|
| `TextView`  | `registerWellcomeTitleTextView` |
| `ImageView` | `loginAppLogoImageView`         |
| `Button`    | `couponRedeemButton`            |
| `Menu`      | `homeAboutUsMenu`               |

**2.3.2.3 Strings**

String names start with a prefix that identifies the section they belong to. For example `registration_email_hint` or `registration_name_hint`. If a string **doesn't belong** to any section, then you should follow the rules below:

| Prefix     | Description                          |
|------------|--------------------------------------|
| `error_ `  | An error message                     |
| `msg_ `    | A regular information message        |
| `title_ `  | A title, i.e. a dialog title         |
| `action_ ` | An action such as "Save" or "Create" |

**2.3.2.4 Styles and Themes**

Unless the rest of resources, style names are written in **UpperCamelCase**.

### 2.3.3 Attributes ordering
1. View Id
2. Style
3. Layout width and layout height
4. Other layout attributes, sorted alphabetically
5. Remaining attributes, sorted alphabetically

## 2.4 Tests style rules
### 2.4.1 Unit tests
Test classes should match the name of the class the tests are targeting, followed by Test. For example, if we create a test class that contains tests for the `DatabaseHelper`, we should name it `DatabaseHelperTest`.

Test methods are annotated with `@Test` and should generally start with the name of the method that is being tested, followed by a precondition and/or expected behaviour and separate in each path with underscore.

* Template: `@Test void methodName_precondition_expectedBehaviour()`
* Example: `@Test void signIn_withEmptyEmail_fails()`

Precondition and/or expected behaviour may not always be required if the test is clear enough without them.

Sometimes a class may contain a large amount of methods, that at the same time require several tests for each method. In this case, it's recommendable to split up the test class into multiple ones. For example, if the DataManager contains a lot of methods we may want to divide it into DataManagerSignInTest, DataManagerLoadUsersTest, etc. Generally you will be able to see what tests belong together because they have common test fixtures.










