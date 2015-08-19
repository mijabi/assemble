# assemble

  ## Gruntfile.js

```js:Gruntfile.js
    assemble: {
      site: {
        options: {
          layoutdir: 'dev/assemble-layouts', // 各ページのyamlFMで指定するレイアウトファイル（layout:）設置場所のパス
          data: ['dev/assemble-datas/**/*.{json,yml}'], // 各hbsファイルから変数として呼び出すファイル群の指定
          partials: ['src/includes/**/*.hbs'], // 各hbsファイルから呼び出すテンプレートhtml（.hbs）ファイルを指定
          flatten: false, // true にすると、生成するファイル群からディレクトリパスを削除？？
          helpers: [
            'handlebars-helper-prettify'
          ],
          prettify: {
            condense: true,
            indent_char: '  ',
            indent: 1,
            unformatted: ['br']
          }

          // layoutdir: 'src/layouts',
          // data: ['src/data/**/*.{json,yml}'],
          // partials: ['src/includes/**/*.hbs'],
          // flatten: false,
          // helpers: [
          //   'handlebars-helper-prettify'
          // ],
          // prettify: {
          //   condense: true,
          //   indent_char: '  ',
          //   indent: 1,
          //   unformatted: ['br']
          // }

        },
        dest: 'assemble/', // 生成するファイルの保存先
        src: ['dev/*.hbs'] // ここで指定したファイルだけページ（html）が生成される
        // dest: 'assemble/',
        // src: ['src/pages/**/*.hbs']
      }
    },
```

  ## get Timestamp
    - [handlevars helpers > dates > now](https://github.com/assemble/handlebars-helpers/blob/master/docs/helpers/dates/helper-now.md)
    
    add timestamp as below.
    
    ```hbs

    ?nc={{ now "%y%m%d%H%M" }}

    // ?nc=1508071331

    ```


