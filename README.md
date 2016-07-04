# Spruce

A system for writing CSS that prioritises composing and low specificity.

## Tl;dr
* [Components] are 90% of your styles.
* [Modifiers] handle the state and variation of Components
* [Children] describe unavoidable relationships inside Components.
* [Tweaks] handle real word layout relationships between Components.

## Components

Components are 90% of your styles.  They are isolated elements that define the styling for a single object. A widget, a button or an image carousel, it doesn't matter where the components are placed they will look the same. 

* Components class names begin with a capital letter.
* Components are isolated. They do not rely on class hierarchy or other Components. 

```scss
.Button {
    cursor: pointer;
    padding: 1rem;
}
```


## Modifiers `-`
Modifiers handle the state and variation of Components. A button component might be red when in a warning state, a caption might be left or right aligned. The Modifiers dont change the base styles of a Component, only the bare minimum required to express the difference.

* Modifiers are written as the Component name folled by a hypen followed by the Modfiers name
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
Children describe unavoidable relationships inside Components.

* Children are written as the Component name folled by an underscore followed by the Childs name `ComponentName_childName`
* Children are not placed on the same markup as their parent

The media object is a classic example of unavoidable parent chiuld relationships. The `.Media` component by itself is just a clearfix and `.Media_image` is just a float.
However when used in conjuction they create a highly useful and reusable component. 

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


## Tweaks
Tweaks handle real word layout relationships between Components. They are used all over the place but don't often provide much detailed styling. They are often more about positioning and location over color and form. 

* Tweak classes are written as lowerCamelCase. 
* They can be applied to any markup.
* They affect the way components interact with each other

```scss
.marginRow2 {
    margin-top: 2rem;
    margin-bottom: 2rem;
}

.floatLeft {
    float: left;
}
```


### Ghotachs
### This is not allowed
### Naming
Spruce uses punctuation to define relationship and convey meaning. Because of this words are distinguished through camel case. 

### Style Sheet Order

* Configuration
* Components, Modifiers, Children
* Tweaks

[Components]: #components
[Modifiers]: #modifiers--
[Children]: #children-_
[Tweaks]: #tweaks
