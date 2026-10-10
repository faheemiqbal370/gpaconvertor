# GPA and CGPA Converter

A small web tool that converts a GPA or CGPA from one grading scale to another.

**Live site:** https://faheemiqbal370.github.io/gpaconvertor/

## What it does

Enter a grade, choose the scale it is on, choose the scale you need, and get the converted value. The result shows the formula with your numbers and a two-line ruler that marks your grade at the same relative position on both scales.

Supported scales:

| Scale | Typical use |
|-------|-------------|
| 4.0   | US colleges |
| 4.33  | Schools that count A+ as 4.33 |
| 5.0   | Public universities, some weighted school GPAs |
| 7.0   | Universities with a 7-point system |
| 10.0  | Most Indian universities |

Other behaviour:

- Checks the input and says what is wrong: empty value, negative value, a grade above the top of the chosen scale, or the same scale chosen twice.
- The swap button reverses the scales. If a result is showing, the converted grade becomes the new input, so 3.40 / 4.0 swaps to 8.50 / 10.
- Works on phones, supports keyboard use (Enter converts), and respects the reduced-motion setting.

## How the conversion works

The tool keeps your grade at the same proportional position on the new scale:

```
converted = (grade ÷ original maximum) × new maximum
```

Example: 8.5 on a 10.0 scale → (8.5 ÷ 10) × 4.0 = 3.40 on a 4.0 scale.

Values are rounded to two decimal places for display only. The calculation uses the unrounded numbers.

## Limitations

The result is a proportional estimate. It is not an official conversion.

- **Universities and evaluators use their own rules.** Credential services such as WES convert course by course using institution-specific tables, and they do not publish a single formula. Admissions offices often read your original transcript directly.
- **Some scales are not proportional.** On the standard Saudi 5.0 and 4.0 scales, each letter grade differs by exactly 1.00 point (A+ is 5.00 and 4.00, A is 4.75 and 3.75, and so on). A 4.0 out of 5.0 therefore equals 3.0 on the 4.0 scale, but this tool gives 3.2.
- **CGPA to percentage is not covered.** Percentage rules differ by institution. IUST, for example, uses `percentage = 10 × CGPA`, while CBSE uses `9.5 × CGPA`. Use the formula your own institution publishes.

Always confirm the method with the institution you are applying to.

## Run it locally

No build step or dependencies. Clone the repository and open `index.html` in a browser.

```bash
git clone https://github.com/faheemiqbal370/gpaconvertor.git
cd gpaconvertor
# open index.html in your browser
```

An internet connection is only needed to load the fonts from Google Fonts. Without it, the page falls back to system fonts and works the same.

## Project structure

```
index.html   Page structure and content
style.css    Styles, colour tokens and responsive layout
app.js       Validation, conversion, ruler and swap logic
```

## Adding a scale

1. Add an `<option>` with the scale's maximum as its value to both the `from-scale` and `to-scale` selects in `index.html`.
2. Add a row for it in the "Supported scales" table in `index.html`.

`app.js` reads the maximum from the selected value, so no code changes are needed.

## Built with

HTML, CSS and vanilla JavaScript. Fonts: Literata and Public Sans.