# sassy-mixins

Just some Sass mixins

- [Mixins](#mixins)
	- [Clearfix](#clearfix)
	- [Embed](#embed)
	- [Font-Face](#font-face)
	- [Hidden](#hidden)
	- [Position](#position)
	- [Text-Truncate](#text-truncate)
- [Functions](#functions)
	- [Font-Size](#font-size)

## Mixins

```scss
@import 'sassy-mixins/mixins';
```

### Clearfix

```scss
.clearfix {
	@include clearfix();
}
```

Compiles to:

```css
.clearfix::after {
	content: '';
	display: table;
	clear: both;
}
```

### Embed

Responsive embeds, like videos or iFrames. By default the ratio is 16:9. Other options are
'4:3', '1:2', '2:1', '1:1' or custom numbers. Also accepts lists.

```scss
.embed {
	@include embed-container();

	iframe,
	embed,
	object,
	video {
		@include embed-element();
	}
}
```

Compiles to:

```css
.embed {
	height: 0;
	position: relative;
	padding-bottom: 56.25%;
}

.embed iframe,
.embed embed,
.embed object,
.embed video {
	border: 0;
	height: 100%;
	left: 0;
	position: absolute;
	top: 0;
	width: 100%;
}
```

### Font-Face

```scss
@include font-face('OpenSans', '../fonts/OpenSans-Regular', $svg: 'OpenSansRegular');
```

Compiles to:

```css
@font-face {
	font-family: "OpenSans";
	src: url("../fonts/OpenSans-Regular.eot");
	src: url("../fonts/OpenSans-Regular.eot?#iefix") format("embedded-opentype"), url("../fonts/OpenSans-Regular.woff2") format("woff2"), url("../fonts/OpenSans-Regular.woff") format("woff"), url("../fonts/OpenSans-Regular.ttf") format("truetype"), url("../fonts/OpenSans-Regular.svg#OpenSansRegular") format("svg");
	font-style: normal;
	font-weight: normal;
}
```

Some font types are missing? Just update the `$exts` property:

```scss
@include font-face('Only-Woff', '../fonts/OnlyWoff', $exts: woff2 woff);
```

### Hidden

Only display content to screen readers

```scss
.hidden {
	@include hidden();
}
```

Compiles to:

```css
.hidden {
	border: 0;
	clip: rect(0, 0, 0, 0);
	height: 1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	white-space: nowrap;
	width: 1px;
}
```

### Position

```scss
.absolute {
	@include absolute(top 0 left 1rem);
}

.relative {
	@include relative(left 50%);
}

.fixed {
	@include fixed(0 0 0 0);
}

.sticky {
	@include sticky(top);
}
```

Compiles to:

```css
.absolute {
	position: absolute;
	top: 0;
	left: 1rem;
}

.relative {
	position: relative;
	left: 50%;
}

.fixed {
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
}

.sticky {
	position: sticky;
	top: 0;
}
```

### Text-Truncate

```scss
.text-truncate {
	@include text-truncate();
}
```

Compiles to:

```css
.text-truncate {
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
```

## Functions

### Font-Size

A font-size helper function for em and rem units

```scss
@import 'sassy-mixins/functions';

$font-size-base: 16px;  // Define base font-size

h1 {
	font-size: rem(30);

	> span {
		font-size: em(24, 30);
	}
}
```

Compiles to:

```css
h1 {
	font-size: 1.875rem;
}

h1 > span {
	font-size: 0.8em;
}
```

---

[Further examples](./test/)

## License

[MIT](./LICENSE)
