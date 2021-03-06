# stylize

[![Build Status](https://travis-ci.org/alexfish/stylize.svg)](https://travis-ci.org/alexfish/stylize)

A funcitonal wrapper of NSAttributedString for easy string styling

## Contents

* [Why does NSAttributedString need a wrapper?](#why-does-nsattributedstring-need-a-wrapper)
* [Integration](#integration)
    * [Cocoapods](#cocoapods)
    * [Manual](#manual)
        * [iOS 8+](#ios-8)
* [Usage](#usage)
    * [Substrings](#substrings)
    * [Composing Styles](#composing-styles)
* [Available Attributes](#available-attributes)

## Why does NSAttributedString need a wrapper?

Styling strings with NSAttributedString requires a lot of painful and ugly boiler plate code, for example changing the color of a substring and underlining it requires:

```swift
let string = NSMutableAttributedString(string: "Hello")
string.addAttribute(NSforegroundAttributeName, value: UIColor.redColor(), range: NSMakeRange(0, 5))
string.addAttribute(NSUnderlineStyleAttributeName, value: NSUnderlineStyle.StyleSingle.rawValue, range: NSMakeRange(0, string.length))
```

Ouch!

This quickly builds into a giant chunk of code that is a pain to read and maintain. Using stylize our code looks like this:

```swift
let string          = NSAttributedString(string: "Hello World")
let foregroundStyle = Stylize.foreground(UIColor.redColor(), range: NSMakeRange(0, 5))
let underlineStyle  = Stylize.underline(NSUnderlineStyle.StyleSingle)
let style           = Stylize.compose(foregroundStyle, underlineStyle)

let styledString    = style(string)
```

That's better.

## Integration

### Cocoapods

Add `pod "Stylized"` to your `Podfile`

### Manual

#### iOS 8+
1. Add Stylize to you project as a submodule using `git submodule add https://github.com/alexfish/stylize.git`
2. Open the `Stylize` folder & drag `Stylize.xcodeproj` into your project tree
3. Add `Stylize.framework` to your target's `Link Binary with Libraries` Build Phase
4. Import Stylize with `import Stylize` and you're ready to go

## Usage

```swift
let string        = NSAttributedString(string: "Hello World")
let style         = Stylize.foreground(UIColor.redColor())
let styledString  = style(string)
```

#### Substrings

By default styles will be applied to the entire string, if you need to apply a style to a subsstring an optional `range` paramater is available for each style:

```swift
let string        = NSAttributedString(string: "Hello World")
let style         = Stylize.foreground(UIColor.redColor(), range: NSMakeRange(0, 5))
let styledString  = style(string)
```

#### Composing Styles

stylize has a `compose` function that can compose a style from multiple styles

```swift
let string          = NSAttributedString(string: "Hello World")
let foregroundStyle = Stylize.foreground(UIColor.redColor())
let backgroundStyle = Stylize.background(UIColor.orangeColor())
let underlineStyle  = Stylize.underline(NSUnderlineStyle.StyleSingle)

let style           = Stylize.compose(foregroundStyle, backgroundStyle, underlineStyle)
let styledString    = style(string)
```

## Available Attributes

| Attribute  | Function |
| ------------- | ------------- |
| NSUnderlineStyleAttributeName  | `underline(style: NSUnderlineStyle)`  |
| NSUnderlineColorAttributeName | `underline(color: UIColor)` |
| NSForegroundColorAttributeName | `foreground(color: UIColor)` |
| NSBackgroundColorAttributeName | `background(color: UIColor` |
| NSStrikethroughStyleAttributeName  | `strikethrough(style: NSUnderlineStyle)`  |
| NSStrikethroughColorAttributeName | `strikethrough(color: UIColor)` |
| NSLinkAttributeName | `link(url: NSURL)` |
| NSParagraphStyleAttributeName | `paragraph(style: NSParagraphStyle)` |
| NSKernAttributeName | `kern(points: NSNumber)` |
| NSBaselineOffsetAttributeName | `baseline(offset: NSNumber)` |
| NSShadowAttributeName | `shadow(shadow: NSShadow)` |
| NSStrokeWidthAttributeName| `stroke(width: NSNumber)` |
| NSStrokeColorAttributeName | `stroke(color: UIColor)` |
| NSTextEffectAttributeName | `letterpress()` |
| NSFontAttributeName | `font(font: UIFont)` |
| NSLigatureAttributeName | `ligatures(enabled: Bool)` |
| NSObliquenessAttributeName | `obliqueness(skew: NSNumber)` |
| NSAttachmentAttributeName | `attachment(attachement: NSTextAttachment)` |
| NSExpansionAttributeName | `expand(log: NSNumber)` |
| NSWritingDirectionAttributeName | `direction(direction: WritingDirection)` |
