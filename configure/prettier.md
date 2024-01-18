## How to - install Prettier

- Install prettier as a dev dependency

```
npm i -D prettier
```

## How to - use Prettier with ESLint

- Also install:
  - eslint-config-prettier
  - eslint-plugin-prettier

```
npm i -D eslint-config-prettier eslint-plugin-prettier
```

- Edit the eslint config to extend prettier

```ts
module.exports = {
  extends: ["prettier"],
};
```

## How to - configure Prettier

- Create a `.pretterrc` file in the project root dir.
- Other file types are supported - see prettier docs
- Add configurations in the form of a JSON object.

```json
{
  "printWidth": 80,
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true,
  "jsxSingleQuote": true,
  "trailingComma": "all",
  "bracketSpacing": true,
  "bracketSameLine": false,
  "arrowParens": "always",
  "overrides": [
    {
      "files": ["*.html"],
      "options": {
        "tabWidth": 4,
        "semi": false,
        "trailingComma": "none"
      }
    }
  ]
}
```
