#### 1.使用技术栈 react

#### 2.组件库工具使用：dumi 和 storybook

#### 3.npx create-react-app r-ui --template typescript

#### 4.为 react 项目提供 storybook 能力

- npx storybook init
- yarn storybook 就可以本地启动 Storybook

#### 5.安装 Prettier 是一个代码格式化工具

- yarn add prettier -D
- 配置.prettierrc
- 修改 package.json 脚本 "prettier": "prettier src --write",

#### 6.配置 ESlint

ESLint 用于检测 JS 代码，发现代码质量问题并修复问题，还可以自己根据项目需要进行规则的自定义配置以及检查范围等等。

- yarn add eslint eslint-plugin-react eslint-plugin-simple-import-sort eslint-plugin-unused-imports @typescript-eslint/eslint-plugin @typescript-eslint/parser -D
- 配置 .eslintrc.js
- package.json 增加脚本 "eslint": "eslint src --fix",

#### 7.配置 lint-staged

lint-staged 相当于一个文件过滤器，每次提交时只检查本次提交的暂存区的文件，它不能格式化代码和校验文件，需要自己配置一下，如：.eslintrc、.stylelintrc 等，然后在 package.json 中引入。

- yarn add lint-staged -D
- 配置 .lintstagedrc
- 配置脚本 "ling-staged": "ling-staged",

#### 8.配置 husky

husky 工具可以定义拦截 git 钩子，对提交的文件和信息做校验和自动修复。

- yarn add husky -D
- 配置脚本 "prepare": "husky install",
- 执行 yarn prepare
- 会生成 .husky 文件，在内部配置文件 pre-commit 文件
- 在 git commit 之前，将会自动执行上面 pre-commit 脚本配置的命令。

#### 9.配置 commitlint

commitlint 是一个 git commit 信息校验工具。

- yarn add commitlint @commitlint/config-conventional -D
- 配置 .commitlintrc.js
- 在.husky 文件内部配置文件 commit-msg 文件
- git commit-msg 钩子函数触发时，将会自动执行 commit-msg 脚本配置的命令，校验 commit msg 是否符合规范

#### 10.开发公共组件

- src 下建公共组件文件

  - [component-name].tsx
  - [component-name].scss
  - index.ts
  - [component-name].stories.mdx

- 举例瀑布流插件

#### 11.组件库打包

比较热门的打包工具有 Webpack、rollup。
Webpack 对于代码分割和静态资源导入有着“先天优势”，并且支持热模块替换(HMR)，而 Rollup 并不支持，所以当项目需要用到以上，则可以考虑选择 Webpack。但是，Rollup 对于代码的 Tree-shaking 和 ES6 模块有着算法优势上的支持，若你项目只需要打包出一个简单的 bundle 包，并是基于 ES6 模块开发的，可以考虑使用 Rollup。
因此组件库打包工具选择 rollup。

- npm i rollup -g 全局安装 rollup 打包工具
- yarn add @rollup/plugin-commonjs @rollup/plugin-node-resolve @rollup/plugin-strip @rollup/plugin-typescript rollup-plugin-postcss rollup-plugin-node-externals autoprefixer -D
- 配置 rollup.config.js
- 新增文件 src/index.ts
- 配置打包脚本 "build-rollup": "rimraf es && rollup -c",
- 注意 rollup.config.mjs 的配置，有关使用 esm 导入，配置相应插件，后缀为 mjs, 以及 package.json 中 "module"，"types"等配置

#### 12.发布组件库到网站

- 安装 chromatic yarn add --dev chromatic
- 发布 Storybook 注意：确保 your-project-token 用您自己的项目令牌替换。
  - npx chromatic --project-token=<your-project-token>

#### 发布项目

项目发布成功后，如果有问题，可以通过 yarn link 进行调试，确认没问题后再发布版本。
link 的本质就是软链接，这样可以让我们快速使用本地正在开发的其它包。
假设组件库仓库为项目 A，使用组件库的仓库为项目 B。
在项目 A 下运行 yarn link，在项目 B 下运行 yarn link A，就可以实时调试项目 A 了
