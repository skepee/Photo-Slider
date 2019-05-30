# Photo-Slider on horizontal panels

This project shows the creation and use of horizontally panels, not vertically. The project is separated in three different files:

* **Basic Panels**: a step by step building of horizontally panels, with the use of "+" button to create panels horizontally on the right, and "-" button to remove the current panel.

* **Photo Slider a**: use of basic panels to create a photo panels. 

* **Photo Slider b**: another use of basic panels to create a photo panels without toolbar on the top. 


---

Let's analyze the **Basic Panels**.

![Basic Panel](https://github.com/skepee/Photo-Slider/ScreenshotBasicPanel.png)



Basically the panels are created through JQuery starting with a div element:

```
<div class='container'></div>
```

The loading page starts with the creation of the first panel and putting into this div. 

```
var initBox = createBox(1);
$(".container").html(initBox);

```

The createBox function basically builds the panel and the navigation on the top. Do not forget to add also the script to handle the adding/removing panels. 

```
function createBox(id)
{
  result += "<div class='box' " +  margin + " id=box" + id +">";
  result += addHandleBox(id);     // <== adds the toolbar
  result += addContent(id);       // <== adds the inner div for the content
  result += "	</div>";
  result += addScript(id);        // <== adds the adding/removing panel
  return result;
};
```

When the "+" is clicked, what happens? A new panel is added by calling the "addBox" function. An integer "i" value is passed as a parameter to the function. The "i" parameter indicates the i-th panel and it is used to create the "i+1" panel.


```
function addBox(id)
{
var idnext = parseInt(id) + 1;
var result = '';

result += "	$('#add" + id + "').click(function(){";          <== dynamically invoke createBox function on clicking on the #add element
result += "	$('.container').append(createBox(" + idnext + "));"


result += "$('#add" + id + "').hide();";       <== hide the adding/remove element on the current element
result += "$('#rem" + id + "').hide();";
result += "});";
return result;
};

```


---

Let's analyze the **Photo Slider a/b**.
In this case, because some photos will be shown, in order to make it prettier, Bootstrap will be used.
In the loading function basically the photo urls are loaded into an array.

The function "elem()" takes the n-element of the array to create the html code for the panel: 


```
function elem()
{
  var currPhoto="<img src='" + photos[currIndex] +"'></img>";
  var html="<div class='elem'><div class='headerelem alert alert-primary' role='alert'><div class='titleelem'>title</div><div class='btn'><span class='moveleft'><i class='fas fa-arrow-alt-circle-left' ></i></span>&nbsp;&nbsp;<span class='moveright'><i class='fas fa-arrow-alt-circle-right'></i></span></div></div><div class='contentelem alert alert-secondary' role='alert'>" + currPhoto + "</div></div>";

  return $(html);
}

```
