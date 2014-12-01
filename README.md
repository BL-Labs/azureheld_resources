Lists of items accessible from Azure storage
--------------------------------------------

Tags added or deleted from Flickr images:
=========================================
http://blmc.blob.core.windows.net/metadata/taghistory_20141120.tsv  [NB ~1.2GB]

    **Headings**:
    flickrid - photo id of the image
    enteredtext - Text entered by user
    from &
    to -    This tag appeared or dissapeared between these two scan dates (in epoch seconds).
    tagid - tag id given by flickr to the tag
    author - user id of commenter
    tag - simplyfied tag (eg for use in flickr's URL schemes)
    mode - 'add' or 'del' to show the tag either being added or removed.

Majority of tag removals will be for the image rotation - 'rotate' or a tag of that ilk removed and replaced by a tag such as 'rotated' or 'rotatedcc' to signify that the image has been rotated.

OCR data for the Book collection
================================

**General Filename format:**

000000000_00.txt  or _text.json

==>

[*book identifier*]_[*book volume*]...

See the book_metadata.json file for metadata for a given identifier.


"ocrplaintext" is a rendering of the entire volume as a single text file, broken up by easily recognisable scan number breaks. The JSON version is the same text, but the text is broken up by page in a hash, with the key corresponding to the scan number (a scan number of '1' is the front cover of the book for example).

Plain text example:
-------------------

From http://blmc.blob.core.windows.net/ocrplaintext/004159587_01.txt

NB On non-empty 'pages' are included in the plain text version:

    --8--
    Ife
    
    
    --9--
    AN HISTORICAL, TOPOGRAPHICAL, AND DESCRIPTIVE VIEW OF THE COUNTY PALATINE OF DURHAM; COMPREHENDING THE VARIOUS SUBJECTS OF NATURAL, CIVIL, AND ECCLESIASTICAL GEOGRAPHY, AGRICULTURE, MINES, MANUFACTURES, NAVIGATION, TRADE, COMMERCE, BUILDINGS, ANTIQUITIES, CURIOSITIES, PUBLIC INSTITUTIONS, CHARITIES, POPULATION, CUSTOMS, BIOGRAPHY, LOCAL HISTORY, $-c. VOLUME I. BY E. MACKENZIE AND M. ROSS. iSrlucasstlc upon STpiw: PRINTED AND PUBLISHED BY MACKENZIE AND DENT, 181, PILGRIM STREET SOLD ALSO BY THE BOOKSELLERS IN THE COUNTIES OF DURHAM, NORTHUMBERLAND, NEAVCASTLE, AND IN BERWICK, &C. 1834.
    
    
    --11--
    PREFACE. -••i»J-»e-»- Jr EW portions of the British Empire possess stronger claims to attention than the County Palatine of Durham. During six centuries, it was, in almost every thing but the name, a miniature kingdom ; and its " mitred princes" still possess a consi derable share of their ancient and peculiar dignities. The important place which it occupies in ...

To remove the page scan numbers, you can use 'grep' to do so. For example:

    grep -v -e "^--[0-9]\+--" 004159587_01.txt > 004159587_01_nopages.txt

To do this to a directory of files:

    ls /path/to/ocr/textfiles/*.txt | while read name; do grep -v -e "^--[0-9]\+--" $name > ${name%.*}_nopages.txt; done

JSON example
------------

For the same book: http://blmc.blob.core.windows.net/ocrjson/004159587_01_text.json

    [[1, ""], [2, ""], [3, ""], [4, ""], [5, ""], [6, ""], [7, ""], [8, "Ife"], [9, "AN HISTORICAL, TOPOGRAPHICAL, AND DESCRIPTIVE VIEW OF THE COUNTY PALATINE OF DURHAM; COMPREHENDING THE VARIOUS SUBJECTS OF NATURAL, CIVIL, AND ECCLESIASTICAL GEOGRAPHY, AGRICULTURE, MINES, MANUFACTURES, NAVIGATION, TRADE, COMMERCE, BUILDINGS, ANTIQUITIES, CURIOSITIES, PUBLIC INSTITUTIONS, CHARITIES, POPULATION, CUSTOMS, BIOGRAPHY, LOCAL HISTORY, $-c. VOLUME I. BY E. MACKENZIE AND M. ROSS. iSrlucasstlc upon STpiw: PRINTED AND PUBLISHED BY MACKENZIE AND DENT, 181, PILGRIM STREET SOLD ALSO BY THE BOOKSELLERS IN THE COUNTIES OF DURHAM, NORTHUMBERLAND, NEAVCASTLE, AND IN BERWICK, &C. 1834."], [10, ""], [11, "PREFACE. -\u2022\u2022i\u00bbJ-\u00bbe-\u00bb- Jr EW portions of the British Empire possess stronger claims to attention than the County Palatine of Durham. During six centuries, it was, in almost every thing but the name, a miniature kingdom ; and its \" mitred princes\" still possess a consi derable share of their ancient and peculiar dignities. The important place which it occupies in ...
