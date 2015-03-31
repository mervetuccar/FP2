# Final Project Assignment 2: Explore One More! (FP2) 
DUE March 30, 2015 Monday (2015-03-30)


### My Library: Racket Graphical Interface Toolkit, racket/gui/base
Write what you did!
Remember that this report must include:
 
* a narrative of what you did:
<br />
In this library exploration assignment, I played around GUI library. I tried creating windows; buttons, canvas, dialog, panel, message boxes, checkboxes and etc. I didn’t create something that makes sense as whole but instead tried the run the little code pieces given in the documentation, and modified their data (labels etc.) mostly. I really enjoyed playing with GUI library, and am considering to use it in the final project.
* the code that you wrote
```
#lang racket/gui
(require racket/gui/base)

(define frame (new frame% [label "Merve"]))
(send frame show #t)
(define msg (new message% [parent frame]
                          [label "Hello! This is FP2!"]))

(new button% [parent frame]
              [label "Click me"]
              [callback (lambda (button event)
                          (send msg set-label "Tadaaaa"))])

(send frame show #t)

(define my-canvas%
  (class canvas% 
    (define/override (on-event event)
      (send msg set-label "Canvas mouse"))
    (define/override (on-char event)
      (send msg set-label "Canvas keyboard"))
    (super-new)))
(new my-canvas% [parent frame])

(new button% [parent frame]
             [label "Pause"]
             [callback (lambda (button event) (sleep 5))])

(define panel (new horizontal-panel% [parent frame]))
(new button% [parent panel]
             [label "Left"]
             [callback (lambda (button event)
                         (send msg set-label "Left click!"))])
(new button% [parent panel]
             [label "Right"]
             [callback (lambda (button event)
                         (send msg set-label "Right click!"))])

(define frame2 (new frame%
                   [label "Example"]
                   [width 400]
                   [height 400]))
(new canvas% [parent frame2]
             [paint-callback
              (lambda (canvas dc)
                (send dc set-scale 3 3)
                (send dc set-text-foreground "blue")
                (send dc draw-text "This is Frame2!" 0 0))])
(send frame2 show #t)


; Create a dialog
(define dialog (instantiate dialog% ("First Dialog Box")))
 
(new text-field% [parent dialog] [label "Your name"])
 
(define panel2 (new horizontal-panel% [parent dialog]
                                     [alignment '(center center)]))
 
(new button% [parent panel2] [label "Cancel"])
(new button% [parent panel2] [label "Ok"])
(when (system-position-ok-before-cancel?)
  (send panel2 change-children reverse))
 
(send dialog show #t)

(define check-box (new check-box%
                       (parent panel)
                       (label "New Check Box")
                       (value #t)))

(define choice (new choice%
                    (label "Choice")
                    (parent panel)
                    (choices (list "Item 0" "Item 1" "Item 2"))))


(define tab-panel (new tab-panel%
                       (parent panel)
                       (choices (list "Tab 0"
                                      "Tab 1"
                                      "Tab 2"))))

```
* output from your code demonstrating what it produced
<br />
Sample picture of output: [output1](http://imgur.com/lD8Ac0Y)
<br />
Another sample picture: [output2](http://imgur.com/Zv8w5xr)


The narrative itself should be no longer than 350 words. Yes, you can add more files and link or refer to them. This is github, handling files is awesome and easy!

Ask questions publicly in the Piazza group.

### How to Do and Submit this assignment

1. To start, [**fork** this repository][forking].
1. Modify the README.md file and [**commit**][ref-commit] changes to complete your solution.
  2. (This assignment is just one README.md file, so you can edit it right in github without cloning)
  3. (You may need to clone and push if you want to add extra files)
1. [Create a **pull request**][pull-request] on the original repository to turn in the assignment.

<!-- Links -->
[piazza]: https://piazza.com/class/i55is8xqqwhmr?cid=411
[schedule]: https://piazza.com/class/i55is8xqqwhmr?cid=453
[markdown]: https://help.github.com/articles/markdown-basics/
[forking]: https://guides.github.com/activities/forking/
[ref-clone]: http://gitref.org/creating/#clone
[ref-commit]: http://gitref.org/basic/#commit
[ref-push]: http://gitref.org/remotes/#push
[pull-request]: https://help.github.com/articles/creating-a-pull-request

