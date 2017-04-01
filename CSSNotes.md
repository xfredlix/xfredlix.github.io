# CSS

- Pseudo-classes: select elements that already exist, :

- Pseudo-elements: create faux elements you can style, ::

- ID: 1-0-0, class: 0-1-0, type: 0-0-1

- Clearfix: technique used to contain floats, uses :before and :after pseudo-elements on the parent element
.group:before,
.group:after {content: ""; display: table;}
.group:after {clear: both;}
.group {*zoom: 1;}

- Position:
- relative is the same as static butit accepts the box offset properties top, right, bottom, and left
Give parent position: relative, and children position: absolute. box-offset properties can be used with relative, absolute and fixed, if a position is not specified, it will be positioned to the document body. In order to apply the z-index property to an element, you must first apply a position value of relative, absolute, or fixed

- Drop units from zero values: div {margin: 20px 0; letter-spacing: 0; padding: 0 5px;}

- Nest classes to only two or three layers deep: .news .special { ... }

- Layer styles with multiple classes: <a class="btn btn-danger">...</a><a class="btn btn-success">...</a>
.btn {font-size: 16px;}
.btn-danger {background: red;}
.btn-success {background: green;}

- Colors: keywords, hexadecimal notation, RGB and HSL values

- Lengths:
- Absolute Lengths: 1 px = 1/96th of an inch
- Relative Lengths: Percentages Percentage lengths are defined in relation to the length of another object, em length is calculated based on an element’s font size

- Images should always include the alt attribute, The alt attribute value should be very descriptive of what the image contains

### Responsive Web Design

1) Flexible layout: Use percentage-based grids instead of fixed-width, pixel-based grids
target / context = %
.span {width: 90px;} 1 column for a 300 px wide element 90 / 300 = .3
.span {width: 30%;}

2) Flexible media
- img, video, canvas {max-width: 100%;} doesn't let media scale above its native resolution, as the viewport gets smaller any media will scale down according to its containers width
- for iframes and embedded media, max-width doesn't work, instead use this css
 parent {height: 0; padding-bottom: 56.25%; /* 16:9 */ position: relative; width: 100%;}
iframe {height: 100%; left: 0; position: absolute; top: 0; width: 100%;}

3) Media queries
- types: all, screen, print, tv, and braille, screen is default, screen and print most common
- feature: name value pair, width and orientation most common
- logical operators: and (allows extra conditions to be added), not (negates the query, specifying any query but the one identified), only
- when using the not and only logical operators the media type may be left off, in which the media type defaults to all
- the min prefix indicates a values of greater than or equal to while the max prefix indicates a value of less than or equal to, min-width and max-width most common
- @media (min-width: 600px) {/* styles for 600px and up here */}
- @media (max-width: 38em) {/* styles for 38em and down here */}
- large resolution first use max-width
- small resolution first use min-width
- use em because its relative to its parent and font size
- the orientation media feature determines if a device is in the landscape or portrait orientation. The landscape mode is triggered when the display is wider than taller and the portrait mode is triggered when the display is taller than wider
- @media all and (orientation: landscape) {...}
- <meta name="viewport" content="width=device-width, initial-scale=1">
- @viewport {width: device-width; zoom: 1;}

- Touch Target Area: min 44px X 44px, use padding instead of margin

- Hover States: don't hide content behind :hover, click nav bar for dropdown instead of hover

- Contrast: try your site outside in the sun, in bed when it's dark, take it with you

- Readability: small screen !== small type, increase font size