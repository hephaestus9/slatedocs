# Changing the Logo

Just replace `source/images/logo.png` with your logo. We recommend a width of 230px and a height of around 50-100px. You can adjust the padding below the logo in `source/stylesheets/_variables.scss`, with the `$logo-margin` variable.

# Adding Images

If you want to add images in the center section of slate you need to perform few steps to achieve this.

Change `index.html.md` to `index.html.md.erb`

Change the name of your include file where the image needs to be placed from `*.md` to `*.md.erb` as well

Change the includes in `index.html.md.erb` from

    includes:
        - test-images.md

To

    includes:
        - test-images.md.erb

Finally in `test-images.md.erb` add the following tag to add an image `<%= image_tag "images/my-image.png" %>`