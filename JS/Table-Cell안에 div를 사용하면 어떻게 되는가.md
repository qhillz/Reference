# Table-Cell안에 div를 사용하면 어떻게 되는가?

Using a `div` instide a `td` is not worse than any other way of using tables for layout. (Some people never use tables for layout though, and I happen to be one of them.)

If you use a `div` in a `td` you will however get in a situation where it might be hard to predict how the elements will be sized. The default for a div is to determine its width from its parent, and the default for a table cell is to determine its size depending on the size of its content.

The rules for how a `div` should be sized is well defined in the standards, but the rules for how a `td` should be sized is not as well defined, so different browsers use slightly different algorithms.



```html
<!ELEMENT td %Flow;>
<!-- %Flow; mixes block and inline and is used for list items etc. -->
<!ENTITY %Flow "(#PCDATA | %block; | form | %inline; | %misc;>
<!ENTITY %block "p | %heading; | div | %lists; | %blocktext; | fieldset | table">
```

td 안의 block 요소 (p, heading, div, list...)들을 사용 가능하다.

The ['vertical-align'](https://www.w3.org/TR/CSS2/visudet.html#propdef-vertical-align) property of each table cell determines its alignment within the row. Each cell's content has a baseline, a top, a middle, and a bottom, as does the row itself. In the context of tables, values for ['vertical-align'](https://www.w3.org/TR/CSS2/visudet.html#propdef-vertical-align) have the following meanings:

- **baseline**

  The baseline of the cell is put at the same height as the baseline of the first of the rows it spans (see below for the definition of baselines of cells and rows).

- **top**

  The top of the cell box is aligned with the top of the first row it spans.

- **bottom**

  The bottom of the cell box is aligned with the bottom of the last row it spans.

- **middle**

  The center of the cell is aligned with the center of the rows it spans.

- **sub, super, text-top, text-bottom, <length>, <percentage>**

  These values do not apply to cells; the cell is aligned at the baseline instead.