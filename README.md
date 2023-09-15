# Create Next App Skeleton Package (Typescript)

---

## 프로젝트 생성 날짜 

2023/09/14

## 목적

create next app 프로젝트 진행 전 사용할 초기 세팅 프로젝트

## 패키지 업데이트
## Date: 2023 / 09 / 15

### Whats new

1. `.css` 작성시 typscript/lint 규칙에 포함되어서 발생되는 lint error 해결
2. `styled-components` lazy apply 해결을 위한 registry.tsx 파일 추가


---

## 세팅 목록

1. Typescript
2. eslint / prettier
3. 라이브러리


### package.json

```javascript
{
  "name": "next-skeleton-package",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "lint:fix": "eslint --fix './*.{ts,tsx,js,jsx}'",
    "prettier": "prettier --write --config ./.prettierrc.json './*.{ts,tsx}'",
    "postinstall": "husky install",
    "format": "prettier --cache --write .",
    "prepare": "husky install"
  },
  "dependencies": {
    "@types/node": "20.6.0",
    "@types/react": "18.2.21",
    "@types/react-dom": "18.2.7",
    "axios": "^1.5.0",
    "eslint": "^8.49.0",
    "eslint-config-next": "13.4.19",
    "next": "13.4.19",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "styled-components": "^6.0.8",
    "typescript": "5.2.2"
  },
  "devDependencies": {
    "@next/eslint-plugin-next": "^13.4.19",
    "@typescript-eslint/eslint-plugin": "^6.7.0",
    "@typescript-eslint/parser": "^6.7.0",
    "eslint-config-airbnb": "^19.0.4",
    "eslint-config-airbnb-typescript": "^17.1.0",
    "eslint-config-prettier": "^9.0.0",
    "eslint-plugin-import": "^2.28.1",
    "eslint-plugin-jsx-a11y": "^6.7.1",
    "eslint-plugin-prettier": "^5.0.0",
    "eslint-plugin-react": "^7.33.2",
    "eslint-plugin-react-hooks": "^4.6.0",
    "husky": "^8.0.3",
    "lint-staged": "^14.0.1",
    "prettier": "^3.0.3"
  },
  "lint-staged": {
    "*.{ts,tsx}": [
      "prettier --write",
      "eslint --fix"
    ]
  }
}
```

#### dependecies

- axios
- styled-components

#### devDependencies

- husky
- eslint
- prettier

---

### eslint, prettier

```javascript
// .eslintrc.json
{
  "env": {
    "browser": true,
    "es2021": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "next/core-web-vitals",
    "airbnb",
    "airbnb/hooks",
    "airbnb-typescript",
    "prettier"
  ],
  "overrides": [],
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module",
    "project": ["./tsconfig.json"]
  },
  "plugins": ["react", "@typescript-eslint"],
  "rules": {
    "react/react-in-jsx-scope": "off",
    "react/jsx-props-no-spreading": "off"
  }
}
```

```javascript
// .prettierrc.json
{
  "singleQuote": true,
  "parser": "typescript",
  "semi": true,
  "useTabs": false,
  "printWidth": 120,
  "tabWidth": 2
}
```

---

### husky

```shell
# pre-commit

#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

yarn run format
yarn lint-staged
```

```shell
# pre-push

#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

yarn run lint
```