[![npm version](https://badge.fury.io/js/@harvest-dev/ng-perfect-scrollbar.svg)](https://badge.fury.io/js/@harvest-dev/ng-perfect-scrollbar) [![Downloads](https://img.shields.io/npm/dm/@harvest/ngx-perfect-scrollbar.svg)](https://www.npmjs.com/package/@harvest-dev/ng-perfect-scrollbar) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/Harvest-Dev/ng-select2/master/LICENSE.md)

# Angular Perfect Scrollbar

This fork of [ngx-perfect-scrollbar](https://github.com/zefoy/ngx-perfect-scrollbar) is an Angular wrapper library for the [Perfect Scrollbar](https://utatti.github.io/perfect-scrollbar/). To use this library you should get familiar with the Perfect Scrollbar documentation as well since this documentation only explains details specific to this wrapper.

### Quick links

[Example application](https://harvest-dev.github.io/ngx-perfect-scrollbar/dist/ng-perfect-scrollbar/)
|
[Perfect Scrollbar documentation](https://github.com/utatti/perfect-scrollbar/)

### Installing and usage

```bash
npm install @harvest-dev/ng-perfect-scrollbar --save
```

### Requirements

-   peerDependencies:

    -   `angular` 16.1.0 and more
    -   `angular/cdk` 16.1.0 and more

##### Load the module for your app (with global configuration):

Providing the global configuration is optional and when used you should only provide the configuration in your root module.

```javascript
import { PerfectScrollbarModule } from 'ngx-perfect-scrollbar';
import { PERFECT_SCROLLBAR_CONFIG } from 'ngx-perfect-scrollbar';
import { PerfectScrollbarConfigInterface } from 'ngx-perfect-scrollbar';

const DEFAULT_PERFECT_SCROLLBAR_CONFIG: PerfectScrollbarConfigInterface = {
  suppressScrollX: true
};

@NgModule({
  ...
  imports: [
    ...
    PerfectScrollbarModule
  ],
  providers: [
    {
      provide: PERFECT_SCROLLBAR_CONFIG,
      useValue: DEFAULT_PERFECT_SCROLLBAR_CONFIG
    }
  ]
})
```

##### Use it in your HTML template (with custom configuration):

This library provides two ways to create a Perfect Scrollbar element, a component and a directive. Component tries to make the usage as simple as possible and the directive is meant for more custom / advanced use cases.

The scroll area always needs some fixed height to work. The default styles uses 100% as the height value so the parent needs to have fixed height or you need to set it via CSS styles. Otherwise the height keeps growing and you won't get the scrollbars.

**COMPONENT USAGE**

Simply replace the element that would ordinarily be passed to `PerfectScrollbar` with the perfect-scollbar component.

```html
<perfect-scrollbar style="max-width: 600px; max-height: 400px;" [config]="config">
    <div>Scrollable content</div>
</perfect-scrollbar>
```

```javascript
[config]                // Custom config to override the global defaults.
[disabled]              // Disables the Perfect Scrollbar initialization.

[usePSClass]            // Use 'ps' class (needed by the ps theme styles).

[autoPropagation]       // Automatic swipe and wheel propagation control.
[scrollIndicators]      // Enable fading edges scroll indicators showing.

(<psEventName>)         // All Perfect Scrollbar events work as bindings.
                        // Event names are in camel case (not kebab case).
                        // Example: ps-y-reach-start -> psYReachStart
```

**DIRECTIVE USAGE**

When using only the directive you need to provide your own theming or import the default theme:

```css
@import '~perfect-scrollbar/css/perfect-scrollbar.css';
```

Perfect Scrollbar directive should be used with div elements and can take optional custom configuration:

```html
<div class="ps" style="position: relative; max-width: 600px; max-height: 400px;" [perfectScrollbar]="config">
    <div>Scrollable content</div>
</div>
```

```javascript
[perfectScrollbar]      // Can be used to provide optional custom config.

[disabled]              // Disables the Perfect Scrollbar initialization.

(<psEventName>)         // All Perfect Scrollbar events work as bindings.
                        // Event namea are in camel case (not kebab case).
                        // Example: ps-y-reach-start -> psYReachStart
```

##### Available configuration options (custom / global configuration):

```javascript
handlers; // List of event handlers to scroll the element.
wheelSpeed; // Scroll speed for the mousewheel event (Default: 1).
swipeEasing; // Use easing for the swipe scrolling (Default: true).
suppressScrollX; // Disable X axis in all situations (Default: false).
suppressScrollY; // Disable Y axis in all situations (Default: false).
wheelPropagation; // Propagate wheel events at the end (Default: false).
useBothWheelAxes; // Always use both of the wheel axes (Default: false).
minScrollbarLength; // Minimum size (px) for the scrollbar (Default: null).
maxScrollbarLength; // Maximum size (px) for the scrollbar (Default: null).
scrollXMarginOffset; // Offset before enabling the X scroller (Default: 0).
scrollYMarginOffset; // Offset before enabling the Y scroller (Default: 0).
```

For more detailed documentation with all the supported events / options see the the Perfect Scrollbar documentation.

##### Available control / helper functions (provided by the directive):

```javascript
ps()                                        // Returns reference to the PS instance.

update()                                    // Updates the scrollbar size and position.

geometry(prefix)                            // Returns the geometry with specified prefix.
position(absolute)                          // Returns the reach or absolute scroll position.

scrollable(direction)                       // Checks if the given direction is scrollable.
                                            // Direction can be: 'any', 'both', 'x', 'y'

scrollTo(x, y, speed?)                      // Animate scroll to given x,y coordinates.
scrollToY(position, speed?)                 // Animate scroll to given vertical position.
scrollToX(position, speed?)                 // Animate scroll to given horizontal position.
scrollToTop(offset?, speed?)                // Animate scroll to given offset from the top.
scrollToLeft(offset?, speed?)               // Animate scroll to given offset from the left.
scrollToRight(offset?, speed?)              // Animate scroll to given offset from the right.
scrollToBottom(offset?, speed?)             // Animate scroll to given offset from the bottom.
scrollToElement(element, offset?, speed?)   // Animate scroll to given or matching HTML element.
                                            // Input can be HTMLElement or a query selector string.
```

Above functions can be accessed through the directive reference (available as directiveRef in the component). Position and offset needs to be given in pixels and speed in milliseconds.

### Publishing the library

```
npm run build:lib
npm run publish:lib
```

### Update Demo

```
npm run build:demo
```

#### Running the example

```bash
npm install
npm run start
```
