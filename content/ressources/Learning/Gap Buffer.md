---
title: Gap Buffer
draft: false
publish: true
tags:
  - data-structures
date: 2024-09-02
---
- A **gap buffer** in [computer science](https://en.wikipedia.org/wiki/Computer_science) is a [dynamic array](https://en.wikipedia.org/wiki/Dynamic_array) that allows efficient insertion and deletion operations clustered near the same location. Gap buffers are especially common in [text editors](https://en.wikipedia.org/wiki/Text_editor), where most changes to the text occur at or near the current location of the [cursor](https://en.wikipedia.org/wiki/Cursor_(computers)). The text is stored in a large buffer in two contiguous segments, with a gap between them for inserting new text. Moving the cursor involves copying text from one side of the gap to the other (sometimes copying is delayed until the next operation that changes the text). Insertion adds new text at the end of the first segment; deletion deletes it.
- Text in a gap buffer is represented as two [strings](https://en.wikipedia.org/wiki/String_(computer_science)), which take very little extra space and which can be searched and displayed very quickly, compared to more sophisticated [data structures](https://en.wikipedia.org/wiki/Data_structure) such as [linked lists](https://en.wikipedia.org/wiki/Linked_list). However, operations at different locations in the text and ones that fill the gap (requiring a new gap to be created) may require copying most of the text, which is especially inefficient for large files. The use of gap buffers is based on the assumption that such recopying occurs rarely enough that its cost can be [amortized](https://en.wikipedia.org/wiki/Amortized_analysis) over the more common cheap operations. This makes the gap buffer a simpler alternative to the [rope](https://en.wikipedia.org/wiki/Rope_(data_structure)) for use in text editors[[1]](https://en.wikipedia.org/wiki/Gap_buffer#cite_note-chucarroll-1) such as [Emacs](https://en.wikipedia.org/wiki/Emacs).[[2]](https://en.wikipedia.org/wiki/Gap_buffer#cite_note-elisp-2)
- [Wikipedia](https://en.wikipedia.org/wiki/Gap_buffer)

References: [[Data Structures]] [[Computer Science]]