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

| Asset Type  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |



