## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/bdvenom/bubbafreedom/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3


<script>
  
  var startTime = 0.25; //set countdown in Minutes
  
  var doneClass = "done"; //optional styling when timer is done
  function startTimer(duration, display) {
    var timer = duration, minutes, seconds;
    var intervalLoop = setInterval(function () {
        minutes = parseInt(timer / 60, 10)
        seconds = parseInt(timer % 60, 10);
        minutes = minutes < 10 ? "0" + minutes : minutes;
        seconds = seconds < 10 ? "0" + seconds : seconds;
		for(var i=0;i<display.length;i++){
          display[i].textContent = minutes + ":" + seconds;
        }
        if (--timer < 0) {
          for(var i=0;i<display.length;i++){
            display[i].classList.add(doneClass);
            display[i].textContent = "DONE";
          }
          clearInterval(intervalLoop);
        }
    	}, 1000);
	}
window.onload = function () {
    var setMinutes = 60 * startTime,
    display = document.querySelectorAll(".timer");
    startTimer(setMinutes, display);
};
</script>
