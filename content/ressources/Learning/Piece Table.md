---
title: Piece Table
draft: false
publish: true
tags:
  - data-structures
  - software-architecture
date: 2024-09-02
---
- In [computing](https://en.wikipedia.org/wiki/Computing), a **piece table** is a [data structure](https://en.wikipedia.org/wiki/Data_structure) typically used to represent a [text document](https://en.wikipedia.org/wiki/Text_document) while it is edited in a [text editor](https://en.wikipedia.org/wiki/Text_editor). Initially a reference (or 'span') to the whole of the original file is created, which represents the as yet unchanged file. Subsequent inserts and deletes replace a span by combinations of one, two, or three references to sections of either the original document or to a buffer holding inserted text.[[1]](https://en.wikipedia.org/wiki/Piece_table#cite_note-crowley-1)
- Typically the text of the original document is held in one [immutable](https://en.wikipedia.org/wiki/Immutable_object) block, and the text of each subsequent insert is stored in new immutable blocks. Because even deleted text is still included in the piece table, this makes multi-level or unlimited [undo](https://en.wikipedia.org/wiki/Undo) easier to implement with a piece table than with alternative data structures such as a [gap buffer](https://en.wikipedia.org/wiki/Gap_buffer).

References: [[Data Structures]] [[Software Architecture]] [[Computer Science]]