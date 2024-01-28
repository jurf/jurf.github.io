---
title: How to implement a bilingual QMK layout for programming (with EurKEY)
layout: post
series: layouts
series_suffix: " on <strong>keyboard layouts</strong>"
---

I frequently write in two different languages -- Slovak and English. The Slovak layout is fine for day-to-day use, but for programming, the English (US) layout is much more ergonomic.

Another problem is that you have to use Shift to access numbers in the number row, which tends to break the design of smaller layouts, while also requiring you to build up twice as much muscle memory, which is very confusing.

Not long after writing my [first blog post]({% post_url 2023-07-11-60-percent-miryoku %}) on my layout, I concluded that I had had enough and decided to make a hybrid EN/SK layout.

I use the base Miryoku layout and use the outer keys for the accented versions. This guide summarises how to make them work while keeping the core Miryoku intact.

[![reference](/assets/img/sofle-layout/reference.svg)][figma]

## Architecture

There are three options I considered:
 1. Use the Slovak layout and add overrides for the symbols
 2. Type all the Slovak keys with Unicode input methods
 3. Use an international layout to implement the Slovak letters

All three have their pros and cons. Using the Slovak layout meant that I could use QMK's existing [language-specific keycodes][keymap-extra], but I would have to override all of the 21 shifted symbols.
 
I also wanted to implement Shift making capital versions of the Slovak keys, which would add another 12 overrides.

That sounded tedious and a waste of firmware space.

Using the Unicode input option would be just slightly annoying when typing (due to the delay and flash of characters) but much simpler (just 12 overrides). However, I wanted it to be cross-platform without having to install any programs.

So I explored using international layouts. My first thought was the US International layout, but the version in Linux did not have the dead keys I needed.

I then stumbled upon the [EurKEY][eurkey] layout. It was cross-platform, pre-installed in Linux and supported many of the keys I needed. It also supported adding Shift to make capital versions of the characters, unlike the Slovak layout! That meant no need for overrides.

However, about half of the characters needed to be typed with a dead key. It has a smaller delay and flash than the Unicode option, but it turned out a bit tricky to implement correctly.

## Implementation

If your language only uses keys already present in the layout, the implementation is dead simple. Create macros for all the keys you need.

```c
#define EU_YACU ALGR(KC_R)   // ý
#define EU_AACU ALGR(KC_X)   // á
#define EU_IACU ALGR(KC_B)   // í
#define EU_EACU ALGR(KC_G)   // é
#define EU_UACU ALGR(KC_J)   // ú
#define EU_OACU ALGR(KC_DOT) // ó
#define EU_ADIA ALGR(KC_A)   // ä
```

You can immediately start using these in your keymap.

For full functionality, you only need to deal with some nuances, like [configuring Caps Work](https://docs.qmk.fm/#/feature_caps_word?id=configure-which-keys-are-word-breaking) to not consider them word breaking, or adding them to the Auto Shift configuration[^autoshift] if you use it.

[^autoshift]: Unfortunately I did not manage to implement it for the dead key characters. It is not a big deal to me but if you figure it out, send me an email and I'll add it here

The dead keys are a bit more involved. For each one, you need to define a custom keycode. Then, during handling, you need to:

1. Remove any Shift modifiers[^delmods]
2. Type out the sequence needed to type the dead key (e.g. using macros)
3. Add back the modifiers
4. Check if Caps Word is on and manually add a weak Shift if yes
5. Type out the base character

[^delmods]: This is only necessary if you want Shift to make a capital letter

Check my QMK fork for a [reference implementation][keymap_eurkey.c].

## Mod-Taps

An unfortunate reality is that Mod-Taps [do not support][modtap-caveat] 16-bit keycodes. This affects both regular (as they are accessed with modifiers) and dead key characters.

I recommend refactoring the functionality into three functions.

1. Dead key implementation
2. Override of the tap functionality of regular keys
    - Note that this will also need manual application of Caps Word
3. Override of the tap functionality of dead keys

Then your `process_record_user` can look like this:

```c
switch (keycode) {
    case EU_OCIR ... EU_ZCAR:
        return process_deadkey(keycode, record);

    // Mod-taps do not support 16-bit keys; manually set the keycode
    case SFT_T(EU_OACU):
        return process_modtap(EU_OACU, record);
    case GUI_T(EU_OCIR):
        return process_modtap_deadkey(EU_OCIR, record);
    case SFT_T(EU_NCAR):
        return process_modtap_deadkey(EU_NCAR, record);

    default:
        return true;
}
```

[figma]: https://www.figma.com/file/Ty5GlR07527IqVRcMPnfTQ/P%C3%B4vab-Layout?type=design&node-id=0%3A1&mode=design&t=L4o97CRDY0nQGUmc-1
[keymap-extra]: https://docs.qmk.fm/#/reference_keymap_extras?id=header-files
[eurkey]: https://eurkey.steffen.bruentjen.eu/
[caps-word]: https://docs.qmk.fm/#/feature_caps_word?id=configure-which-keys-are-word-breaking
[keymap_eurkey.c]: https://github.com/jurf/qmk_firmware/blob/master/keyboards/sofle/keymaps/jurf/keymap_extras/keymap_eurkey.c
[modtap-caveat]: https://github.com/qmk/qmk_firmware/blob/master/docs/mod_tap.md#caveats