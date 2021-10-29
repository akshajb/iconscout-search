# Task 1 and Task 2

## Note:

Tried to recreate as much as possible from the Iconscout search page. Below are the features as well as challenges faced during this mini project.

### Features

1. Search for Icons from the input in the Navbar.
2. Sub header with result count and text.
3. Sidebar filters for Price, Dimension and Styles.
4. Sidebar animation.
5. Collapse for each filter category using BootstrapVue.
6. Filter badges near search results to remove them.
7. Icon Results
8. Icon tile hover state for like and download button.
9. Loading animation.
10. Proper Route queries for all the filters and results.
11. "Icon Editor" link in the Navbar for Task 2.

### Challenges

1. Challenge: icon_grid attribute for Dimension filter unavailable in <code>/v3/search/</code> API.<br/> 
   Solution: Went through the Live API at iconscout.com to see what was being used.
   
2. Challenge: <code>product_type="pack"</code> does not return pack results, instead gives back <code>item</code> results.<br/> 
   Solution: Since a working solution cannot be implemented without the API results, the filter for packs is disabled.
   
3. Challenge: Task 2. <br/> 
   Solution: 
   
   i. Convert palette colors to HSL.<br/> 
   ii. Convert Icon colors to HSL.<br/> 
  iii. Compare hue of each Icon color with each palette color to find the minimum distance/difference.<br/> 
  iv. Use the palette color with the least difference in hue as the icon color until the number of icon colors are less than palette colors.<br/> 
  v. Once the icon colors exceed the palette colors count, Apply the hue with the minimum distance while preserving the saturation and lightness from the icon colors to generate the new colors.<br/> 

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```



