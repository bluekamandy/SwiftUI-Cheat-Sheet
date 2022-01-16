# SwiftUI Cheat Sheet

This document is a cheat sheet I created for myself but perhaps it will be useful to others. I will continue to work on it as I learn more about SwiftUI. If you see mistakes or have suggestions, please feel free to contact me at masood@masoodkamandy.com.

## What is SwiftUI

SwiftUI is a domain-specific programming language embedded within Swift that leverages [Swift's function builders](https://www.vadimbulavin.com/swift-function-builders-swiftui-view-builder/) concept. Unlike UIKit, SwiftUI has a declarative syntax and handles updating views for you. The design of SwiftUI generally results in complex user interfaces being possible with very little code.

What I hope this guide eventually does is to help demystify something that can seem quite opaque at first. I'm also hoping this can be a repository for my own research in the area so that I don't have to re-learn concepts when I need them.

## Creating a New SwiftUI App

It's always good to know what the default code in an app is. Let's take a look at `ContentView.swift`. SwiftUI is unique in that the default app actually includes a lot of clues as to how SwiftUI works:

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .padding()
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

The first struct `ContentView` is where all of your UI design will happen. By default, everything in SwiftUI starts out **centered**. All of the declarative structures in SwiftUI are **capitalized**. So you can see that the 

SwiftUI code is parsed into a tree structure, so there is a lot of **[method chaining](https://en.wikipedia.org/wiki/Method_chaining)** ([another link](https://blog.avenuecode.com/how-well-do-you-know-swiftui)) for modifying views. The structure of a user interface is based on various ContentViews that are placed on the screen and filled with different types of content. If you look at the view debugging of the basic app, you'll see this structure.

![Screen Shot 2022-01-16 at 2.12.28 PM](/Users/masoodkamandy/Desktop/_LAYER/_CurrentCoding/SwiftUI-Cheat-Sheet/images/ViewDebug.png)

## SwiftUI is Based on a Tree Structure

In the baseline code for a SwiftUI app, there is only one child within the body of the ContentView's body: the text label. That child has a child, which is the modifier that adds the padding on the next line. Thinking about SwiftUI in terms of a tree, as long as you are familiar with that concept, can be very helpful when "thinking in SwiftUI." This idea is, admittedly, not mine and comes from the amazing book [*Thinking in SwiftUI* by objc.io](https://www.objc.io/books/thinking-in-swiftui/).

To display its content, SwiftUI divides the scene into however many children are within each view and adds default padding. A good way to visualize this is to draw some rectangles.

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Rectangle()
                .foregroundColor(.red)
            Rectangle()
                .foregroundColor(.green)
            Rectangle()
                .foregroundColor(.blue)
            Rectangle()
                .foregroundColor(.gray)
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

![image-20220116142650568](/Users/masoodkamandy/Desktop/_LAYER/_CurrentCoding/SwiftUI-Cheat-Sheet/images/RectangleExample.png)

In this example the `body` has **one child** which is **the `VStack`**. The `VStack` then has **4 children** which are the **`Rectangle`s**. These shapes are distributed evenly in a vertical fashion because we are inside a `VStack`.