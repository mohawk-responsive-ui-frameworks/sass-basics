# Sass Activity

In this activity we'll be working with [Sass](https://sass-lang.com/) for the first time. We'll be using the officially recommended _SCSS syntax_ which is a _superset_ of CSS. A programming language superset contains all the features of a given language and has been expanded or enhanced to include other features as well. This means CSS is valid SCSS, so any valid CSS file can be given the `.scss` file extension and you now have a valid SCSS file.

Sass must be _compiled_ into CSS. Another name for this compilation is _preprocessing_. You can read about preprocessing [here](https://sass-lang.com/guide#topic-1). In short we compile SCSS into CSS at _compile time_ which then generates the CSS files to be served up **once**. The compilation is not done for every HTTP request, and recompilation only needs to be done when changes are made to the Sass files.

A compiler has already been set up for you and will run and watch for file changes while running the `npm start` command in this repository. We won't go into details into how this is all set up in this course but for those curious you can read about it [here](https://www.npmjs.com/package/node-sass).

Throughout this activity you will be introduced to Sass's additional features one at a time. We will do this by modifying the `sass/styles.scss` file found in this repository. Links to relevant documentation will also be linked at the end of each section and at the top of this readme.

***Any errors that may happen at compilation can be checked in your terminal. If changes aren't showing up on your webpage you may have an error.***

***
- [Rule Nesting](#rule-nesting)
	- [Ampersand Operator](#ampersand-operator)
	- [Activity](#rule-nesting-activity)
- [Variables](#variables)
- [Imports](#imports)
- [Functions](#functions)
- [Mixins](#mixins)
- [Resources](#resources)
***




## Rule Nesting

Take a moment to read this section of Sass's [documentation](https://sass-lang.com/guide#topic-3).

Rule nesting allows us to write our Sass in a more concise manner that also makes it easier to change a parent class name without updating it in multiple spots in your Sass file. To make things clearer here's an example of CSS rewritten using Sass nesting you can find in `sass/styles.scss`. The SCSS compiles into the CSS version making them functional equivalents:

***
**CSS**
```css
.gallery {
	text-align: justify;
}

.gallery .card {
	margin-bottom: 1rem;
}

.gallery .card-title {
	font-size: 1.25rem;
}

.gallery .card-footer {
	text-align: right;
}
```
***
**SCSS**
```scss
.gallery {
	text-align: justify;

	.card {
		margin-bottom: 1rem;
	}

	.card-title {
		font-size: 1.25rem;
	}

	.card-footer {
		text-align: right;
	}
}
```
***



### Ampersand Operator

Sass has an _operator_ that uses the character `&` to represent all parent rule nesting. If we modify our previous example to the following code, the `&` would represent `.gallery` and be functionally the same:

```scss
.gallery {
	text-align: justify;

	& .card {
		margin-bottom: 1rem;
	}

	& .card-title {
		font-size: 1.25rem;
	}

	& .card-footer {
		text-align: right;
	}
}
```

Using `&` like this isn't very useful, but where it does come in handy is when we want to define a rule for an element with two class names like so:

***
**SCSS**
```scss
.gallery {
	&.foo {

	}

	&:hover {

	}
}
```
***
**CSS**
```css
.gallery.foo {

}

.gallery:hover {

}
```
***



### Rule Nesting Activity

Implement rule nesting within `sass/styles.scss` wherever reasonably possible. Try to complete activities on your own but check your work with the [expected outcome](.readme-assets/rule-nesting.scss).

***&mdash; [Documentation](https://sass-lang.com/guide#topic-3)***




## Variables

Take a moment to read this section of Sass's [documentation](https://sass-lang.com/guide#topic-2).

Imagine a very large CSS file that made use of the same colours multiple times. Now imagine wanting to change said colour into something else. You could use search and replace to accomplish this but Sass offers a much nicer way to keep track of colours that additionally provide context while reading through your code.

We can see a small example of multiple colours being used within our `sass/styles.css` file. The colour `#cf649a` appears twice and `#af447a` appears once. Lets put these values into Sass variables at the top of our file before any rules.

```scss
$color-main-heading: #cf649a;
$color-main-heading-dark: #af447a;
```

Now replace the hard-coded colour values throughout your Sass like so, but using the appropriate variable names:

```scss
color: $variable-name;
```

You can see the expected results [here](.readme-assets/variables-color.scss).

***&mdash; [Documentation](https://sass-lang.com/guide#topic-2)***




## Imports

Take a moment to read this section of Sass's [documentation](https://sass-lang.com/guide#topic-5).

Sass's `@import` directive allows us to split our Sass up into multiple files while still outputting a single CSS file. This helps us organize our styles so we don't end up working with files that end up being thousands of lines long which can put a real stint in development productivity.

CSS also has an `@import` directive but it's not very performant. It requires the CSS file to be requested, downloaded, then parsed before sending another request for the related CSS file. This problem is compounded when you're importing files that import additional files. Sass has none of these issues as imports are inlined at time of compilation.

Lets start things off by moving all of our variables into their own file. Make a new file called `_variables.scss` alongside `styles.scss` both within the `sass` folder. This makes `styles.scss` our _entry point_ and therefore should **not** start with an underscore. Any file that is not an entry point for a CSS file we want to generate should be prefixed with an underscore. Non-entry point files we import can be referred to as _partials_ and you can read more about them [here](https://sass-lang.com/guide#topic-4).

- **BAD:** `variables.scss`
- **GOOD:** `_variables.scss`

Move the variables into the newly created file and at the top of `styles.scss` add the following SCSS:

```scss
@import "variables";
```

To test if this worked remove `public/styles.css` and rerun `npm start`. If your web page is still styled, it worked!

Split up the remaining SCSS into separate files into the following files:

| Filename | Description |
| --- | --- |
| `_base.scss` | Contains some base rules applied to whole elements such as `html` and `body`. |
| `_main-header.scss` | Contains all styles for `.main-header`. |
| `_hero-banner.scss` | Contains all styles for `.hero-banner`. |
| `_gallery.scss` | Contains all styles for `.gallery`.
| `_main-footer.scss` | Contains all styles for `.main-footer`. |

Take note that splitting things up into files this small can be a little silly. It makes far more sense when things get larger and more unwieldy. Different people also have preferences for how big an import should be and it's a fairly subjective topic. Imports can also be used to import libraries which we'll be going through in the next module.

When complete you can see the expected result [here]().

***&mdash; [Documentation](https://sass-lang.com/guide#topic-5)***




## Functions

Functions allow us to pass values as _parameters_ to resolve into another function. To keep things light and simple we're just going to be using the `darken` function. Looking at the [documentation](https://sass-lang.com/documentation/functions/color#darken) for this function we see it has two parameters: `$color`, and `$amount`. We can call the function like this, so it resolves to a function twenty percent darker than pure white:

```scss
darken(#fff, 20%);
```

In `_variables.scss` we can see that we set the colour of the `h1` element and on hover, transition it into another darker colour. Lets utilize the `darken` function here:

```scss
$color-main-heading: #cf649a;
$color-main-heading-dark: darken($color-main-heading, 5%);
```

If the usefulness of this isn't all too clear the next section should highlight it for you.

***&mdash; [Documentation](https://sass-lang.com/documentation/functions)***




## Mixins

Take a moment to read this section of Sass's [documentation](https://sass-lang.com/guide#topic-6).

Mixins are a feature that allow us to compose our styles including full rulesets. They also take _parameters_ that allow us to generate CSS dynamically. For now we're just going to learn the very basics of mixins and build on that in the next module.

Create a new file called `_mixins.scss` and `@import` it directly after our `_variables.scss` import. Write the following mixin code into our newly imported `_mixins.scss` file.

```scss
@mixin color-with-hover($color) {
	color: $color;
	transition: color .2s linear;
	&:hover {
		color: darken($color, 5%);
	}
}
```

Now update the `_main-header.scss` file to contain the following contents:

```scss
.main-header {
	background-color: #036;

	h1 {
		margin-bottom: 0;
		font-style: italic;
		@include color-with-hover($color-main-heading);
	}
}
```

The `@include` directive is how we apply a previously declared mixin. Also take note of how we no longer need the `$color-main-heading-dark` variable anymore. This mixin also wouldn't be possible to implement without the `darken` function, we would instead need to implement a second parameter for `$hover-color`.

When complete you can see the expected result [here]().

***&mdash; [Documentation](https://sass-lang.com/guide#topic-6)***




## Resources

- [Rule Nesting](https://sass-lang.com/guide#topic-3)
- [Variables](https://sass-lang.com/guide#topic-2)
- [Imports](https://sass-lang.com/guide#topic-5)
- [Partials](https://sass-lang.com/guide#topic-4)
- [Mixins](https://sass-lang.com/guide#topic-6)
- [Functions](https://sass-lang.com/documentation/functions)
- [Function: `darken`](https://sass-lang.com/documentation/functions/color#darken)
- [Function: `lighten`](https://sass-lang.com/documentation/functions/color#lighten)
