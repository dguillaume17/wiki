# Grid Layout

[Link](grid.html)

```html
<style type="text/css">
  .container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 10px;
    grid-auto-rows: minmax(100px, auto);
  }

  .container>div {
    order: 2px solid rgb(233, 171, 88);
    border-radius: 5px;
    background-color: rgba(233, 171, 88, .5);
    padding: 1em;
    color: #d9480f;
  }

  .one {
    grid-column: 1 / 3;
    grid-row: 1;
  }

  .two {
    grid-column: 2 / 4;
    grid-row: 1 / 3;
  }

  .three {
    grid-column: 1;
    grid-row: 2 / 5;
  }

  .four {
    grid-column: 3;
    grid-row: 3;
  }

  .five {
    grid-column: 2;
    grid-row: 4;
  }

  .six {
    grid-column: 3;
    grid-row: 4;
  }
</style>

<div class="container">
  <div class="one"><b>Un</b></div>
  <div class="two">Deux</div>
  <div class="three">Trois</div>
  <div class="four">Quatre</div>
  <div class="five">Cinq</div>
  <div class="six">Six</div>
</div>
```

