# Procedure for making *Bootstrap-like* SCSS grid system

## 0. Requirements
1.  Node JS (accompanied with NPM)
2.  SCSS

	`@import "sass:math"`
	
	`@import "sass:map"`
	
3. Before starting to work, please decide which sort of responsive you are going to do: `desktop first`, or `mobile first` ?

## 1. Initialize variables, breakpoints, gutter and ratio.
> For `mobile first`, please use `min-width`

> For `desktop first`, please use `max-width` and re-arrange the index of list

### a. for Mobile first
```scss
$grid-breakpoints: (
    xs: 0,
    sm: 576px,
    md: 768px,
    lg: 992px,
    xl: 1200px,
    xxl: 1400px,
);
$container-max-widths: (
    sm: 540px,
    md: 720px,
    lg: 960px,
    xl: 1140px,
    xxl: 1320px,
);
```
### b. for Desktop first 
```scss
$grid-breakpoints: (
    xxl: 1400px,
    xl: 1200px,
    lg: 992px,
    md: 768px,
    sm: 576px,
    xs: 0
);
$container-max-widths: (
    sm: 100%,
    md: 540px,
    lg: 720px,
    xl: 960px,
    xxl: 1170px,
);
```
### c. Gutters and ratios
```scss
$grid-columns: 12;
$grid-gutter-width: 30px;
$gutters: (
    0: 0,
    1: 0.25,
    2: 0.5,
    3: 1,
    4: 1.5,
    5: 3,
);
```

## 2. Create `.container` and `.container-fluid`
**Requirement**
1. Their margin have to be set to center
2. Include the `padding-left` and `padding-right` by half of the gutter
3. Set limits as indicated in breakpoint map
4. Indicate default gutter for both x and y as CSS variables. Do not uses SCSS variables to set the gutters

## 3. Create components
### a. Default rows and columns
Create `.row` and `.col` settings. Please check the following requirements
#### `.row`
- Make sure each child of the `.row` are added with gutters

------------
#### `.col`
- Keep all settings to defauts by using `> *`. 
- Do not set flex-basis

### b. Fixed rows and columns
#### `.row-cols-{breakpoint}-{number}`
- Formula: ```100%  /  {num}```
- Default list is from 1 to 6
#### `.col-{breakpoint}-{number}`
- Formula: ```100%  / 12 (by default) * {num}```
- Default list is from 1 to 12

## 4. Create offset
- Classname: ```.offset-{breakpoint}-{number}```
- Use `margin-left` of columns
- Formula: ```100%  / 12 (by default) * {num}```
- Default list is from 0 to 11

## 5. Create gutter

> Usually the `--offset-y` 's default value is 0

> Use the `$grid-gutter-width` the default value

- Classname: ```.g-{breakpoint}-{number}```, ```.gx-{breakpoint}-{number}```, ```.gy-{breakpoint}-{number}```

- Use `padding-left` and `padding-right` for `--gutter-x`, and `margin-top` for `--gutter-y`
- Default list is from 0 to 5
