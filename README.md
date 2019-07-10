# Sass Activity

In this activity we'll be working with [Sass](https://sass-lang.com/) for the first time. We'll be using the officially recommended _SCSS syntax_ which is a _superset_ of CSS. A programming language superset contains all the features of a given language and has been expanded or enhanced to include other features as well. This means CSS is valid SCSS, so any valid CSS file can be given the `.scss` file extension and you now have a valid SCSS file.

Sass must be _compiled_ into CSS. A compiler has already been set up for you and will run and watch for file changes while running the `npm start` command in this repository. We won't go into details into how this is all set up in this course but for those curious you can read about it [here](https://www.npmjs.com/package/node-sass).

Throughout this activity you will be introduced to Sass's additional features one at a time. We will do this by modifying the `sass/styles.scss` file found in this repository. Links to relevant documentation will also be linked at the end of each section and at the bottom of this readme.

***
- [Rule Nesting](#rule-nesting)
	- [Ampersand Operator](#ampersand-operator)
	- [Rule Nesting Activity](#rule-nesting-activity)
- [Resources](#resources)
***




## Rule Nesting

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

***&mdash; [Documentation](https://sass-lang.com/documentation/style-rules#nesting)***



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




## Resources

- [Rule Nesting](https://sass-lang.com/documentation/style-rules#nesting)
