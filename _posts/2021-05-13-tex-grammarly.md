---
title: Using Grammarly with TeX
layout: post
---

Currently, there is no easy way to utilise Grammarly with TeX. I encountered this problem while writing my bachelor’s thesis, but luckily, there is a way to work this around. I got several requests to document it, hence the blog post.

Several [attempts][overleaf-hacks] integrate Grammarly into Overleaf, but they all deviate from how the platform is meant to be used and are slightly cumbersome.

If you can settle for an offline setup -- which I can wholly recommend -- there is a more ergonomic solution. It involves a combination of three tools:

- [Visual Studio Code][vscode]
- the TeX [markdown package][tex-markdown]
- the VSCode unofficial [Grammarly extension][vscode-grammarly]

Since VSCode is very extensible, the exact details of your workflow may differ. I can recommend the [Markdown All in One][vscode-markdown] extension, which eases working with Markdown files quite a bit. I use its preview to check for Markdown errors before having to deal with TeX. I’ve also had varying levels of success with the [markdownlint][vscode-markdown-lint] extension to help keep my Markdown files clean.

You can stop here and already get several good use-cases -- for example, the way this workflow clicked into the way I write blog posts was an unexpected but welcome bonus.

I cannot comment on the usage with LaTeX, but I have heard good things about the [LaTeX Workshop][vscode-latex] extension (the numbers speak for themselves).

ConTeXt support in VSCode is finicky, but so is ConTeXt support everywhere else, so it is good enough. I use the [ConTeXt Syntax][vscode-context] extension with custom build tasks and problem matchers, but that is the subject of a future blog post.

To integrate the markdown you produced into your TeX document, you will have to dive into the [documentation][tex-markdown-docs] of the TeX markdown package, as its feature set is quite extensive. It has support for probably everything you will need, like citations, footnotes, figures, and you can also enable hybrid mode to mix in TeX syntax, such as math. Big shoutout to (our very own) Vít Novotný, as his work does most of the heavy lifting in this setup.

Although few rough edges need honing -- e.g. the support for alt-text in images (used in the markdown package to display figures with annotations) triggers a Grammarly error if you use it to check curly quotation marks -- but the overall functionality is highly usable.

A final thing to note is how the Grammarly editing process perfectly fits into the VSCode user experience -- `Ctrl+.` to apply and `F8`/`Shift+F8` to jump arround issues is _such a nicer way_ to edit documents than the default Grammarly clicky experience.

[vscode]: https://code.visualstudio.com/
[overleaf-hacks]: https://tex.stackexchange.com/questions/333947/integrating-grammarly-with-online-latex-editors-such-as-overleaf
[tex-markdown]: https://github.com/Witiko/markdown/
[vscode-grammarly]: https://marketplace.visualstudio.com/items?itemName=znck.grammarly
[latex-workshop]: https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop
[vscode-markdown]: https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
[vscode-markdown-lint]: https://thisdavej.com/build-an-amazing-markdown-editor-using-visual-studio-code-and-pandoc/
[vscode-latex]: https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop
[vscode-context]: https://marketplace.visualstudio.com/items?itemName=JulianGmp.context-syntax
[tex-markdown-docs]: https://github.com/Witiko/markdown/#further-information
