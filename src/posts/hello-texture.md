---
layout: layouts/post.njk
title: Hello Texture
date: 2019-08-30 16:11:41
---

```swift
import AsyncDisplayKit

class HelloViewController: ASViewController<SDisplayNode> {
  init() {
    super.init(node: ASDisplayNode().apply {
      $0.automaticallyManagesSubnodes = true
      let children = [
        ASImageNode().apply {
          $0.image = UIImage(named: "avatar")
          $0.contentMode = .center
        },
        ASTextNode().apply {
          $0.attributedText = NSAttributedString(string: "name")
        },
      ]
      $0.layoutSpecBlock = {
        ASStackLayoutSpec.vertical().apply {
          $0.alignItems = .center
          $0.spacing = 5
          $0.children = children
        }
      }
    });
  }
}

```
