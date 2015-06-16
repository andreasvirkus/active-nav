# active-nav
A snippet that changes the active menu item while scrolling.

## HTML
Be sure to have a `<ul>` tag  with the ID assigned to the JS var `topMenu`
..Also, have the desired anchor ID-s in the navigation's links' `href` attributes, e.g.

    <ul id="a-cool-menu">
      <li class="active">
        <a href="#">Top</a>
      </li>
      <li>
        <a href="#foo">Foo</a>
      </li>
      <li>
        <a href="#bar">Bar</a>
      </li>
    </ul>
    
        
    <div id="foo"></div>

    <div id="bar"></div>




## JavaScript
    // Cache selectors
    var topMenu = $("#a-cool-menu"),
    topMenuHeight = topMenu.outerHeight()+15,
    // All list items
    menuItems = topMenu.find("a"),
    // Anchors corresponding to menu items
    scrollItems = menuItems.map(function(){
      var item = $($(this).attr("href"));
      if (item.length) { return item; }
    });

    // Bind to scroll
    $(window).scroll(function(){
    // Get container scroll position
    var fromTop = $(this).scrollTop()+topMenuHeight;

    // Get id of current scroll item
     var cur = scrollItems.map(function(){
     if ($(this).offset().top < fromTop)
       return this;
     });
     // Get the id of the current element
     cur = cur[cur.length-1];
     var id = cur && cur.length ? cur[0].id : "";
     // Set/remove active class
     menuItems
       .parent().removeClass("active")
       .end().filter("[href=#"+id+"]").parent().addClass("active");
      });​
