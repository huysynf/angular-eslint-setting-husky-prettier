# install-lint-angular
# Create file
```bash 
touch .prettierrc
ng add @angular-eslint/schematics
npm install --save-dev  @typescript-eslint/parser  eslint-config-prettier   eslint-plugin-prettier@latest
touch .eslintignore
touch .editorconfig
touch .eslintrc.json
```

## config .editorconfig

```text
root = true

[*]
charset = utf-8
indent_style = space
indent_size = 4 # this is the only change I made, to be aligned with prettier
insert_final_newline = true
trim_trailing_whitespace = true

[*.ts]
quote_type = single

[*.md]
max_line_length = off
trim_trailing_whitespace = false
```
## config .prettierrc


```text
{
    "trailingComma": "es5",
    "printWidth": 80,
    "singleQuote": true,
    "useTabs": false,
    "tabWidth": 4,
    "semi": true,
    "bracketSpacing": true
}

```
## config .eslintignore

```text
package.json
package-lock.json
dist
e2e/**
karma.conf.js
commitlint.config.js

```

##  Update the scripts in the package.json

```bash 
"test": "ng test --watch=false --browsers ChromeHeadless",
"lint": "npx eslint \"src/**/*.{js,jsx,ts,tsx,html}\" --quiet --fix",
"format": "npx prettier \"src/**/*.{js,jsx,ts,tsx,html,css,scss}\" --write"

```

## config eslintrc.json

```json
{
    "root": true,
    "ignorePatterns": [
        "projects/**/*"
    ],
    "overrides": [
        {
            "files": [
                "*.ts"
            ],
            "parserOptions": {
                "project": [
                    "tsconfig.json"
                ],
                "createDefaultProgram": true
            },
            "extends": [
                "plugin:@angular-eslint/recommended",
                "plugin:@angular-eslint/template/process-inline-templates",
                "plugin:prettier/recommended"
            ],
            "rules": {
                "@angular-eslint/directive-selector": [
                    "error",
                    {
                        "type": "attribute",
                        "prefix": "app",
                        "style": "camelCase"
                    }
                ],
                "@angular-eslint/component-selector": [
                    "error",
                    {
                        "type": "element",
                        "prefix": "app",
                        "style": "kebab-case"
                    }
                ],
                "no-empty-function": "off",
                "@typescript-eslint/no-empty-function": "off",
                "@angular-eslint/no-empty-lifecycle-method": "off"
            }
        },
        {
            "files": ["*.html"],
            "extends": ["plugin:@angular-eslint/template/recommended"],
            "rules": {}
        },
        {
            "files": [
                "*.component.html"
            ],
            "extends": [
                "plugin:@angular-eslint/template/recommended",
                "plugin:prettier/recommended"
            ],
            "rules": {}
        }
    ]
}


```

## install husky

```bash 

# use npm 

 npx husky-init && npm

 # use yarn

  npx husky-init && yarn 
```
# edit .husky/pre-commit

```bash 
npx  lint-staged
```

## update pakage.json add 

```bash 
 "lint-staged": {
        "*.{ts,tsx}": [
            "npm run lint"
        ],
        "*.{ts,tsx, css,scss}": [
            "npm run format"
        ]
    }

```

