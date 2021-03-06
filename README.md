# Android App Template
![Kotlin](https://img.shields.io/badge/Language-Kotlin-orange.svg) ![Android](https://img.shields.io/badge/Platform-Android-green.svg) ![Reaktor](https://img.shields.io/badge/Architecture-Reaktor-red.svg)

This is an Android app template which can be used for new projects. A small example app is available [here](https://github.com/tailoredmedia/AndroidAppTemplateExample).

Check out [AndroidAppUtil](https://github.com/tailoredmedia/AndroidAppUtil) for several utility classes.

### Table of Contents
* [Technologies](#technologies)
* [Setup](#setup)
* [App structure](#app_structure)
* [Module/Package structure](#module_structure)
* [Testing](#testing)
* [Other](#other)
    * [Dependencies](#dependencies)
    * [ktlint](#ktlint)
    * [fastlane](#fastlane)
    * [Naming Conventions](#naming_conventions)
* [Recommended Reading](#recommended_reading)
* [License](#license)

## Technologies <a name="technologies"></a>
* Kotlin
* Android Architecture Component Navigation for navigation
* Koin for dependency injection (or Dagger2 if preferred)
* Retrofit/OkHttp/Gson for networking
* Reaktor (MVI) as architectural pattern
* (Room for local data storage)

## Setup <a name="setup"></a>
1. Create your **git** repository and check it out on your machine.
2. Add `git@github.com:tailoredmedia/AndroidAppTemplate.git` as remote and merge the latest commit into your repository (you most likely need to `--allow-unrelated-histories`).
3. Run the provided `setup.sh` script to rename files and properties according to project. Afterwards delete `setup.sh` from your repository.
4. Change `Readme.md` content to something appropriate.
5. Commit and Push to your **git** repository.

## App structure <a name="app_structure"></a>
Features should be contained in a separate module. The `core` module should contain shared code, for example *apis* or *databases* that are needed in multiple feature modules. The `app` module contains Android app related (*ui*) code. Depending on the project size 

* each feature could be contained in a separated module to support and promote reusability, such as for example a `login` module or a `map` module. Each module then contains all the necessary code for the module to **live** on its own. For example a `login` module could contain the login *api*, the token storage *database* and the *views* containing the login user interface.

* or all *ui* related elements are located in the `app` module in the according feature packages and the `core` module contains business logic that can potentially be shared with other feature or ui modules in future expansions of the application.

When adding a new module, create a library module and add `apply from: "$rootDir/library-module.gradle"` to the top of the newly created `build.gradle` file and afterwards your dependencies (see `core`'s `build.gradle` for example).

Remember however: app and module structure should be thought through separately for every project.

## Module/Package structure <a name="module_structure"></a>
* Model classes should be located in a `model` package.
* Network related classes and interfaces (e.g. networking api's) are located in a `remote` package.
* Local storage related classes (e.g. databases or dao's) are located in a `local` package.
* Classes that do not correspond to a certain feature, should either be located in an `all` package or on the top level of the module. For example: Utility classes should be located in a `util` package in the `all` package.

These rules can be applied to either whole *modules* or *packages* depending on if you have feature modules or feature packages. An example for such a module/package structure can be found [here](https://github.com/tailoredmedia/AndroidAppTemplateExample).

## Testing <a name="testing"></a>
* Every module should contain tests for its use cases.
* `test`: Write unit tests for every `Reactor`. Mockito or PowerMock can be used to mock objects and verify correct behaviour. Add the `RxSchedulersOverrideRule` to prevent errors with RxJava.
* `androidTest`: Write UI tests for common actions in your app. Use JUnit 4 Tests with Espresso. Some helper methods are available in EspressoUtils.

## Other <a name="other"></a>

### Dependencies <a name="dependencies"></a>

**All** dependencies should be located in a `dependencies.gradle`. To implement them in your module use `implementation deps.XXX`.

Checking whether project dependencies are ready to be updated use `./gradlew dependencyUpdates`. 

### ktlint <a name="ktlint"></a>
[ktlint](https://ktlint.github.io/) is a *Kotlin* linter and formatter. Using it is recommended to keep the code base clean and readable. Use 
* `./gradlew ktlint` to lint your code.
* `./gradlew ktlintFormat` to automatically format all your code according to the linting rules.

To conform to the rule of "**No wildcard imports**", go to *Preferences&rarr;Editor&rarr;Code Style&rarr;Kotlin&rarr;Imports* and enable **Use single name import**.

### fastlane <a name="fastlane"></a>
[fastlane](https://fastlane.tools/) is an automation framework that can be used to for deployment and release processes for Android or iOS apps. It is recommended to setup your Project with *fastlane*. 

### Naming Conventions <a name="naming_conventions"></a>
**Bold** rules should be applied. *Italic* rules are optional.

| Component        | Rule             | Example                   |
| ---------------- | ---------------------- | ----------------------------- |
| Layouts | **\<what\>**\_**\<where\>**.xml | `activity_main.xml`, `item_detail.xml` |
| Sub-Layouts | **\<what\>**\_**\<where\>**\_**\<description\>**.xml | `activity_main_appbar.xml` |
| Strings | **\<where\>**\_**\<what\>**\_**\<description\>** | `detail_tv_location` |
| Drawables | **\<what\>**\_**\<where\>**\_**\<description\>** | `btn_detail_background`, `card_overview_background` |
| Icons | ic_**\<description\>**\_**\<where\>**.xml | `ic_close.xml`, `ic_location_pin_detail.xml` |
| Dimensions | *\<where\>*\_**\<what\>**\_*\<description\>*\_*\<size\>* | `margin`, `detail_height_card`, `textsize_small` |
| Styles | **\<What\>**\.**\<Description\>** | `Text.Bold`, `Ratingbar.Preview` |
| Component Ids | **\<what\>\<Description\>** | `btnOpen`, `tvTitle` |


## Recommended Reading <a name="recommended_reading"></a>
* [Navigation Architecture Component](https://developer.android.com/topic/libraries/architecture/navigation/)
* [RxJava](http://www.vogella.com/tutorials/RxJava/article.html)
* [Reaktor](https://github.com/floschu/Reaktor)
* [Koin](https://insert-koin.io/)
* [Room](http://www.vogella.com/tutorials/AndroidSQLite/article.html)
* [Retrofit](http://www.vogella.com/tutorials/Retrofit/article.html)

## License <a name="license"></a>
```
Copyright 2019 Tailored Media GmbH.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
