# Typography

Typography is how we stylise our text. Font, Color, Size, Spacing, Bolding and Italicize.

We customise the font styles, `h2`, `p`, `strong`, `em` because browsers default have a styling that changes depends on browsers.

`font-size:` can change the size of the font and uses an absolute size `px` or relative `em` (1em is 16px) 

`font-weight` determins the thickness of the font. It takes options like `bold` or number values going up in hundreds 0-1000.

`font-family` is used to change the fonts. You can also choose backup fonts if the computer can't load that font.

```css
p {
    font-family: "Times New Roman", Times, serif; /*first choice is Times New Roman, than Times and finally serif*/
}
```

To find new fonts use <u>Google Fonts</u> 