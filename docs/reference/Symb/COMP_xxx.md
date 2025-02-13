##### Symbolic Value : Compound Text
##### COMP_xxx - CompoundTextXxx () Control Flags
---
```
#include <easycd.h>
```

**Symbolic Values :**

	COMP_FROM_FILE	  -  CompoundText is derived from a file.

	COMP_PRESERVE_LINES	  -  Insert a line break (0) for each line delimiter found in the input text buffer. This preserves input line breaks.

	COMP_PARA_LINE	  -  Create a new paragraph for each line delimiter found in the input text buffer.

	COMP_PARA_BLANK_LINE	  -  Create a new paragraph for each blank line found in the input text buffer. A blank line is defined as a line containing just a line delimiter (specified by the pszLineDelim parameter to CompoundTextAddTextExt).

	COMP_SERVER_HINT_FOLLOWS	  -  A "hint" follows the comment for a document link. If this flag is set, the pszComment argument points to the comment string, the terminating NUL ('\0'), the hint string, and the terminating NUL.


**Description :**

The flags COMP_FROM_FILE, COMP_PRESERVE_LINES, COMP_PARA_LINE, and COMP_PARA_BLANK_LINE control the way CompoundTextAddTextExt parses the input text buffer (or file) to create a sequence of CD records. Combine these flags by bitwise OR-ing them together.<br>
<br>
If the COMP_FROM_FILE flag is clear, CompoundTextAddTextExt adds the number of text characters specifed by the dwTextLen parameter and starting at the address specified by the pchText parameter to the compound text context.  If the COMP_FROM_FILE flag is set, CompundTextAddTextExt treats the text specified by pchText as the name of a file, and the dwTextLen parameter is ignored.  CompundTextAddTextExt opens and reads the specified file, and adds its contents to the compound text context.<br>
<br>
For input from a typical text buffer, just specify COMP_PRESERVE_LINES.  For input from a typical character text file, specify COMP_FROM_FILE | COMP_PRESERVE_LINES | COMP_PARA_BLANK_LINE.  <br>
<br>
If the COMP_PRESERVE_LINES flag is set, CompoundTextAddTextExt preserves the line breaks it finds in the input text. For each line delimiter found in the input, CompoundTextAddTextExt inserts a hard line break (a zero byte) in the CDTEXT record. Set COMP_PRESERVE_LINES if your input text contains lines that should remain separate after input into Domino or Notes. Clear COMP_PRESERVE_LINES if you do not need to perserve the line formatting of your input text.<br>
<br>
The flags COMP_PARA_LINE and COMP_PARA_BLANK_LINE control when CompoundTextAddTextExt emits a new paragraph.  A new paragraph in the compound text context consists of a CDPARAGRAPH record followed by a CDPABREFERENCE record.<br>
<br>
The flag COMP_PARA_LINE causes CompoundTextAddTextExt to emit a new paragraph for each line delimiter it encounters in the input.<br>
<br>
The flag COMP_PARA_BLANK_LINE causes CompoundTextAddTextExt to emit a new paragraph only when it encounters a line containing just a line delimiter. <br>
<br>
If neither COMP_PARA_LINE nor COMP_PARA_BLANK_LINE are set, CompoundTextAddTextExt will break large amounts of input into paragraphs of approximately 10K of text each. <br>
<br>
Note: it is redundant to specify both COMP_PARA_LINE and COMP_PARA_BLANK_LINE.<br>
<br>
Note: if both COMP_PARA_LINE and COMP_PRESERVE_LINES are specified, CompoundTextAddTextExt ignores COMP_PRESERVE_LINES.
<ul><br>
<br>
CompoundTextAddTextExt can add up to 5 megabytes of text to a rich text item.  The input text from either a memory buffer or a file is automatically divided into Domino items that are approximately 30 kilobytes in size.  If COMP_PARA_LINE is not specified, or if COMP_PARA_BLANK_LINE is specified and no blank lines are found, a paragraph is automatically emitted after every 10 kilobytes of text.<br>
<br>
The flag COMP_SERVER_HINT_FOLLOWS is used with the compound text document link functions to provide a &quot;hint&quot; string containing a server name following the doclink record.  The server name follows the comment string.  If this flag is set, the pszComment parameter points to two consecutive NUL-terminated strings:  the comment string, the NUL terminator ('\0'), the server name, and a second NUL terminator.</ul>



**See Also :**
[CompoundTextAddDocLink](/domino-c-api-docs/reference/Func/CompoundTextAddDocLink)
[CompoundTextAddTextExt](/domino-c-api-docs/reference/Func/CompoundTextAddTextExt)
---
