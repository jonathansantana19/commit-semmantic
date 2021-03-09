# test-commit-semmantic
Projeto Testando boas práticas de commits semmantic e gerando change log automático



# Projeto NestJs typescript

Lib: https://www.conventionalcommits.org/en/v1.0.0/ <b>
Fonte: https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional <b>
Rules : https://commitlint.js.org/#/reference-rules?id=scope-case <b>
https://github.com/conventional-changelog/commitlint/blob/master/docs/reference-rules.md#scope-case <b>


# Instalação passo a passo 
https://remarkablemark.org/blog/2019/05/29/git-husky-commitlint/

# Types

feat : Para um novo arquivo. (A ferramenta não consegue diferenciar o conteúdo de um recurso / refatoração / correção de bug, mas assume que um novo arquivo provavelmente será um novo recurso) <b>
chore:  Para arquivos de configuração e para excluir, renomear ou mover um arquivo. <b>
ci: 	Para configurações em torno de Ações GH, CircleCI e BuildKite. <b>
test: Para diretórios e arquivos relacionados a testes, como tests/ou index.spec.js. <b>
docs : Para alterações na documentação, goste README.md, docs/ou CONTRIBUTING.md. <b>


# Install commitlint with a config:


```$ npm install @commitlint/{cli,config-conventional} ``` <b>
This command installs both @commitlint/cli and @commitlint/config-conventional.

<b><b><b>
config-conventional is a standard based on the Angular convention.

Create .commitlintrc.json, which extends the rules from config-conventional:
```
{
  "extends": ["@commitlint/config-conventional"]
}
Or export the rules in commitlint.config.js:

module.exports = {
  extends: ['@commitlint/config-conventional'],
};

```
Install husky:

```$ npm install husky ```
Enable Git hooks:

```$ npx husky install
Or add postinstall script to package.json to enable Git hooks after npm install:

{
  "private": true,
  "scripts": {
    "postinstall": "husky install"
  },
  "devDependencies": {
    "@commitlint/cli": "^11.0.0",
    "@commitlint/config-conventional": "^11.0.0",
    "husky": "^5.0.9"
  }
}
```
It’s assumed that the package is private. If the package is public, then make sure to disable postinstall script using pinst. See Husky docs for more information.

Add the commit-msg hook:

```$ npx husky add .husky/commit-msg 'npx commitlint --edit $1' ```
Make sure to use single quotes intead of double quotes so $1 is added correctly.

Test that the commit hook works.

Husky 4
Install commitlint with a config:

```
$ npm install @commitlint/{cli,config-conventional}
Create .commitlintrc.json, which extends the rules from config-conventional:

{
  "extends": ["@commitlint/config-conventional"]
}
Or export the rules in commitlint.config.js:

module.exports = {
  extends: ['@commitlint/config-conventional'],
};
Install husky@4, which sets up the Git hooks:

$ npm install husky@4
Create .huskyrc (or .huskyrc.json) and add the Git commit-msg hook that runs commitlint:

{
  "hooks": {
    "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
  }
}
Or add the hook to package.json:

{
  "devDependencies": {
    "@commitlint/cli": "latest",
    "@commitlint/config-conventional": "latest",
    "husky": "4"
  },
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  }
}
```
Test that the commit hook works.

# Test
```
Commit and verify the message follows Conventional Commits:
$ git commit -m 'add commitlint'       # fail
$ git commit -m 'feat: add commitlint' # success

```

# Change Log Automatic

Fonte:  https://www.mokkapps.de/blog/how-to-automatically-generate-a-helpful-changelog-from-your-git-commit-messages/
Lib: https://www.npmjs.com/package/standard-version 
Conf: https://github.com/conventional-changelog/conventional-changelog-config-spec/blob/master/versions/2.1.0/README.md


```
$ npm i --save-dev standard-version

```
 npm scripts in our package.json:
 ```
   "scripts": {
    "release": "standard-version",
    "release:minor": "standard-version --release-as minor",
    "release:patch": "standard-version --release-as patch",
    "release:major": "standard-version --release-as major"
  },
  ```

  .versionrc.json<br>

  ```
{
    "types": [
      {"type": "feat", "section": "Features"},
      {"type": "fix", "section": "Bug Fixes"},
      {"type": "chore", "hidden": true},
      {"type": "docs", "hidden": true},
      {"type": "style", "hidden": true},
      {"type": "refactor", "hidden": true},
      {"type": "perf", "hidden": true},
      {"type": "test", "hidden": true}
    ],
    "commitUrlFormat": "https://github.com/mokkapps/changelog-generator-demo/commits/{{hash}}",
    "compareUrlFormat": "https://github.com/mokkapps/changelog-generator-demo/compare/{{previousTag}}...{{currentTag}}"
  }
  ```

  The first release can be created by running npm run release -- --first-release in the terminal:
