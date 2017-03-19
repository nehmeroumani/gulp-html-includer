# gulp-tag-include-html
is a gulp plugin,used to include html.

## feature
    Using the <include> tag that include the HTML fragment in other files;
    Using the doT.js template engine, rendering include content;
    Using the tag attributes and child elements, two ways to transfer data;
    doT.js document：http://olado.github.io/doT/

    在html中使用<include>标签，包含其他文件中的html片段；
    使用doT.js模板引擎，渲染被包含的内容；
    使用标签属性和子元素，两种方式传递数据；
    doT.js模板引擎文档：http://olado.github.io/doT/
    (英文不好，以上特性描述如果有误，欢迎指正：50793247@qq.com)

## install
```bash
npm install gulp-tag-include
```

## example

gulpfile.js
```js
var gulp = require('gulp');
var include = require('gulp-tag-include-html');
gulp.task('default', function() {
    gulp.src('./views/index.html')
      .pipe(include())
      .pipe(gulp.dest('dest'));
});
```

/views/index.html
```html
<include src="./partials/head.html" title="home">
  <link rel="stylesheet" href="1.css">
  <link rel="stylesheet" href="2.css">
</include>
<div><h1>this is body</h1></div>
<include src="./partials/footer.html" js="['1.js','2.js']" />
```

/views/partials/head.html
```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>{{=it.title}}</title>
  {{=it.children}}
</head>
<body>
```

/views/partials/footer.html
```html
<h2>this is footer</h2>
{{~it.js:item:index}}
  <script src="{{=item}}"></script>
{{~}}
</body>
</html>
```

result:
/dest/index.html
```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>home</title>
  <link rel="stylesheet" href="1.css">
  <link rel="stylesheet" href="2.css">
</head>
<body>
<div><h1>this is body</h1></div>
<h2>this is footer</h2>

  <script src="1.js"></script>

  <script src="2.js"></script>

</body>
</html>
```

## Author
nickham-su
Email:50793247@qq.com

Thank you
