### Why You Should Use CoffeeScript

JavaScript (JS) is the programming language that allows web developers to make web pages interactive. Each browser has a slightly different implementation, which developers iron out by using cross-browser frameworks such as JQuery. It doesn't matter if the server side component is written in PHP or Ruby - the front end is always JavaScript. Thanks to Google's V8 JavaScript engine and Node.js, JS is also becoming the goto language for realtime interactive web applications such as chat, live blogs. JS is the language behind most everything the end user perceives as cool in the UI.

JS has been around since the late 1990s. Like a house with several owners with different tastes, it's been added on to over the years. It's really easy to write ugly JS, chock full of bugs, that no other developer will ever want to or be able to read. You can accidentally open memory leaks that crash the browser. You can accidentally put a variable in the global namespace and cause the rest of the program to come to a crashing halt, or behave mysteriously.

At the same time, the core of JS is a beautiful language that, if you stick to the "good parts," can support the richest of rich client apps with grace and aplomb. That is where CoffeeScript comes in. 

CoffeeScript (CS) is a language that compiles into JavaScript. It makes it easier and less tedious to do good things with JS, and harder to do bad things. Because CS only turns into JS when the i's are dotted and the t's are crossed, it is harder to write buggy JS.

## Line Noise Reduction

Programming languages based on C or Java, such as JS and PHP, are filled with parentheses and semicolons to tell the computer where each block of code starts and ends. Keywords such as "var" and "function" tell the computer which are variables and which are functions. The programmer's eye gets used to them, and may even come to rely on them to interpret code on the screen.

Oftentimes before I write a paper I begin with an outline. Top level items are on the left, and each layer of subitem gets one level of indentation. My word processor responds when I press the TAB key, and has an indent button. There is no facility to write an outline like the following, nor is there a word processing facility for doing so outside of a code editor:

I. The Industrial Revolution {
    A. Origins {
        i. deforestation in 17th century England
        ii. proximity of coal and iron deposits
        iii. accumulation of capital from overseas trade
    }
}

Therefore if you want to make code more human readable, replace the braces with indentation, and let the compiler put them back in for you to make the computer happy. CS does this, calling it "syntactic whitespace":

<code>
class App
    ...
    initUI: ->
        if $('#controls').size() is 0
            $('#title').append render('searchControls')
            JKT.earth.addControls() if (JKT.earth)
        ...
</code>

becomes:

App = (function() {
    function App() {
        ...
    }
    App.prototype.initUI = function() {
      if ($('#controls').size() === 0) {
        $('#title').append(render('searchControls'));
        if (JKT.earth) {
          JKT.earth.addControls();
        }
      }
    return App;
});

I personally find the CS more meaningful, and the compiled code to be cleaner than the code I would have written to do the same thing (although it's not fashionable to admit that your code isn't always the cleanest and most awesome code anyone has ever written).

Notice that the -> stands for "function", and function name colon: means "add this function to the object prototype." Please read the CS documentation a few times before you try CS - this is just the beginning of the stuff you can do.

The bottom line is that "line noise reduction" removes as much computer-oriented meaning as possible from the code, while leaving the human-oriented meaning. The principle is that while programmers write code for computers to run, unless it's one-time only throwaway code, they're also writing code for other programmers (including themselves when they come back to it three months later to add a new feature). The less time it takes a programmer to figure out what is going on, the higher the business value.

## Meaningful Code is Cleaner Code

The code snippet above isn't necessarily fair, because it doesn't show JS "before I started writing CS." I see that it has benefited from the other thing I most like about CS: to make it easier to debug, you have to break it down into smaller parts. Smaller parts that do one thing only are cleaner parts.

That's right. In the old regime, I might have a JS file with several hundred lines. When a error pops up, Firebug will tell me what line it's on, and I can jump to it in the code editor and fix it. Maybe right there I will add some more code, and pretty soon I'll have a large JS file that is hard to edit without Firebug, with lots of interconnected parts and mixed behaviors.

Since CS makes working with the JS object model so easy, I find myself using it. I would take that 500 line JS file and break it into a half dozen or more constituent parts. I have development mode set to deliver these to the browser individually, so if an error crops up, it's easier for me to find it in the CS. Production mode combines and minifies the JS into one file for speed of delivery to the user. 

If you're coming from Ruby or Python, you'll recognize the philosophy of human oriented code. You'll also recognize that CS is 2/3 Python and 1/3 Ruby. Therefore CS will be easier for you if you know one of those; likewise if you hate Ruby, stay away from CS. (And if you don't know JS yet, don't try CS...)

## Gotchas

I must admit that CS came with some pounding of my head on the table, especially when I started. Here's where I got stuck, and what I did to get unstuck:

1. I started by opening a JS file and "saving as" a coffee file. DON'T DO THAT! Create a new coffee file, copy the JS from the JS file, and paste it into the coffee file. The paste action will get the indentation right.

2. Your code may look indented to you, but it may not be so for coffee. You may have SPACES mixed in with your TABS. 

When you make changes to coffee but nothing seems to happen in the browser:

1. First check that you are running the compiler. I have a shell script that starts coffee's compile-on-edit mode. Sometimes I forget to run it. By the third alert statement, I check for that.

2. Second, check the compiler output. You may have a syntax error in CS. It won't compile at all if there's a problem with the CS. If you see "cannot use a pure statement in an expression", it usually means there's a rogue space in your tab indentation. Redo the indentation and try again.

3. Third, if the CS compiled but weird things are happening such as it says a function doesn't exist when you know it does, check the compiled JS. Sometimes there is an indentation issue that doesn't break the compiler, but causes it to misinterpret where classes end and begin.

## In a perfect world

CS is new. Therefore it is not integrated into most IDEs yet. Since Rails 3.1 uses CoffeeScript, it shouldn't be long before you see CS support in Aptana. There is an IntelliJ plugin for RubyMine and PHPStorm. I use the TextMate bundle. My colleague Jim uses Eclipse and edits it with plain text, as he finds it still easier to read than JS.

## Getting started

I recommend going to the CS website (http://jashkenas.github.com/coffee-script/). Read it a few times before you do anything. Bookmark it. Then install node, npm, and coffee. 

When I started on CS, I had a few thousand lines of JS already written. Most of it was for a prototype, and I dreaded having to whip it into production grade and add the rest of the features to it. I started learning CS by porting some of the easier JS files. When I was comfortable, I took on the hairy part. It emerged as a piece of code I'm proud of and like to work with. 

In a nutshell, CoffeeScript makes it fun for me to write clean JavaScript, and delivers business value by helping me to write maintainable JavaScript faster that it otherwise would. If you're not using it yet, it's time to start.

## References
1. The CoffeeScript web page: http://jashkenas.github.com/coffee-script/
2. My presentation to the Ithaca Web Group: http://www.slideshare.net/davidfurber/real-lifecoffeescript
3. Tongue in cheek presentation of why you'll hate CS: http://www.slideshare.net/tim.lossen.de/coffeescript-7-reasons-you-are-gonna-hate-it
