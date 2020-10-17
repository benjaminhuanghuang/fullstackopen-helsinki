
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


