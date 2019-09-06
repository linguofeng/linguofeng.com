---
layout: layouts/post.njk
title: Flutter SingleChildScrollView 嵌套 WebView 滚动
date: 2019-09-06 10:36:27
tags:
  - flutter
---

在 Flutter 中会遇到需要 WebView 展示 html 页面，如果整个页面都是 html 的会比较简单，只需要

```dart
Scaffold(
  body: WebView(
    initialUrl: 'https://linguofeng.com',
  ),
);
```

在 `body` 中挂载 `WebView` 组件即可，但如果需要嵌套 `WebView` 局部展示 html 那就不太好处理，需要计算出 `WebView` 的滚动高度，如下:

```dart
Scaffold(
  body: SingleChildScrollView(
    child: Column(children: <Widget>[
      Text('h'),
      Text('e'),
      Text('l'),
      Text('l'),
      Text('o'),
      Container(
        height: _webViewHeight ?? 1000,
        child: WebView(
          initialUrl: 'https://linguofeng.com',
          javascriptMode: JavascriptMode.unrestricted,
          onWebViewCreated: (controller) {
            setState(() {
              _controller = controller;
            });
          },
          onPageFinished: (url) async {
            // 获取滚动高度
            final scrollHeight = await _controller?.evaluateJavascript(
              '(() => document.body.scrollHeight)();',
            );
            if (scrollHeight != null) {
              setState(() {
                _webViewHeight = double.parse(scrollHeight);
              });
            }
          },
        ),
      ),
      Text('w'),
      Text('o'),
      Text('r'),
      Text('l'),
      Text('d'),
    ],
  ),
);
```
