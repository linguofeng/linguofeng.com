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

```swift
import Foundation

protocol ScopeFunc {}

extension ScopeFunc {
  @inline(__always) func apply(block: (Self) -> Void) -> Self {
    block(self)
    return self
  }

  @inline(__always) func `let`<R>(block: (Self) -> R) -> R {
    return block(self)
  }
}

extension NSObject: ScopeFunc {}

extension Optional where Wrapped: ScopeFunc {
  @inline(__always) func `let`<R>(block: (Wrapped) -> R) -> R? {
    guard let self = self else { return nil }
    return block(self)
  }
}

extension String: ScopeFunc {}
extension Int: ScopeFunc {}
```
