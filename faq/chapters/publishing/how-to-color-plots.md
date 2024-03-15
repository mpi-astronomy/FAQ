# How to use color in scientific plots?

**[tl;dr]** Creating readable and accessible science plots is not rocket science, follow the simple rules below.

Color is a powerful tool in scientific visualization, aiding in the effective communication of complex data. When creating scientific figures, careful consideration of color choices is essential to ensure clarity, accessibility, and visual appeal. Here we provide a brief overview of the key principles of using color in scientific figures, emphasizing accessibility, meaningfulness, and best practices for effective data visualization.

### Best Practices:

• **Do not use rainbows**. Use a perceptually uniform colour map, such as viridis or cividis.

• Avoid red. Red does not appear as bright and vivid color. Especially avoid using red in combination with green or red symbols on a dark background. 

• Be mindful of existing norms associated with colors when selecting a color palette (e.g., colors of hot vs. cool stars). Ensure that your choices align with the intended message and audience of your visualization.

• If in doubt, go grey. Check if your figure can colors/symbols are still distingishable in greyscale. Or display greayscale images in addition to the color ones. 

• Pick a palette. Choose one that works for everyone. See some suggestions below.

• Do not use color as the sole encoding. Show difference BOTH in color and shapes/line textures to disambiguate colour.

• For graphs and line drawings, label elements of the graph on the graph itself rather than making a separate color-coded key, since matching same colors in distant places is extremely difficult.

• Test drive. Use a simulator such as Color Oracle or Coblis to ensure images can be interpreted accurately by everyone.

A number of tools and resources can make your life easier. Please consider consulting them next time when you are making science figures for a talk or a paper.

### Color Selection Tools:
1. **[Color Cycle Picker](https://colorcyclepicker.mpetroff.net)**: Utilize tools like the Color Cycle Picker to select color schemes that are colorblind-friendly and visually distinct.
2. **[ColorBrewer](https://colorbrewer2.org)**: Explore ColorBrewer, which offers a "colorblind safe" option for choosing appropriate color schemes.
3. **[Matplotlib Colormaps](https://matplotlib.org/cmocean/)**: At the very least use the viridis (now default) and cividis color maps. Consider using packages like [cmocean](https://matplotlib.org/cmocean/) and [colorcet](https://colorcet.holoviz.org/) for perceptually uniform colormaps in Python's Matplotlib library.
4. **[Color Blindness Simulator, Colibris](https://www.color-blindness.com/coblis-color-blindness-simulator/)**: Validate your color choices using tools like Coblis Color Blindness Simulator to ensure compatibility with different types of color vision deficiencies. Other available tools is [ColorOracle](https://colororacle.org/)(a standalone application that applies a filter to your screen). 

If you'd like to make your own digital workspace more accessible, consider using the [Solarized color palette](https://ethanschoonover.com/solarized/) developed by Ethan Schoonover. This color palette is available for many terminal emulators, text editors and IDEs. Morgan created his own Python implementations which can be found [here]( My python implementation: https://keeper.mpdl.mpg.de/f/0bc11f7fb56c43a088a0/).

If you'd like to dive deeper into the issue, this article on [Picking a Colour Scale for Scientific Graphics](https://betterfigures.org/2015/06/23/picking-a-colour-scale-for-scientific-graphics/) is a great starting point. 

By following these guidelines and leveraging the recommended tools, scientists can create figures that are not only visually engaging but also inclusive and informative for a diverse audience.

---

### Further resources:

- One of the seminal publications in the field is [Okabe & Ito (2002)](https://web.archive.org/web/20030821055411/http://jfly.iam.u-tokyo.ac.jp/color/text.html). 
- "Colour me better: fixing figures for colour blindness", [Katsnelson, Nature, 2021](ttps://www.nature.com/articles/d41586-021-02696-z): 
- A lengthy discussion on a [matplotlib issue](https://github.com/matplotlib/matplotlib/issues/9460) of color palettes
