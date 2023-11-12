# Creating an Accessible Reading Experience

<br/>

#

## Reading Content Protocol

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled.png)

- Let's see how VoiceOver interacts with the sample app. VoiceOver on.
- As I drag my finger across the screen, VoiceOver plays a sound effect indicating there is no content to be found.
- Therefore, the first thing we need to do is make our text content accessible.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%201.png)

- To make your content accessible, you should use the `UIAccessibilityReadingContent` Protocol. This protocol consists of 4 core methods.
- `AccessibilityLineNumber(for point:)` asks you to return the line number for a given touch location
- `AccessibilityContent (forLineNumber and accessibilityFrame (forLineNumber` asks for the text content and rect for a given line respectively.
- Finally, `accessibilityPageContent` asks you to return the entire pages worth of content.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%202.png)

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%203.png)

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%204.png)

- The first thing we need to do is make our page view an accessibility element. We do this by setting isAccessibilityElement to true in the page views initializer.
- Next, we begin to implement the reading content protocol. Our first method is `accessibilityLineNumber(for` point.
- First, we hitTest the page view using the past in line number.
- If the resulting view is one of our known sub views, we map that to the value of our layout enum. Finally, we return the rawValue as this is the representation VoiceOver understands.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%205.png)

- The implementation of `accessibilityFrame (forLineNumber` is very similar. We begin by creating a new instance of the layout enum with our given raw value.
- We switch over the possible cases and map that to one of our known sub views. Finally, we return accessibility frame, which represents the rect for a given line.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%206.png)

- Finally, to implement accessibilityPageContent we gather together the text from our known sub views and return them as a single string.

<br/>

#

## Automatic Page Turning

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%207.png)

- Next let's talk about automatic page turning. When VoiceOver's read all command is invoked, it's expected that VoiceOver will be able to read all of your content from beginning to end.
- This may require VoiceOver to turn pages in your app. To implement automatic page turning you need to adopt 2 accessibility APIs.
- First, you should include the causesPageTurn accessibility trait on your page view.
- Second, you should implement AccessibilityScroll in direction. This gives VoiceOver the ability to turn pages in your app.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%208.png)

- Let's see how we would implement automatic page turning in our sample app.
- First, we need to include the causesPageTurn accessibility trait. We do this by setting accessibility trait in the page views initializer.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%209.png)

- Next, we implement accessibilityScroll and direction.
- We do this by switching over the possible cases of the direction parameter.
- If the direction is previous or left, we ask our delegate to turn to the previous page. If that's successful, we notify VoiceOver with a pageScrolled notification.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%2010.png)

- Similarly, if the value is right or next, we ask the delegate to turn to the next page and if that's successful, we notify VoiceOver with a pageScrolled notification.

<br/>

#

## Customizing Speech

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%2011.png)

- You may want to control the way VoiceOver speaks your app's content.
- To do this you can use 2 alternate methods in the reading content protocol.
- These method versions return NSAttributedStrings instead of simple strings.
- By supplying the appropriate accessibility attributes, you can control various aspects about how VoiceOver speaks your content.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%2012.png)

- For example, you may have a passage you would like spoken in a particular language.
- To do this you can include the accessibilitySpeechLanguage attribute along with the appropriate language identifier.
- This causes VoiceOver to use the most appropriate voice to speak your content. Arc de Triomphe.

<br/>

![Untitled](Creating%20an%20Accessible%20Reading%20Experience%20e6b89626f0aa4786a7bd1bd1d4ff008c/Untitled%2013.png)

- Furthermore, you may want fine-grained control over the way VoiceOver speaks your content.
- To do this you can supply the IPA representation for your passage along with the accessibilitySpeechIPANotation attribute.

<br/>

- So to create a great reading experience for VoiceOver, you first need to make your text content accessible. You do this by implementing the UIAccessibilityReadingContent protocol.
- Next, you should implement automatic page turning so VoiceOver can read all of the content in your app from beginning to end.
- Finally, to control the way VoiceOver speaks your content, you should consider using the NS attributed strings versions of the methods in the reading content protocol and supply the appropriate accessibility attributes.