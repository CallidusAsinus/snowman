# Chickpea

Chickpea is a Twine 2 story format based on [Snowman](https://github.com/videlais/snowman). It's meant to be used in the second semester of Coding for Filmmakers at BSA.

Like Snowman, Chickpea is a minimal Twine 2 story format designed for people who already know
JavaScript and CSS. It's designed to implement basic functionality for playing
Twine stories and then get out of your way.

Chickpea includes [jQuery](http://jquery.com) and [Underscore](http://underscorejs.org/) for you.

## Changes From The Norm

It uses Underscore templating to provide interactivity. Specifically, passages are rendered onscreen with this process:

1. The passage source is run through Underscore's [_.template() method](http://underscorejs.org/#template). Code in `<% blocks %>` receive two special variables:

	* `s`, which is a shorthand for `window.story.state`
	* `$`, which acts like jQuery's `$` method but with one exception. If you pass it a single function, this function is run when the passage appears onscreen, with it bound to the passage DOM element.

2. Comments inside `/* inline blocks */` are removed, as are `// line comments`. `//` comments remove their line break, so that:
```
The die comes up...

// TODO: randomize this properly
Three!
```
is rendered as:
```
The die comes up...

Three!
```
Line comments (that is, ones that start with //) may be used at the very start of a line. This is to avoid problems when URLs appear in the text, which might otherwise accidentally trigger a comment.

3. All double-bracketed links (`[[passage]]`, `[[displayed->passage]]`, and `[[passage<-displayed]]` are converted to functional links.

## Building From Source

Run `npm install` to install dependencies. `npm run build` will create a Twine 2-ready story format under dist/, as well as a guide to Snowman features at `dist/guide.html`. `npm start` will start a file watching process that updates the story format as changes are made under `src/`.

To check for style errors, run `npm run lint`. To run unit tests, run `npm test`. Please ensure that both run cleanly before submitting a pull request.
