# Classic books

This is a Jekyll setup for turning markdown into HTML for simple classic books, e.g. from Project Gutenberg text files.

## Tips

This assumes you're using kramdown as your markdown engine.

### Poetry

Markdown for poetry is tricky. You want HTML that puts each verse in a paragraph, with line breaks between lines. Add two spaces at the end of each line so that the poetry reads easily in markdown, but the HTML will have a `<br />` at the end of each line.

Line numbers in poetry are tricky, too. Where line numbers are in the text at the ends of lines like this

```
Behold, my line of poetry, behold 5
```

you want the HTML to be

```
Behold, my line of poetry, behold <em class="line-number">5</em><br />
```

So that you can float those line numbers to the right with CSS:

```
em.line-number {
	display: block;
	float: right;
}
```

You can use a regex search-and-replace to add the markdown for this. Being careful not to apply this to numbers inside the poems, and with regex search on:

*	search for `(\d+)`
* 	replace with `\*\1\*{:.line-number}`

In the search, the `\d` finds any digit. Adding the `+` for `\d+` finds any string of digits; i.e. a number 10 or greater. The brackets tell the search to remember the number.

In the replace, the `\*` is an asterisk (escaped with a `\` to prevent regex thinking it's a wildcard). The `\1` places the number it remembers from the search. And the `{:.line-number}` is the kramdown inline attribute that creates the class attribute we need in the HTML `em` element.
