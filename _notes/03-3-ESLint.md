

```
  npm install eslint --save-dev
```

Init ESlint
```
  node_modules/.bin/eslint --init
```
The config will be save in .eslintrc.js


Run eslint
```
node_modules/.bin/eslint index.js
```
or use npm script
```
"scripts": {
    // ...
    "lint": "eslint ."
  },
```
创建一个 .eslintignore文件，使 ESlint 不检查整个 build 目录
```
  build
```




