# Guided Project: A Simple Photo Gallery
  
  * With what you've learned so far, you should now be able to construct a simple photo gallery. We'll get you started by creating a simple gallery of 5 images of varying sizes. We'll display the images one per line, with each image left-justified, and with a caption beneath each.

  * For this project, you can use any images you want. For the best results, try to choose a variety of different image widths, including at least one that is too big to fit horizontally in your usual browser window.

  * If you want, you can use these images instead:
    * ![Transit Shadows](https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/photo-gallery/1.jpg)
    * ![Missy Chaplin](https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/photo-gallery/2.jpg)
    * ![Thunderbirds in Formation](https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/photo-gallery/3.jpg)
    * ![Orange Rose](https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/photo-gallery/4.jpg)
    * ![Kentucky Darleks](https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/photo-gallery/5.jpg)
 
  * LS notes
    * We'll zero out the margins and padding for all these elements to ensure that the appearance remains similar in different browsers:
    * we call this type of margin/padding zeroing a reset; we'll discuss it in more detail later. For now, all you need to know is that it provides some assurance that different browsers won't display different results.
    
    * We're using the main element as a master "container" element for the entire photo gallery. It provides some semantic meaning for the document as it identifies the primary content area.

    * Now, let's walk through some additional styling to finish the gallery. 
    * Our **goal** is to end up with the five pictures arranged in a 3 row by 2 column grid, with the final grid element empty. 
    * All images should have the same width and should fit horizontally within the browser window. We'll let you do most of the work.

  * Problem: create a photo gallery
    * LS starter code; (using the given images of different sizes) all 5 images are displayed on the photo gallery page; but they're all different sizes/shapes.
    * you have to scroll down the page to see all the images 
    
    * **goal** arrange the phots in grid of 3 rows by 2 columns. with the final grid empty.
    * all images should have the same width (height should be scaled (by browser?) to keep the aspect ratio)
    * should be able to view all 5 images at once- inside the browser window (no scrolling)?
    
  
* LS Guided Steps
  1. After loading the page, you may notice that the images are vertically too near each other, 
    * and they're flush with the top and left edges of the window. 
    * Adjust the spacing **between the figure elements** and the distance between the left and right edges of the browser window to **50px** to give the images some breathing room.
       
     
    * Problem:
      * current spacing between images is too small -adjust it to 50px all sides - top/bottm margins
      * adjust spacing on the/right of the browser to 50px as well - left/right margins to 50px
      
      * LS added a `red` outline to each figure - debugging tool.
      * if there is a border; the outline goes directly outside of it; (not matter how thick the border is)
      * the outline is outside of the content-box, and any padding/borders. the margins are seen outside of the `outline` line.
      * unlike borders, outlines don't affect the box model or the page layout.
    
    ```css 
    figure {
      margin: 50px;
      outline: 1px solid red;   /* for development use only - does not affect the page layout or box model for the any elements */
    }
    ```


  2. Reduce your browser window's width, if necessary, until at least one image exceeds the window width. 
    * Next, adjust the CSS to make them all fit inside the window. 
    * Don't forget that there is a margin around each figure, which should be evident when you display the page.

    * Once you're done, check what happens as you expand and shrink the browser window; no matter what adjustments you make, all images should fit in the window.
  
    * Problem: adjust the css to have all the images be completetly viewable (not cutoff) in all windows sizes - expanded/shrunken browser window size.
    * need to set either height/width to have them all fit in any window size. set one to a fixed size
      * (probably relative percentage of the available display )- especially since each image has a different width/height
    * the margin around all sides is 50px. 
    
    * images are inline by default
      * but the browser does not ignore width/height for images.
      * images use both left/right and top/bottom margins
      
    * so if we switch the box-sizing to border box then everything but the margins are accounted for. 
    * if we use width/height with auto the browser will to fit the entire element(including the margins) into the container
    
    * both height/and width can be both auto? so it can fit even with the margins
    
    * RESULT:
      * setting `img` to width: auto does make the image fit into the container (figure) in a standard browser size
        * but the images don't shrink with changing browser size.
      * for items to fit with changing browser, percentages are what work.
      * since the `margin` values of 50px apply to the entire container (meaning figure container must be 50px from the edges/other pictures)
        * but the image(its content; no padding or border here) should fit inside the entire container
      * using width: 100% let's the image fill the entire figure container box AND let's it shrink/grow depending on the browser size.
      
    * this let's the image size fit in any window (but it doesn't fill its container - only fills it when the window is very small)
    ```css
    img {
      max-width: 100%
    }
  ```
  
  3. Every image should use the entire width of the figure elements. Modify your CSS to implement this requirement.
    * we change the width to be 100%, so at all times the image fits its container
    * and it still fits it at 100% when we shrink the viewport (browser window) down
  
  ```css
    img {
      /* max-width: 100%; delete this line */
      width: 100%;
    }
  ```


  4. Reduce the width of each figure to 1/2 the width of the browser window:
    * add a width property to the figure css rule, set it to 50%\
    ```css 
    figure {
      width: 50%; /* added to figure css rule */
    }
    ```
  
  5. At this point, the figures are narrow enough that we should be able to squeeze 2 of them in every row on the page. 
    * However, since figure's are block elements, they always take up an entire row. Instead, you must convert the figure elements to inline-block. Please do so.
    
    * add a `display: inline-block` property to the css figure rule
    ```css
    figure {
      display: inline-block;
    }
    ```
  
    * LS note: Even though we converted the box model to inline-block, the images still don't fit side-by-side. There's a problem - actually, two problems. Can you see what's wrong? Try to determine what you need to do before continuing. We'll return to this issue after an unrelated question.
   
   
    * block elements can end up on the same line if they have different parents (if those parents are inline-block or inline) - block figure elements have their parent - main who is a block element
    
    * each figure is an inline-block element. so the whitespace between elements is collapsed into one or two whitespacess and it's seen as content between the two elements
    * and each figure has 50px margin between elements which collapses to just 50px between two elements in the middle of them for inline-block
    
    * remove the whitespace between inline-elements and the making the margins 0 between figures lets them be side by side
    * since the width is 50% for each figure (not including margins or any between element whitespace)- both margin and that whitespace content needs to be handled for two images to show on one line
    * 

  6. There's a small cosmetic issue unrelated to squeezing two images per row. Let's center the captions beneath each image:
    * we need to center the `figcaption` element in each figure container.
    ```css 
    figcaption {
      text-align: center;
    }
    ```

  7. Returning to the problem of squeezing two images per row, the main issue we have is that we have margins to the left and right of each figure. 
    * Recall that we used margins here to satisfy our rule of thumb about choosing margins or padding. 
    * However, those margins take up space in the browser window, so we can't squeeze two 50%-width elements side-by-side. 
    * Instead, we need to set the left and right margins on the figure elements to 0, and redistribute that space in some other way. Give this a try now.
    
    * if we change box-sizing to border-box, then we can use padding instead. border-box will shrink the content size (the image) so that everything (except margins) will fit inside its container
    * we can set the padding to 50px instead
    
    * so in my code, I set padding to be all around 50px (to replace margin) and I removed the whitespace with comments (for the images that we want side by side)
    * LS solution only changed the left/right to be padding (so that the content will shrink to fit side by side with another image)
    * but LS left the top/bottom margin to still be the previous 50px. they want each image to be 50px from any row above or below them
    * now the images don't completely fill the container due to the left/right padding. but they are sized to fit two images per row; with their aspect ratio intact
    *
    LS solution 
    ```css 
    figure {
      box-sizing: border-box;
      margin: 50px 0;
      padding: 0 50px;
    }
   ```


  8. The other part of the problem of squeezing two images per row is that there is a small amount of whitespace between every pair of inline-block elements. It's not much whitespace, but it's enough to prevent two 50% elements from fitting side-by-side. Go ahead and make the necessary adjustments to get rid of the whitespace.
    * I used comments between the section elements that I wanted to share the same line (but since it's 50% fill width for each figure container, that actually won't matter)
    * LS solution used font 0 instead (font zero whitespace takes up zero space - but for some mobile browsers/may have a few weird issues  like cascading em fonts)
    * 
    ```html  
    <!-- space between multiple figure elements -->
    <figure></figure><!--
    
      --><figure>
    ```
  
    * versus LS solution of zero font
  ```css 
    main {
      font-size: 0;
    }
    
    figcaption {
      font-size: 1rem;
    }
  ```
  * By reducing the font size for the main element to 0 (we don't have any other text in this element), the space character shrinks into nothingness. However, we must remember to restore the font before we display anything, such as the caption.
  * since font size is inherited
  

  9. The images are a bit on the small side. Let's give the user the ability to see them full-sized by clicking on them. 
    * When clicked, the browser should load the image directly into a new tab or window. To accomplish this, convert your images into links.
     
    * you can do this by wrapping an image element inside an `a` element
    * we'll use the same link here so that the user can view the image in a new tab/window - where the image won't be constrained by other elements/layout on the page that its currently viewed on
    
    * now the img elements are wrapped in the a tag.
    ```css 
     <figure>
      <a href= "https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/photo-gallery/1.jpg" target="_blank">
        <img src="https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/photo-gallery/1.jpg"
             alt="Transit Shadows" />
      </a>
      <figcaption>Transit Shadows</figcaption>
    </figure><!--
    ```

  10. You can now get rid of the outline you attached to the figure elements, and assign a pleasant background to the gallery. You can use the background image we used earlier in this lesson (https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/gradient-background.png) or one of your own.
   
   ![background image](https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/gradient-background.png)
  
  ```css 
  figure {
    outline: 1px solid red;  /* removed to get rid of outline */
  }
  
  body {
    background-image:
      url("https://d3jtzah944tvom.cloudfront.net/202/images/lesson_3/gradient-background.png");
  } 
  ```

 * with my solution, the background is different colors for the images margins/behind the caption
 * when you change the screen size; it shows differing portions of the background image. (like you don't see 100% of the background when you shrink the page)
 * when you enlarge browser (basically zooming out) the background repeats- the full background image show up more than once
 
 * LS solution added 
 ```css
 body {
   background-size: cover; /* this scales the background image without changing the proportions to fit the available space; rather than leaving it at its natural size
 }
 ```