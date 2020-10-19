## Create React App with TypeScript
```
  npx create-react-app my-app --template typescript
```

## tsconfig.json 
allowJs 被设置为true。 如果你需要混合使用TypeScript和 JavaScript (例如，如果你正在将一个 JavaScript 项目转换成TypeScript或者其他原因) ，那么这样做是可以的，但是我们希望我们的应用是纯粹的TypeScript，所以让我们把这个设置改为false。


## ESlint
create-react-app 已经安装ESLint依赖项


 .eslintrc
```
  {
    "env": {
      "browser": true,
      "es6": true,
      "jest": true
    },
    "extends": [
      "eslint:recommended",
      "plugin:react/recommended",
      "plugin:@typescript-eslint/recommended"
    ],
    "plugins": ["react", "@typescript-eslint"],
    "settings": {
      "react": {
        "pragma": "React",
        "version": "detect"
      }
    },
    "rules": {
      "@typescript-eslint/explicit-function-return-type": 0
    }
  }
``` 
因为基本上所有 React 组件都返回一个JSX.Element 类型或null 类型，
所以我们通过禁用 规则 explicit-function-return-type来稍微放松默认的lint规则，这样就不需要在所有地方显式写出函数返回类型 。


eslint 对应的 npm script
```
"lint": "eslint './src/**/*.{ts,tsx}'"
```

## Type
TypeScript 不再需要prop-types 包来定义 prop 类型，
可以通过使用 FunctionComponent 类型或者更短的别名 FC，在 TypeScript 本身的帮助下定义类型

需要在.eslintrc中禁用prop-types:
```
{
  // ...
  "rules": {
    "react/prop-types": 0,
  },  
  // ...
}
```