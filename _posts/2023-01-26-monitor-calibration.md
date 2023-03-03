---
title: "How to get the most out of your monitor without any equipment"
layout: post
last_modified_at: 2023-03-03
---

For years I have been trying to get a truly neutral image out of my monitors, which is rather difficult due to the sheer amount of [desirable nonsense][desirable-nonsense] monitor firmware tends to include. I also do not own a colourimeter, without which objective improvements were hard to obtain.

So here is my current boiled-down ritual I go through with any monitor I have to work with, in roughly the order of importance.

0. **Get a [monitor stand]({% post_url 2022-11-02-budget-ergonomics-workspace-life %}#stell-sos-1010-monitor-stand)** or at least a stack of books. There is no use in tweaking the monitor if you can't use it like a human.

1. **Get a digital cable**. With old monitors and an abundance of VGA cables (like I had), one can be tempted to just use analogue. However, analogue cables suffer from [signal degradation][signal-degradation][^vga]. Digital cables also do not need image adjustment to work.

   If you can, use DisplayPort (preferred -- open standard, desktop-focused), HDMI or DVI‑D. If your monitor does not have a digital port, prefer thicker and shorter cables.

   If you use HDMI, **use the full range of RGB**. I was once working on a monitor that should have been good but had absolutely no detail in the blacks. I found out that it was set to [limited RGB][limited-rgb], which is a mode used mainly by televisions that limits the detail in shadows and highlights. If your input and output settings are mismatched, you will drastically reduce your image quality. For desktop, you always want full.

2. **Switch the picture mode to 'user'** (or at least 'standard'). A mode that lets you set up as much as possible is preferred, as 'standard' modes sometimes tend to have unadjustable settings, such as tint compensations. Disable any dynamic contrast or colour enhancements. Sometimes it's good to start with a reset, depending on the previous owner.

3. **Remove software sharpening**. The [Lagom LCD test pages][lagom-sharpness] have a great test image for this. On analogue, you will probably never get a _truly_ neutral image (the setting is actually there for compensating sharpness loss). On digital, you should be able to get a completely flat grey image that you do not have to squint hard at for it to be completely uniform. Neutral typically means '50'[^luck].

4. **Set [gamma][gamma] to sRGB** (and neutralise contrast changes). The contrast setting affects the gamma, but AFAIK, there is no clear test for it. Try the [Lagom contrast test page][lagom-contrast] for a quick adjustment. Keep in mind that some monitors are just plain bad and are not capable of differentiating colours at the extremities. If the numerical middle does not yield a neutral image, go for neutral-ish.

   Gamma is better, however. There is a [separate test][lagom-gamma] on Lagom, but I prefer the sharpness test; it just seems a little easier to see. To properly reproduce sRGB images (i.e. images on the web), the gamma should be set to roughly 2.2. If your monitor has an sRGB setting, use that, otherwise, use whatever produces the best results.

   Some monitors do not have a setting equivalent to sRGB. If that is the case, you can emulate it in the OS. You can either use the Windows display calibration tool (you can leave the rest of the settings at default) or your drivers. I am not aware of any simple way of doing this in Linux; if you do, please contact me. However, I did not have good experience with this.

5. **Remove colour casts**. Most monitors I have come across have some sort of colour tint when completely neutral. Manufacturers compensate for this with default settings. However, unfortunately, these default settings are not necessarily neutral. They can be either warmer or colder by default, moreover, LCDs tend to yellow over time, so if your monitor is not new, these default settings (and also any sRGB profiles if present) are basically useless.

   Fortunately, you can calibrate this pretty well yourself with just a [sheet of white paper][paper-callibration]. Since we are trying to recreate the D65 white point which was created to best represent [average midday light][d65], let some sunlight in (just not directly on your screen and paper), open a completely white screen (i.e. the Eizo [defective pixel][eizo-test] test) and try to match the paper colour by **lowering** the individual RGB channels[^colours].

6. **Tweak overdrive**. Overdrive (or [response time compensation][overdrive]) is a technique for improving the speed at which LCD pixels change colour by initially increasing voltage, which improves the response times of screens (sometimes by quite a bit). You'll see it under many different names, as manufacturers tried to avoid paying royalty fees to the patent holder in the past.

   It works similarly to how you would put a pan on high heat at the start to make it reach the target temperature more quickly. If you are not careful, you will miss the target temperature and go higher than you want. Similarly, in screens this creates [artifacts][overdrive-artifacts] ('coronas'), so you may want to tweak the parameters to reach a balance. You can use the [ghosting test][ghosting-test] on Blur Busters.

   Some monitors include a light strobing mode (or they insert black frames) which lowers blurs down to a minimum, but I would probably recommend against this unless you do competitive gaming, as flickering lights (commonly experienced as PWM for controlling brightness on screens) have been [linked][pwm] to eye strain and headaches. If you have a flicker-free backlight, this negates its advantages.

7. **Turn on the night light feature and auto-dark mode** in your OS. You need good eyes to see your properly-setup monitor! Night filters are standard nowadays. For auto dark modes, there is [Windows Auto Dark Mode][win-auto-dark] or the [Night Theme Switcher][night-theme-switcher] extension for GNOME.

I hope you found this guide useful.

Of course, if you are a professional and need truly accurate colour reproduction, then you will need to do a calibration with a colourimeter.

And now that you have an accurate, neutral image, why not try [accurate, neutral sound][autoeq] as well?

---

[^vga]: I was really surprised at how big the difference in sharpness was when I switched.
[^luck]: If you are lucky. Sometimes neutral is '5' or '0', but in the end, you will have to use your own judgment. On my old Samsung monitor, the neutral for contrast and sharpness is somewhere around 60.
[^colours]:
    Some argue that this should only be done if you _need_ this for your work (i.e. you do photography, graphic design or video editing), but for casual use cases, you should use the full range of colours, so that movies and games are more vibrant.

    I do not necessarily agree. I think colour casts generally do not look good and degrade your experience, especially if you have a dual monitor setup or you use the screen during the day. Even manufacturers prefer compensation (and thus limiting the colour vibrancy) to a colour cast. Do you want every movie you watch to be yellow or green?

    However, if you have a really bad (or old) monitor, doing this calibration will leave you with very bland colours. In that case, I would only compensate slightly (i.e. not going below 40 if 50 is neutral), or just simply roll with it. Might as well see at least some colours!

[desirable-nonsense]: https://www.youtube.com/watch?v=B_8HDPBfvHI
[signal-degradation]: https://youtu.be/f38sotYHqtA?t=33
[limited-rgb]: https://www.benq.com/en-us/knowledge-center/knowledge/full-rgb-vs-limited-rgb-is-there-a-difference.html
[lagom-sharpness]: http://www.lagom.nl/lcd-test/sharpness.php
[gamma]: https://en.wikipedia.org/wiki/Gamma_correction
[lagom-contrast]: http://www.lagom.nl/lcd-test/contrast.php
[lagom-gamma]: http://www.lagom.nl/lcd-test/gamma_calibration.php
[paper-callibration]: https://youtube.com/watch?v=avJTz1JhkR4&t=70
[d65]: https://en.wikipedia.org/wiki/Illuminant_D65
[eizo-test]: https://www.eizo.be/monitor-test/
[overdrive]: https://en.wikipedia.org/wiki/Response_Time_Compensation
[overdrive-artifacts]: https://blurbusters.com/faq/lcd-overdrive-artifacts
[ghosting-test]: https://www.testufo.com/ghosting
[pwm]: https://tftcentral.co.uk/articles/pulse_width_modulation
[win-auto-dark]: https://github.com/AutoDarkMode/Windows-Auto-Night-Mode
[night-theme-switcher]: https://extensions.gnome.org/extension/2236/night-theme-switcher/
[autoeq]: https://medium.com/@jaakkopasanen/make-your-headphones-sound-supreme-1cbd567832a9
