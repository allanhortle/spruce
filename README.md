# Spruce

A system for writing CSS that prioritises composing and low specificity.

## Tl;dr
* Components are 90% of your styles.
* Modifiers handle the state and variation of Components
* Children describe unavoidable relationships inside Components.
* Tweaks handle real word layout relationships between Components.

## Components
Components are 90% of your styles. They are discreet, repeatable sections of design that can be reused. Button, link, carousel, thumbnail, avatar. 

```
.Button {
}
```

* Components class names begin with a capital letter
* They must remain isolated. Components do not rely on class hierarchy or other classes. 

## Modifiers
Modifiers handle the state and variation of Components. Components may need to be described through changes in state or subtle changes. A button might be red when in a warning state. Or a caption might be left or right aligned.  

Modifiers 

## Children
## Tweaks

## Extras
### This is not allowed
### Naming
Spruce uses punctuation to define relationship and convey meaning. Because of this words are distinguished through camel case. 

### Style Sheet Order
