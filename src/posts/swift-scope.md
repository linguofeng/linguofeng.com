---
layout: layouts/post.njk
title: Swift Kotlin Scope Functions
date: 2019-08-30 16:39:49
---

Via: https://gist.github.com/kakajika/0bb3fd14f4afd5e5c2ec

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
