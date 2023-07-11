---
title: "My split keyboard layout: A 60% Miryoku"
layout: post

series: ergonomics
series_suffix: " on <strong>budget ergonomics</strong>"
series_note: Coming up – how to build a split keyboard on a budget, and how to make do without one if you are on an even tighter one.
---

I have a soft spot for 40% keyboard layouts. However, Slovak uses 46[^digraphs] letters, compared to English's 26, so having them only on layers quite drastically reduces your typing speed. Thus I am stuck with a 60% board... but why not have the best of both worlds?

[^digraphs]: ...of which 3 are digraphs (ch, dz, dž), so I guess actually only 43, but how would you call them then? [Grapheme clusters](http://utf8everywhere.org/#characters)?

## The layout

I did quite a lot of experimenting with my own layouts, and when I encountered [Miryoku][miryoku], a 36-key layout, I was really impressed with its thought-through design. Its [principles][principles] were very similar to the things I derived from my own experiences, and it implemented them meticulously.

This is my 56-key version of Miryoku on the Sofle keyboard.

[![The layout](/assets/img/sofle-layout/reference.png)](http://www.keyboard-layout-editor.com/#/gists/8213f2479b8b08d5406ddc5c9c08c135)

## The core

The inside is a basically unmodified Miryoku (don't these tiny layouts look cute?).

![Miryoku on the inside](/assets/img/sofle-layout/miryoku.png)

Overall, I really like the layout. Here are my condensed thoughts on it.

Pros:

- Home row mods are awesome. They take some getting used to, but it is worth it. _chef's kiss_ so comfy
- The thumb cluster is great, I never realised how much I use these keys (especially backspace). They also play well well with alt- and ctrl-tabbing, even though it takes a week or two to start tapping them in the correct order
- Also, their dual layer-switching function is really neat; it makes them very powerful
- Colemak-DH will probably need a separate blog post, but any optimised layout is better than QWERTY so worth it
- The pinky button layer makes copy-pasting independent from the layout, which is great
- Easy to learn gradually
- Manages to pack in _all_ the keys, except for the numpad

Cons:

- The 200ms mod-tap delay is there. You stop feeling it a bit after a while but it still feels better without it
- It's especially annoying to use with mouse-heavy programs, like graphic design or 3D modelling, due to the 200ms delay on all modifiers. A lot of the time I still click to soon (as it's not a problem with key combinations). The tap layer helps, but there is not enough space on a 40% board for the modifiers. I will probably design a custom full-60% layer for that
- The layer-locking seems half-baked, most of the time you miss at least on key from other layers (e.g. on the number layer you do not have the `/` key)
- This is a double-edged sword, but since Miryoku is so efficient, there is no space for custom characters, (e.g. I would really like typographic unicode symbols somewhere. Maybe the top row? Or a tri-layer?)
- Also see the [bonus keys](#bonus-keys) section for some workarounds I had to implement

But overall, the best layout I tried so far. I do recommend reading the whole [reference manual][reference] to learn it more quickly.

## Number row

![The number row](/assets/img/sofle-layout/number-row.png)

I left it as-is, except for the outermost keys, which are too far away to be useful, and do not contain interesting keys for me anyway. If I need them, I can use them in the Miryoku layers.

I also included the Slovak legends here to give an idea just how important these keys are to me.

## Outer pinky columns

![The outer pinky columns](/assets/img/sofle-layout/outer-pinky-columns.png)

These were the interesting ones. Miryoku already includes an elegant and easy-to-remember solution on the number layer. The left and right columns contain all the leftover keys. The keys that already existed on the three main rows (`[`, `;` and `]`[^apostrophe]) have their positions unchanged. The three remaining keys are placed arbitrarily, but I found them comfortable to use.

[^apostrophe]: Note that Miryoku swaps the apostrophe and the semicolon

I returned the left column to its original place. The right column then went on the opposite side; this took some getting used to, but I quickly adapted and found it comfortable.

The only change I made was to swap the backtick (a semicolon on the Slovak layout) for a [caron dead key (`ˇ`)][caron], which is needed for some of the letters that do not fit, such as ď, or capital letters.

## Bonus keys

This leaves us with 4 remaining keys (discounting the two top corner keys, which I only include in my tap/gaming layer) and two encoders.

I just flung whatever I found personally useful there.

![The bonus keys](/assets/img/sofle-layout/bonus-keys.png)

- The bottom left key is for returning from the tap/gaming layer, as Miryoku [does not include a key][tap-exit] for that. This one is just hard to hit by accident
- The next key is the backtick, as GNOME uses it for the `` Alt+` `` same-app window switching shortcut. This is the single most annoying downside of switching to Miryoku, as I cannot figure out an elegant one-handed solution to it; this is my best workaround
- I use the analogous keys on the right side for arrows, as I am often lazy to use both hands for rewinding a video
- The encoders are my favourite part.
  - The left one is `PageUp` and `PageDown` by default, for quickly scrolling long documents. When pressed, it switches to edit mode, where it scrubs edit history instead (which is a bit awkward in Miryoku with one hand). Both of these are incredibly useful, especially one-handed
  - The right one is volume control, with play/pause on press. Along with the bottom arrow keys, this covers most of the media controls I need with just one half of the keyboard

I hope you found some of this information useful for designing your own layout.

[miryoku]: https://github.com/manna-harbour/miryoku
[principles]: https://github.com/manna-harbour/miryoku/tree/master/docs/reference#general-principles
[reference]: https://github.com/manna-harbour/miryoku/tree/master/docs/reference
[caron]: https://en.wikipedia.org/wiki/Caron
[tap-exit]: https://github.com/manna-harbour/miryoku/tree/master/docs/reference#additional-features
