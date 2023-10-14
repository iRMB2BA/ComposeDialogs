### About

[![Release](https://jitpack.io/v/MFlisar/ComposeDialogs.svg)](https://jitpack.io/#MFlisar/ComposeDialogs)
![License](https://img.shields.io/github/license/MFlisar/ComposeDialogs)

This library offers you an easily extendible compose framework for modal dialogs and allows to show them as a **dialog** or a **bottom sheet**.

Made for **Compose M3**.

### Dependencies

| Dependency |        Version |
|:-------------------------------------------------------------------- |---------------:|
| [Compose BOM](https://developer.android.com/jetpack/compose/bom/bom) |   `2023.10.00` |
| Material3 | `1.1.2` |

Compose Mappings for BOM file: [Mapping](https://developer.android.com/jetpack/compose/bom/bom-mapping)

### Gradle (via [JitPack.io](https://jitpack.io/))

1. add jitpack to your project's `build.gradle`:
```groovy
repositories {
    maven { url "https://jitpack.io" }
}
```

2. add the compile statement to your module's `build.gradle`:
```groovy
dependencies {

  // core module
  implementation "com.github.MFlisar:ComposeDialogs:core:<LATEST-VERSION>"
  
  // ui modules
  implementation "com.github.MFlisar:ComposeDialogs:dialog-info:<LATEST-VERSION>"
  implementation "com.github.MFlisar:ComposeDialogs:dialog-input:<LATEST-VERSION>"
  implementation "com.github.MFlisar:ComposeDialogs:dialog-list:<LATEST-VERSION>"
  implementation "com.github.MFlisar:ComposeDialogs:dialog-progress:<LATEST-VERSION>"
  implementation "com.github.MFlisar:ComposeDialogs:dialog-time:<LATEST-VERSION>"
  implementation "com.github.MFlisar:ComposeDialogs:dialog-date:<LATEST-VERSION>"
  implementation "com.github.MFlisar:ComposeDialogs:dialog-color:<LATEST-VERSION>"
}
```

### Example

It works as simple as following:

```kotlin

// create and remember a state
val state = rememberDialogState()

// show a dialog if necessary
if (state.showing)
{
    DialogInfo(
        state = state,
        // Custom - Required
        info: String,
        // Custom - Optional
        infoTitle: String = "",
        // Base Dialog -  Optional - all options can be set up with custom attributes, following are just the default examples
        title: String = "",
        titleStyle: DialogTitleStyle = DialogDefaults.titleStyle(), // or DialogDefaults.titleStyleSmall() => both have a few settings...
        icon: DialogIcon? = null, // use DialogIcon.Painter(...) or DialogIcon.Vector(...) to add an icon
        style: DialogStyle = DialogDefaults.styleDialog(), // DialogDefaults.styleBottomSheet() => both have a few settings...
        buttons: DialogButtons = DialogDefaults.buttons(),
        options: Options = Options(),
        onEvent: (event: DialogEvent) -> Unit = {
            // optional event handler for all dialog events
        }
    )
}

// show the dialog inside a button press event or similar
Button(onClick = { state.show() }) {
    Text("Show Dialog")
}
```

### Demo

A full demo is included inside the `demo` module, it shows nearly every usage with working examples.

### Screenshots

I only show the bottom sheet version for the info dialog, but of course any dialog does support the bottom sheet mode.

**Info Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_info1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_info2.jpg?raw=true "Demo") | ![Demo](screenshots/demo_info3.jpg?raw=true "Demo") | ![Demo](screenshots/demo_info4.jpg?raw=true "Demo") |

**Input Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_input1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_input2.jpg?raw=true "Demo") | | |

**Date Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_calendar1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_calendar2.jpg?raw=true "Demo") | ![Demo](screenshots/demo_calendar3.jpg?raw=true "Demo") | |

**Time Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_time1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_time2.jpg?raw=true "Demo") | |  |

**Color Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_color1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_color2.jpg?raw=true "Demo") | ![Demo](screenshots/demo_color3.jpg?raw=true "Demo") | ![Demo](screenshots/demo_color4.jpg?raw=true "Demo") |

**List Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_list1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_list2.jpg?raw=true "Demo") | ![Demo](screenshots/demo_list3.jpg?raw=true "Demo") | ![Demo](screenshots/demo_list4.jpg?raw=true "Demo") |
| ![Demo](screenshots/demo_list5.jpg?raw=true "Demo") | ![Demo](screenshots/demo_list6.jpg?raw=true "Demo") | ![Demo](screenshots/demo_list7.jpg?raw=true "Demo") | |

**Progress Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_progress1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_progress2.jpg?raw=true "Demo") | |  |


### Settings and advanced usage

Check out the dialog state and the dialogs to find out what settings you can use and especially the demo app for a working example.

**Dialog State (simple with a boolean flag or complex with a data object)**

In case of the simple state `true` means that the dialog is visible and `false` that it's not. In case of the complex state holding an object means the dialog is visible and `null` means it's not visible.

https://github.com/MFlisar/ComposeDialogs/blob/7dcafb6f5731bcdd9f744f538988cd3d567bafc6/library/core/src/main/java/com/michaelflisar/composedialogs/core/DialogState.kt#L77-L83

In case of the complex state simply use `state.show(data)` to show the dialog and then inside your dialog call `val data = state.requireData()` to get the data from the state. I provide an overload for all supported data types (types that are supported by `Bundle`). For all other cases you must provide a custom saver.

https://github.com/MFlisar/ComposeDialogs/blob/7dcafb6f5731bcdd9f744f538988cd3d567bafc6/library/core/src/main/java/com/michaelflisar/composedialogs/core/DialogState.kt#L131-L138

https://github.com/MFlisar/ComposeDialogs/blob/7dcafb6f5731bcdd9f744f538988cd3d567bafc6/library/core/src/main/java/com/michaelflisar/composedialogs/core/DialogState.kt#L39-L47
  
### Existing dialogs

**Info Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/7e36c2d5143282ffc641390e9438905f5c04db8c/library/modules/info/src/main/java/com/michaelflisar/composedialogs/dialogs/info/DialogInfo.kt#L10-L24

**Input Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/7e36c2d5143282ffc641390e9438905f5c04db8c/library/modules/input/src/main/java/com/michaelflisar/composedialogs/dialogs/info/DialogInput.kt#L43-L72

**Date Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/7e36c2d5143282ffc641390e9438905f5c04db8c/library/modules/date/src/main/java/com/michaelflisar/composedialogs/dialogs/datetime/DialogDate.kt#L56-L71

**Time Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/7e36c2d5143282ffc641390e9438905f5c04db8c/library/modules/time/src/main/java/com/michaelflisar/composedialogs/dialogs/datetime/DialogTime.kt#L19-L33

**Color Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/7e36c2d5143282ffc641390e9438905f5c04db8c/library/modules/color/src/main/java/com/michaelflisar/composedialogs/dialogs/color/DialogColor.kt#L60-L80

**List Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/7e36c2d5143282ffc641390e9438905f5c04db8c/library/modules/list/src/main/java/com/michaelflisar/composedialogs/dialogs/list/DialogList.kt#L45-L64

https://github.com/MFlisar/ComposeDialogs/blob/7e36c2d5143282ffc641390e9438905f5c04db8c/library/modules/list/src/main/java/com/michaelflisar/composedialogs/dialogs/list/DialogList.kt#L85-L109

**Progress Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/7e36c2d5143282ffc641390e9438905f5c04db8c/library/modules/progress/src/main/java/com/michaelflisar/composedialogs/dialogs/progress/DialogProgress.kt#L19-L34

**Custom Dialog**

```kotlin
Dialog(state, title, titleStyle, icon, style, buttons, options, onEvent = onEvent) {
	Text("Text in custom dialog")
	// ...
}
```