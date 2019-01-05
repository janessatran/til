### Notes from Interactive Data Visualizations for the Web - An Introduction to Designing with D3 

## Scalable Vector Graphics 
### Styling SVG Elements
- SVG's default style is black fill with no stroke
- can apply properties inline or with a CSS style rule (set class = "style-rule-name")
  - CSS approach benefits:
    - can specify a style once and have it applied to multiple elements
    - CSS code is easier to read than inline attributes
    - more maintainable/design changes are faster to implement
    
### Common SVG properties:
- **fill**: a color value
- **stroke**: a color value
- **stroke-wdith**: a numeric measurement (typically in pixels)
- **opacity**: a numeric value between 0.0 (completely transparent) and 1.0 (completely opaque)

### Layering and Drawing Order
- no "layers" in SVG -> shapes are arranged within 2D plane
- order in which elements are coded determines their depth order 
