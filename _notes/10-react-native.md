
创建一个为GitHub 仓库投票的应用

## Setup
Expo 是一个简化了React Native 应用的安装、开发、构建以及部署的平台
```
npm install --global expo-cli
```
init project
```
expo init rate-repository-app --template expo-template-blank@sdk-38
```

```
npm install --save-dev eslint babel-eslint eslint-plugin-react
```
create  .eslintrc 

add lint script
```
   "lint": "eslint ./src/**/*.{js,jsx} App.js --no-error-on-unmatched-pattern"
```

## React Native Debugger
https://github.com/jhen0409/react-native-debugger#installation

```
  $ brew update && brew cask install react-native-debugger
```


## Form
React 许多不错的库可以简化表单的状态管理。其中一个类库便是 Formik
Formik 的主要概念就是context上下文 和 field字段。
Formik的context 是由 Formik组件提供的，它包含了表单的状态。
状态包含了form 字段的一系列信息。这里的信息包括例如每个字段的值、验证错误信息等。
状态的字段可以通过参考他们的名字，使用useField hook 或者Field 组件。

```
npm install formik
```
Form validation
表单验证

Formik 提供两种方法来进行表单验证：验证函数或者验证schema。

验证函数是一个为Formik 组件提供validate 属性值的函数。 它接收表单的值作为入参，并返回一个包含field 对应错误信息的对象。

第二种方法是为Formik 组件提供验证schema，作为validationSchema 属性的值。这个验证schema 可以通过验证类库Yup 进行创建：

```
  npm install yup
```
