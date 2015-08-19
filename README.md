# assemble

## Gruntfile.js

#### 一般的なやつ

```js:Gruntfile.js
    assemble: {
      site: {
        options: {
          layoutdir: 'dev/assemble-layouts', // 各ページのYFMで指定するレイアウトファイル（layout:）設置場所のパス
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

        },
        dest: 'assemble/', // 生成するファイルの保存先
        src: ['dev/*.hbs'] // ここで指定したファイルだけページ（html）が生成される
        // dest: 'assemble/',
        // src: ['src/pages/**/*.hbs']
      }
    },
```

#### 生成ファイルをjsonで指定（大量ファイル生成時とか）
  
```js:Gruntfile.js
    assemble: {
      site: {
      options: {
        layoutdir: 'src/layouts', // 各ページのYFMで指定するレイアウトファイル（layout:）設置場所のパス
        data: ['src/data/**/*.{json,yml}'], // 各hbsファイルから変数として呼び出すファイル群の指定
        partials: ['src/includes/**/*.hbs'], // 各hbsファイルから呼び出すテンプレートhtml（.hbs）ファイルを指定
        flatten: false, // true にすると、生成するファイル群からディレクトリパスを削除？？
        pages: grunt.file.readJSON('pages.json'), // 生成対象ページを json で指定。ディレクトリの指定ナシなので、Gruntfile.js と同階層
        expand: true // option の設定を有効にするかどうか。
      }
    },
```

```json:pages.json
{
  "en/s/trn/pf_hokkaido/index": { // ファイルの生成パス
    "metadata": { // YFM に定義しておくのと同義になる？？
      "h1": "Station Search [XXXXXXXX] - Restaurant Guide in Hokkaido",
      "canonical": "",
      "description": "Station Search [XXXXXXXX] - Restaurant Guide in Hokkaido.Restaurant search by Cuisines and Location, Station, Budget, Discount, Features. XXXXXXXX is All you need to plan travel and meal to Japan.",
      "keyword": "station,hokkaido,gourmet,restaurant,restaurant guide,japan restaurant guide,xxxxxxxx",
      "photo": "/img/sp/area/hokkaido.jpg",
      "prefcode": "01",
      "lang": "en",
      "layout": "list_trn.hbs"
    },
    "content": ""
  },
  "en/s/trn/pf_aomori/index": {
    "metadata": {
      "h1": "Station Search [XXXXXXXX] - Restaurant Guide in Aomori",
      "canonical": "",
      "description": "Station Search [XXXXXXXX] - Restaurant Guide in Aomori.Restaurant search by Cuisines and Location, Station, Budget, Discount, Features. XXXXXXXX is All you need to plan travel and meal to Japan.",
      "keyword": "station,aomori,gourmet,restaurant,restaurant guide,japan restaurant guide,xxxxxxxx",
      "photo": "",
      "prefcode": "02",
      "lang": "en",
      "layout": "list_trn.hbs"
    },
    "content": ""
  },
```

```hbs:list_trn.hbs
<!DOCTYPE HTML>
{{#is lang "en"}}<html lang="en" dir="ltr">{{/is}}
{{#is lang "zh-hans"}}<html lang="zh-hans" dir="ltr">{{/is}}
{{#is lang "zh-hant"}}<html lang="zh-hant" dir="ltr">{{/is}}
{{#is lang "ko"}}<html lang="ko" dir="ltr">{{/is}}
<head>
  <meta charset="utf-8" />
  <meta name="description" content="{{description }}" />
  <meta name="keywords" content="{{keyword }}" />
  <meta name="viewport" content="width=device-width,user-scalable=no,initial-scale=1,maximum-scale=1" />
  <meta name="format-detection" content="telephone=no" />
  <meta name="sc_page" content="sma" />
  <title>{{h1 }}</title>
  <link rel="stylesheet" href="/css/ensmp.css" />
  <link rel="stylesheet" href="/css/colorbox.css" />
</head>
<body id="iSearch" class="bg-warm">
<div>
{{> header }}
{{> body }}
  <div class="g-back">
    <a href="../"><span class="-icon-prev"></span>{{#is lang "en"}}Back{{/is}}{{#is lang "zh-hans"}}返回{{/is}}{{#is lang "zh-hant"}}返回{{/is}}{{#is lang "ko"}}이전{{/is}}</a>
  </div>
  <h1 class="h1 -std">
    {{h1 }}
  </h1>
  <ul class="buttons">
{{#is lang "en"}}
{{#is prefcode "01"}}{{#each trn}}{{#each en.pf_01}}<li><a href="{{url}}" class="button-r">{{name}}</a></li>{{/each}}{{/each}}{{/is}}
  </ul>
{{> footer }}
</div>
{{> scripts }}
</body>
</html>
```

#### ファイル生成ディレクトリをキー側に指定することもできる

```json:Gruntfile.js
    assemble: {
      site: {
      options: {
        layoutdir: 'src/layouts', // 各ページのyamlFMで指定するレイアウトファイル（layout:）設置場所のパス
        data: ['src/data/**/*.{json,yml}'], // 各hbsファイルから変数として呼び出すファイル群の指定
        partials: ['src/includes/**/*.hbs'], // 各hbsファイルから呼び出すテンプレートhtml（.hbs）ファイルを指定
        flatten: false, // true にすると、生成するファイル群からディレクトリパスを削除？？
        expand: true // option の設定を有効にするかどうか。
      },
      pages: {
        files: {
          'dev/': ['src/pages/**/*.hbs']
        }
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

## links

- [official helpers](http://assemble.io/helpers/helpers-collections.html)

