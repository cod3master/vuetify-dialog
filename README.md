# vuetify-dialog (FORK)

### This module will help you work with `vuetify` dialogs without annoying templates

Implementation of [vuedl](https://github.com/yariksav/vuedl) dialog helper with Vuetify.js framework
## Vuedl module documentation

This module uses vuedl to automatically work with dialogs and DOM
[See docs here](https://github.com/yariksav/vuedl#readme)

## Setup

Install the package from npm

> IMPORTANT: After version 0.4.0 css and js were split and therefore you have to import css manually

## Vuetify 2

For Vuetify 2 please use the latest version of vuetify-dialog@2.X.X

### Demo with Vuetify 2
[Demo in CodeSandbox](https://iwdcf.csb.app/),  
[Demo source](https://codesandbox.io/s/vuetify-2-dialog-example-iwdcf)

```npm
npm install vuetify-dialog
```

```javascript
// need instance of vuetify, for example
import vuetify from '@/plugins/vuetify'

import VuetifyDialog from 'vuetify-dialog'
import 'vuetify-dialog/dist/vuetify-dialog.css'

Vue.use(VuetifyDialog, {
  context: {
    vuetify
  }
})
```



### Simple confirm dialog
```js
const res = await this.$dialog.confirm({
  text: 'Do you really want to exit?',
  title: 'Warning'
})
```

### Info dialog
```js
const res = await this.$dialog.info({
  text: 'File copied successfully',
  title: 'Info'
})
```

### Warning dialog
```js
const res = await this.$dialog.warning({
  text: 'Do you really want to exit?',
  title: 'Warning'
})
```

### Error dialog
```js
this.$dialog.error({
  text: 'Cannot delete this item',
  title: 'Error'
})
```

### Prompt dialog
```js
let res = await this.$dialog.prompt({
  text: 'Your name',
  title: 'Please input your name',
})
```

### Prompt dialog with password
```js
let res = await this.$dialog.prompt({
  title: 'Password balidation',
  text: 'Enter your password',
  rules: [(v) => v.length >= 6 || 'Password must be at least 6 characters long'], // vuetify's v-text-field rules prop
  textField: {
    // Any addtional props/attrs that will be binded to v-text-field component
    type: 'password',
  }
})
```

<!-- ![notification demo](https://media.giphy.com/media/w783JDQ6zdQmZl9hy5/giphy.gif) -->

### Programmatically close dialog

If property `waitForResult` set to false, then functions will return dialog instance

Actually waitForResult = true make two steps
1) dialogInstance = $dialog.show(component) // Show dialog
2) return dialogInstance.wait() // Return promise

Therefore to perform programmatically close dialog you have to set waitForResult to false and work with dialogInstance directly

```js
  const dialogInstance = await this.$dialog.warning({
    title: this.title,
    text: this.text,
    waitForResult: false
  });
  setTimeout(() => {
    dialogInstance.close()
  } , 3000)

  // then you can wait for user reaction
  const userChoice = await dialogInstance.wait()
  // after idle 3000 sec - userChoice will be undefigned
  this.$dialog.notify.info(userChoice)
```

### Notifications
The notification component is used to convey important information to the user. 
Notification support positioning, removal delay and callbacks. It comes in 4 variations, **success**, **info**, **warning** and **error**. These have default icons assigned which can be changed and represent different actions

<!-- ![notification demo](https://media.giphy.com/media/25DEAsF1eMtqTB1Js7/giphy.gif) -->

Notification uses [v-alert](https://vuetifyjs.com/en/components/alerts) component

Props:
* **text** - _the text fo your message_
  - type: String
* options:
  - type: Object
  - properties:
    - position: one of _top-left_, _top-right_, _bottom-left_, _bootom-right_
    - timeout: timer to hide message. Default 5000. If set to 0 - message will not closes automatically
    - actions
```js
this.$dialog.notify.info('Test notification', {
  position: 'top-right',
  timeout: 5000
})
```

### Toasts 
The toast component is used to display a quick message to a user. Toasts support positioning, removal delay and callbacks. It comes in 4 variations, **success**, **info**, **warning** and **error**. These have default icons assigned which can be changed and represent different actions

Toast uses [v-snackbar](https://vuetifyjs.com/en/components/snackbars) component

Props:
* **text** - _the text fo your message_
  - type: String
* options:
  - type: Object
  - properties:
    - position: one of _top-left_, _top-right_, _bottom-left_, _bootom-right_
    - timeout: timer to hide message. Default 5000. If set to 0 - message will not closes automatically 
    - actions: - see below
``` javascript
this.$dialog.message.info('Test', {
  position: 'top-left'
})
```
### Actions
To all dialogs you can put your own buttons
Props:
* **key** - _the text fo your message_
  - type: String
* options:
  - type: Object
  - properties:
    - position: one of _top-left_, _top-right_, _bottom-left_, _bootom-right_
    - timeout: timer to hide message. Default 5000. If set to 0 - message will not closes automatically 
    - actions: - see below
```js
{
  ...
  actions: {
    false: 'No',
    true: 'Yes'
  }
}
// result will be true, false, or undefined
{
  ...
  actions: ['No', 'Yes']
}
// result will be 'No', 'Yes', or undefigned

```
You can also send full button options
```js
{
  actions: [{
    text: 'Yes', color: 'blue', key: true
  }]
}
```


[npm-image]: https://img.shields.io/npm/v/vuetify-dialog.svg?style=flat-square
[npm-url]: https://npmjs.org/package/vuetify-dialog
