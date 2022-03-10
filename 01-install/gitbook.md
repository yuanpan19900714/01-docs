## windows系统gitbook安装

- 前提：[安装nodejs]()
- 验证前提：win+R快捷键输入cmd打开DOS窗口，输入以下命令验证
  - 验证nodejs
  ```
  C:\Users\Administrator>node --version
  v12.19.0
  ```
  - 验证npm
  ```
  C:\Users\Administrator>npm --version
  6.14.8
  ```
- 安装gitbook
```
C:\Users\Administrator>npm install -g gitbook

gitbook@2.6.9 
AppData\Local\Temp\tmp-16763iLw34wjVBqN\node_modules\gitbook
├── bash-color@0.0.3.6.9
├── gitbook-plugin-livereload@0.0.1
├── escape-string-regexp@1.0.3
├── nunjucks-filter@1.0.0
├── spawn-cmd@0.0.2
├── gitbook-plugin-sharing@1.0.1
├── gitbook-plugin-fontsettings@1.0.2
├── nunjucks-autoescape@1.0.0
├── jsonschema@1.0.2
├── github-slugid@1.0.0
├── q@1.0.1
├── json-schema-defaults@0.1.1
├── graceful-fs@3.0.5
├── urijs@1.17.0
├── crc@3.2.1
├── semver@5.0.1
├── tmp@0.0.24
├── dom-serializer@0.1.0 (domelementtype@1.1.3, entities@1.1.2)
├── resolve@0.6.3
├── npmi@0.1.1 (semver@4.3.6)
├── merge-defaults@0.2.1 (lodash@2.4.2)
├── send@0.2.0 (range-parser@1.0.3, fresh@0.2.4, mime@1.2.11, debug@3.2.7)
├── i18n@0.5.0 (sprintf@0.1.5, mustache@4.2.0, debug@3.2.7)
├── fs-extra@0.16.5 (jsonfile@2.4.0, rimraf@2.7.1)
├── request@2.51.0 (tunnel-agent@0.4.3, aws-sign2@0.5.0, forever-agent@0.5.2, stringstream@0.0.6, caseless@0.8.0, oauth-sign@0.5.0, json-stringify-safe@5.0.1, mime-types@1.0.2, qs@2.3.3, node-uuid@1.4.8, combined-stream@0.0.7, tough-cookie@4.0.0, http-signature@0.10.1, form-data@0.2.0, bl@0.9.5, hawk@1.1.1)
├── nunjucks@2.2.0 (asap@2.0.6, optimist@0.6.1)
├── tiny-lr@0.2.1 (parseurl@1.3.3, livereload-js@2.4.0, qs@5.1.0, debug@2.2.0, body-parser@1.14.2, faye-websocket@0.10.0)
├── gitbook-plugin-search@1.1.0 (lunr@0.5.12)
├── cheerio@0.19.0 (entities@1.1.2, css-select@1.0.0, htmlparser2@3.8.3)
├── chokidar@1.0.6 (path-is-absolute@1.0.1, is-glob@1.1.3, arrify@1.0.1, async-each@0.1.6, is-binary-path@1.0.1, glob-parent@1.3.0, readdirp@1.4.0, anymatch@1.3.2)
├── gitbook-parsers@0.8.9 (q@1.5.1, gitbook-restructuredtext@0.2.3, gitbook-markdown@0.5.3, gitbook-asciidoc@0.2.4)
├── fstream-ignore@1.0.2 (inherits@2.0.4, minimatch@2.0.10, fstream@1.0.12)
├── gitbook-plugin-highlight@1.0.3 (highlight.js@8.8.0)
├── lodash@3.10.1
├── juice@1.5.0 (commander@2.3.0, slick@1.12.1, batch@0.5.2, cssom@0.3.0, web-resource-inliner@1.1.4)
└── npm@2.4.1
```
- 使用：见[gitbook使用](../02-usage/gitbook.md)