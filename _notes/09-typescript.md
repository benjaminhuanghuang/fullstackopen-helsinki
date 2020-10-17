ts-node能立即编译并执行指定的 TypeScript 文件，因此不需要单独的编译步骤。

```
npm install --save-dev ts-node typescript

npm install --save-dev @types/node
```
Run ts code
```
npm run ts-node -- file.ts
```


## ESLint
```
npm install --save-dev eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser
```

npm script
```
  "lint": "eslint --ext .ts ."
```