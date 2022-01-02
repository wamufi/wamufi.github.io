---
layout: post
title: "YouTube ID 가져오기"
date: "2020-11-27 14:39:00 +0900"
tags: [iOS, Swift, String]
---
동영상 id로 주로 돌리는 것 같아 가져와서 처리.

```swift
public extension String {
    var youtubeID: String {
        let pattern = "((?<=(v|V)/)|(?<=be/)|(?<=(\\?|\\&)v=)|(?<=embed/))([\\w-]++)"

        let regex = try? NSRegularExpression(pattern: pattern, options: .caseInsensitive)
        let range = NSRange(location: 0, length: count)

        guard let result = regex?.firstMatch(in: self, range: range) else {
            return self
        }

        return (self as NSString).substring(with: result.range)
    }
}
```

```swift
let id = "https://www.youtube.com/watch?v=MO7Ta0DvEWA".youtubeID
```
결과값은 `MO7Ta0DvEWA`

