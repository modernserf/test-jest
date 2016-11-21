# Problem

- create-react-app wants to support using `src/node_modules` for internal packages. This is kind of hacky, but is the least bad of available solutions for [the reasons enumerated here](https://github.com/facebookincubator/create-react-app/issues/1065).
- Jest sensibly ignores tests in node_modules by default, but even when those defaults are overridden, it _still_ ignores those tests.

This is the jest configuration in package.json:

```json
{
  "moduleFileExtensions": [
    "jsx",
    "js",
    "json"
  ],
  "moduleNameMapper": {
    "^.+\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": "<rootDir>/config/jest/FileStub.js",
    "^.+\\.css$": "<rootDir>/config/jest/CSSStub.js"
  },
  "setupFiles": [
    "<rootDir>/config/polyfills.js"
  ],
  "testPathIgnorePatterns": [
    "<rootDir>/(build|config|node_modules)/"
  ],
  "preprocessorIgnorePatterns": [
      "<rootDir>/node_modules"
  ],
  "testEnvironment": "node"
}
```

This should ignore `<rootDir>/node_modules`, but _not_ `<rootDir>/src/node_modules`. In fact, even if you set `testPathIgnorePatterns` to just `["<rootDir>/(build)/"]`, it still ignores tests in all `node_modules` directories.

---

This project was bootstrapped with [Create React App](https://github.com/facebookincubator/create-react-app).
