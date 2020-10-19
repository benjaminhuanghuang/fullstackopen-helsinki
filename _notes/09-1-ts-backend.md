## Init TypeScript project
ts-node能立即编译并执行指定的 TypeScript 文件，因此不需要单独的编译步骤。

```
npm init 

npm install --save-dev ts-node typescript

npm install --save-dev @types/node
```

Run ts code
```
npm run ts-node -- file.ts
```

ts-node 有一个nodemon替代方法叫做**ts-node-dev**, 每个更改进行重新编译，不需要重新启动应用
```
npm install --save-dev ts-node-dev
```

ts-node-dev 相应的npm script
```
{
  "scripts": {
      "dev": "ts-node-dev index.ts",
  },
}
```

## ESLint
```
npm install --save-dev eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser
```

npm script for ESLint
```
  "lint": "eslint --ext .ts ."
```

## tsconfig.json
```
{
  "compilerOptions": {
    "target": "ES2020",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "esModuleInterop": true
  }
}
```
noImplicitAny : 所有使用的变量都必须有类型

将 eslint 配置为 disallow explicit any， 将如下规则写入 .eslintrc
```
{
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 11,
    "sourceType": "module"
  },
  "plugins": ["@typescript-eslint"],
  "rules": {
    "@typescript-eslint/no-explicit-any": 2
  }
}
```

设置一个lint npm 脚本，用来检查.ts扩展文件，通过如下修改package.json 文件:

{
  "scripts": {
      "start": "ts-node index.ts",
      "dev": "ts-node-dev index.ts",
      "lint": "eslint --ext .ts ."
  },
}