# Spruce

A system for writing CSS that uses strict class naming rules to prioritize composing and low specificity.

## Tl;dr
* [Components] are 90% of your styles.
* [Modifiers] handle the state and variation of Components
* [Children] describe unavoidable relationships inside Components.
* [Peers] handle relationships between Components.
* [Tweaks] are a last resort for problems with real-world designs.

## Components

> Components are 90% of your styles. 

They are isolated elements that define the styling for a single object. A widget, a button or an image carousel. It doesn't matter where the components are placed they will look the same. 

* Component class names begin with a capital letter.
* Components are isolated. They do not rely on class hierarchy or relationships with other Components.
* Components are defined in a single file per Component.

```scss
.Button {
    cursor: pointer;
    padding: 1rem;
}

// bad
.Carousel {
    .Button {
        ...
    }
}
```


## Modifiers `-`
> Modifiers handle state and variation in Components.

A button component might be red when in a warning state, a caption might be left or right aligned. The Modifiers do not change the base styles of a Component, only the bare minimum required to express the difference.

* Modifiers are written as: `Component-modifier`
* Modifiers are not placed on markup without their Component.

```scss
.Button {
    cursor: pointer;
    padding: 1rem;
}

.Button-red {
    background-color: red;
}

.Button-large {
    padding: 2rem;
}
```
```html
<div class="Button">Regular button</div>
<div class="Button Button-red">Red Button</div>
<div class="Button Button-red Button-large">Large, red button</div>
```



## Children `_`
> Children describe unavoidable relationships inside Components. 

Sometimes a Component will need to rely on a relationship between the styles of the parent and the elements inside. Instead of increasing specificity by the use of nesting or the `>`selector we can express the relationship in the semantics of a class name. This allows the developer to understand the relationship perfectly while retaining a singular level of specificity. 

* Children are written as `ComponentName_childName`
* Children are not placed on the same markup as their parent
* All parent modifiers are placed on their children. `Parent Parent-modifier`, `Parent_child Parent_child-modifier`

The media object is a classic example of unavoidable parent child relationships. The `.Media` component by itself is only a clear-fix and `.Media_image` is a float and margin. Used in isolation these classes are pointless. However when used in conjunction as a parent and child they create a highly useful and reusable component. 

```scss
.Media {
    @include clearfix;
}

.Media_body {
    overflow: hidden;
}

.Media_image {
    float: left;
    margin-right: 1rem;
}
```

```html
<div class="Media">
	<div class="Media_image"></div>
	<div class="Media_body"></div>
</div>
```

### Child modifiers
To keep a flat level of specificity parent modifiers must be applied to each child.

```html
<div class="Media Media-right">
    <div class="Media_image Media_image-right"></div>
    <div class="Media_body Media_body-right"></div>
</div>
```

### Warnings
Some more complex modules may seem like they require a parent child relationship when in actual fact they just share a similar location or theme. These are better described as a collection of Components. 

See Component Grouping. 

## Peers
> Peers handle relationships between Components.

## Tweaks
> Tweaks are a last resorts for problems with real-world designs. 

Describing Components as isolated islands that don't interact with their location or neighboring Components goes a long way to maintaining reusable and composeable styles but using them in the real world doesn't always work out so neatly.

An `Input` component might in most cases require a small margin-bottom to keep the forms rows evenly spaced, but in one location the design requires a larger piece of text inserted between two `Inputs`. The `Title` component  would seem like a good fit but that has a large margin-top and when placed next to the `Input` the resulting extra space is unfit for the design. Neither of these Components are wrong in their description of styling, it is their combination that yields poor results. One solution might be to create a modifier on either `Title` or `Input` but this would create an unnecessary relationship between out two components. It may as well be called `Title-whenUsedAfterInput`. On top of this the changing nature the web could mean that this design might not be in use for very long. If we were to describe this relationship in our component there is a very real chance that over time it may be describing something that no longer exists. Which would only cause confusion for future developers.

The solution is to use Tweaks. Tweaks provide targeted minor layout changes that help to arrange Components next to each other. Tweaks are distinguished from components by their `lowerCamelCase` class names. 

So our problem above can be solved with the use of just one `marginTop0` tweak. 

```html
<form>
    <input class="Input" />
    <label class="Title Title-large marginTop0">Large Text</label>
    <input class="Input" />
</form>
```

* Tweak class names are written as lowerCamelCase. 
* Tweak classes are never defined in Component files.
* Tweaks are defined after Components.
* Tweaks can be applied to any markup.
* Tweaks only affect the way components interact with each other.

```scss

.marginTop0 {
    margin-top: 0;
}

.marginRow2 {
    margin-top: 2rem;
    margin-bottom: 2rem;
}

.floatLeft {
    float: left;
}
```


## Gotchas

### Component Grouping
There is often a tendency to create unnecessary relationships due to a components physical location rather than its shared attributes. Say Carousel contains a large button used as a call to action. It may seem logical to label this `Carousel_button` or`Carousel_callToAction`to show the relationship but in actual fact the buttons position inside this carousel does not actually effect its styling in any way. This would be better represented as either a modifier of `Button`or if sufficiently distinct from it a whole new a Component labeled `CallToAction`

### namingConventions
Spruce's main aim is to standardize specificity and class name confusion by using punctuation to define relationships and convey meaning. Because of this all punctuation is reserved for defining relationships and so multiple words are separated through camel case. 

```html
<!-- bad -->
<div class="bluetooth-list--selected"><div>
<div class="large_red_button"><div>

<!-- Good -->
<div class="BluetoothList BluetoothList-selected"><div>
<div class="Button Button-large Button-red"><div>
```

Words are always written out in full. Needless confusion is created when one developer shortens a word to what they deem logical only for another developer to have know idea what it refers to. The main point of Spruce is to clearly define 

```scss
// Bad
.Btn-lrg
.UsrPrfl

// Good
.Button-large
.UserProfile
```

### Style Sheet Order

* Configuration
* Components, Modifiers, Children
* Tweaks

[Components]: #components
[Modifiers]: #modifiers--
[Children]: #children-_
[Peers]: #peers-_
[Tweaks]: #tweaks
