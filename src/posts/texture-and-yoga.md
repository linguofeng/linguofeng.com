---
layout: layouts/post.njk
title: Texture And Yoga
date: 2019-09-02 10:05:53
---

- Podfile

```ruby
pod 'Texture', :subspecs => [..., 'Yoga']
```

```swift
import AsyncDisplayKit

class HelloViewController: ASViewController<SDisplayNode> {
  init() {
    super.init(node: ASDisplayNode.yogaHorizontalStack().apply {
      $0.style.alignItems = .center
      $0.style.padding = ASEdgeInsetsMake(UIEdgeInsets(top: 20, left: 20, bottom: 20, right: 20))
      $0.yogaChildren = [
        ASImageNode().apply {
          $0.image = UIImage(named: "avatar")
          $0.contentMode = .center
        },
        ASTextNode().apply {
          $0.attributedText = NSAttributedString(string: "name")
        },
      ]
    });
  }
}
```
