### html
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Catbook</title>
    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <nav class="navContainer">
      <!--Could surround the nav element with <header> tags to make it more semantically correct -->
      <h1 class="navTitle">Catbook</h1>
      <!--Replace with <a> when catbook has a homepage to link to!-->
    </nav>

    <div class="appContainer">
      <div class="avatarContainer">
        <img class="avatar" src="cat.png" alt="turtle" />
      </div>
      <h1 class="name u-textCenter">Buka Buka</h1>
      <hr class="line" />
      <div class="u-flex">
        <section class="subContainer u-textCenter">
          <h4 class="subTitle">About Me</h4>
          <p>
            I am more of a turtle person but I'm just trying to fit in and get a
            catbook.
          </p>
        </section>
        <section class="subContainer u-textCenter">
          <h4 class="subTitle">My Favorite Type of Cat</h4>
          <p>I actually prefer turtles.</p>
        </section>
      </div>
    </div>
  </body>
</html>

```

```css
@import url("https://fonts.googleapis.com/css?family=Open+Sans:300,600");

:root {
  --primary: #396dff;
  --grey: #f7f7f7;
  --white: #fff;

  --xs: 4px;
  --s: 8px;
  --m: 16px;
  --l: 24px;
}

body {
  margin: 0;
  font-family: "Open Sans", sans-serif;
}

.u-flex {
  display: flex;
}

.u-textCenter {
  text-align: center;
}

.navContainer {
  padding: var(--s) var(--m);

  background-color: var(--primary);
}

.navTitle {
  color: var(--white);
  font-size: 20px;
  /* Below cancels out some of the default styling of h1 */
  margin: 0;
  font-weight: normal;
}

.appContainer {
  /* TODO: Add a max width, padding, and margin so that
   * the content on the page isn't larger than 960px and
   * this div is centered if the browser is larger tahn 960px.
   */
  max-width: 960px;
  padding: var(--m) var(--m);
  margin: auto;
}

.avatarContainer {
  /* padding makes the image only takes up 30% of the container */
  padding: 0 35%;
}

.avatar {
  /* make it responsive */
  max-width: 100%;
  width: 100%;

  /* make it a circle */
  border-radius: 50%;

  /* make it have a 1:1 aspect ratio */
  aspect-ratio: 1;
  object-fit: cover;
}

.name {
  /* TODO: Change the size and weight of the font so it feels
   * important!
   */
  font-size: 2.4em;
  font-weight: 300;
}

.line {
  /* TODO: Change the color of the line so that it's less weighty */
  border-color: var(--grey);
}

.subContainer {
  flex-grow: 1;
  flex-basis: 0;
}

.subContainer + .subContainer {
  /* TODO: Hmm, I wonder if this can be used to add spacing between
   * subContainers...
   * https://developer.mozilla.org/en-US/docs/Web/CSS/Adjacent_sibling_combinator
   */
  margin-left: var(--m);
}

.subTitle {
  /* TODO: Change the size and weight of the font so it feels
   * important! Optionally add some margin.
   */
  font-size: 1.5em;
  font-weight: 300;
  margin: var(--m) var(--s);
}

```


