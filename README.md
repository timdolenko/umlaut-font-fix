# Umlaut doesn't work with custom font Xcode Swift Kotlin Android

<img width="372" alt="Screenshot 2023-05-08 at 13 54 59" src="https://user-images.githubusercontent.com/35912614/236817343-3e4027f7-c540-44bf-9a33-28c6ca678083.png">

For some reason your custom font freaks out and fails to display umlaut characters like ü, ä, ö.

The reason for this probably is that the string contains, in case of ü, 2 unicode scolars `u`, `\u{0308}` (Combining Diaeresis), instead of one `\u{00FC}`, and your custom font doesn't have Combining Diaeresis defined. 

Different representation of the ü:

| Char | Dec | Hex | Name |
| --- | ----------- | ----------- | ----------- |
| ü | 252 | FC | Latin Capital Letter U with Diaeresis |


### 2 Solutions:
1. In Swift, `text.precomposedStringWithCanonicalMapping` to replace all instances of this unfriendly combination with classical `\u{00FC}` represantation. 
2. Use tool like [glyphrstudio](https://www.glyphrstudio.com/online/) to manually add support for Combining Diaeresis `\u{0308}`.

#### References:
- https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters/#Extended-Grapheme-Clusters
- https://github.com/AliSoftware/OHAttributedLabel/issues/57 
- https://jongampark.wordpress.com/2008/07/21/unicode-normalization-and-nsstring/
