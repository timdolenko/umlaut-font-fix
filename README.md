# Umlaut doesn't work with custom font Xcode Swift Kotlin Android

<img width="372" alt="Screenshot 2023-05-08 at 13 54 59" src="https://user-images.githubusercontent.com/35912614/236817343-3e4027f7-c540-44bf-9a33-28c6ca678083.png">

For some reason your custom font freaks out and fails to display umlaut characters like ü, ä, ö.

### 2 Solutions:
1. In Swift, `text.precomposedStringWithCanonicalMapping` to replace all instances of this unfriendly combination with classical `\u{00FC}` represantation. 
2. Use tool like [glyphrstudio](https://www.glyphrstudio.com/online/) to manually add support for Combining Diaeresis `\u{0308}`.

If you can change the string, just re-type it manually with keyboard - it will fix the issue.

### Why this happens?
Your font doesn't contain [Combining Diaeresis][1] character. In failing case string instead of one ü character represented by one `\u{00FC}`, consists of actually 2 characters `u` and `\u{0308}` (Combining Diaeresis), which your font doesn't support.

#### References:
- https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters/#Extended-Grapheme-Clusters
- https://github.com/AliSoftware/OHAttributedLabel/issues/57 
- https://jongampark.wordpress.com/2008/07/21/unicode-normalization-and-nsstring/
- https://stackoverflow.com/questions/49255928/ios-custom-font-rendering-issues-with-umlaut-glyphs/76200772#76200772


  [1]: https://www.compart.com/en/unicode/U+0308
