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

  val composeDialog = "<LATEST-VERSION>"
  
  // core module
  implementation("com.github.MFlisar.ComposeDialogs:core:$composeDialog")
  
   // ui modules
  implementation("com.github.MFlisar.ComposeDialogs:dialog-info:$composeDialog")
  implementation("com.github.MFlisar.ComposeDialogs:dialog-input:$composeDialog")
  implementation("com.github.MFlisar.ComposeDialogs:dialog-number:$composeDialog")
  implementation("com.github.MFlisar.ComposeDialogs:dialog-list:$composeDialog")
  implementation("com.github.MFlisar.ComposeDialogs:dialog-progress:$composeDialog")
  implementation("com.github.MFlisar.ComposeDialogs:dialog-time:$composeDialog")
  implementation("com.github.MFlisar.ComposeDialogs:dialog-date:$composeDialog")
  implementation("com.github.MFlisar.ComposeDialogs:dialog-color:$composeDialog")
}
```

The latest release can be found [here](https://github.com/MFlisar/ComposeDialogs/releases/latest)

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
        infoLabel: String = "",
        // Base Dialog -  Optional - all options can be set up with custom attributes, following are just the default examples
        title: (@Composable () -> Unit)? = null,
        icon: (@Composable () -> Unit)? = null,
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

Alternatively, if you want to use one dialog with many items (e.g. for list items) you can do following:

```kotlin
// create and remember a state with data (e.g. an Integer)
val state = rememberDialogState<Int>(data = null)

// show a dialog if necessary
if (state.showing)
{
    val data = state.requireData()
    DialogInfo(
        state = state,
        // Custom - Required
        info = "Data = $data"
    )
}

// a list that uses the dialog
val items = 1..100
LazyColumn {
    items.forEach {
        item(key = it) {
            Button(onClick = { state.show(it) }) {
                Text("Item $it")
            }
        }
    }
}
```

### Demo

A full demo is included inside the `demo` module, it shows nearly every usage with working examples.

### Screenshots

I only show the bottom sheet version for the info dialog, but of course any dialog does support the bottom sheet mode. Same holds true for the optional dialog icon.

**Info Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_info1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_info2.jpg?raw=true "Demo") | ![Demo](screenshots/demo_info3.jpg?raw=true "Demo") | ![Demo](screenshots/demo_info4.jpg?raw=true "Demo") |

**Input Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_input1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_input2.jpg?raw=true "Demo") | | |

**Number Dialog**

| | | | |
| :---: | :---: | :---: | :---: |
| ![Demo](screenshots/demo_number1.jpg?raw=true "Demo") | ![Demo](screenshots/demo_number2.jpg?raw=true "Demo") | ![Demo](screenshots/demo_number3.jpg?raw=true "Demo") | |

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

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/core/src/main/java/com/michaelflisar/composedialogs/core/DialogState.kt#L79-L85

In case of the complex state simply use `state.show(data)` to show the dialog and then inside your dialog call `val data = state.requireData()` to get the data from the state.

**CAUTION:** the state must be saveable by `Bundle`, if it is not, provide a custom `saver`!

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/core/src/main/java/com/michaelflisar/composedialogs/core/DialogState.kt#L104-110
  
### Existing dialogs

**Info Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/info/src/main/java/com/michaelflisar/composedialogs/dialogs/info/DialogInfo.kt#L19-32

**Input Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/input/src/main/java/com/michaelflisar/composedialogs/dialogs/input/DialogInput.kt#L63-91

**Number Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/number/src/main/java/com/michaelflisar/composedialogs/dialogs/input/DialogNumberPicker.kt#L43-66

**Date Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/date/src/main/java/com/michaelflisar/composedialogs/dialogs/datetime/DialogDate.kt#L64-78

**Time Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/time/src/main/java/com/michaelflisar/composedialogs/dialogs/datetime/DialogTime.kt#L29-42

**Color Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/color/src/main/java/com/michaelflisar/composedialogs/dialogs/color/DialogColor.kt#L107-126

**List Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/list/src/main/java/com/michaelflisar/composedialogs/dialogs/list/DialogList.kt#L59-77

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/list/src/main/java/com/michaelflisar/composedialogs/dialogs/list/DialogList.kt#L116-140

**Progress Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/modules/progress/src/main/java/com/michaelflisar/composedialogs/dialogs/progress/DialogProgress.kt#L28-42

**Custom Dialog**

https://github.com/MFlisar/ComposeDialogs/blob/07d81a25ab1803e2ca6b3447116a1f0639357ab0/library/core/src/main/java/com/michaelflisar/composedialogs/core/Dialog.kt#L43-53

```kotlin
Dialog(state, title, icon, style, buttons, options, onEvent = onEvent) {
    Text("Text in custom dialog")
    // ...
}
```