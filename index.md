<html>

<head>
 <title>Your Page Name</title>
<SCRIPT LANGUAGE="JavaScript">

<!-- 

var Temp2;
var timerID = null;
var timerRunning = false;
function arry() {
this.length = 12;
this[0] = 31;
this[1] = 28;
this[2] = 31;
this[3] = 30;
this[4] = 31;
this[5] = 30;
this[6] = 31;
this[7] = 31;
this[8] = 30;
this[9] = 31;
this[10] = 30;
this[11] = 31;
}
var date = new arry();

function stopclock() {
if(timerRunning)
clearTimeout(timerID);
timerRunning = false;
}

function startclock() {
stopclock();
showtime();
}

function showtime() {
now = new Date();
var CurMonth = now.getMonth();
var CurDate = now.getDate();
var CurYear = now.getFullYear();
now = null;
if (20 < CurDate) {
CurDate -= date[CurMonth]; CurMonth++;
}
if (5 < CurMonth) {
CurMonth -= 12; CurYear++;
}

var Yearleft = 2036 - CurYear;
var Monthleft = 6 - CurMonth;
var Dateleft = 20 - CurDate;

document.dateform.a.value = Yearleft;
document.dateform.b.value = Monthleft;
document.dateform.c.value = Dateleft;

timerID = setTimeout("showtime()",1000);
timerRunning = true;
}

// -->
</script>
</head>
<body Onload="startclock();">
<form name="dateform">
<!-- This code generated at www.csgnetwork.com/ymdcountdowngen.html. -->
Only <input type="text" name="a" size="2" value=""> years, 
<input type="text" name="b" size="2" value=""> months, and 
<input type="text" name="c" size="2" value=""> days left until 6/20/2020
</form>
<!-- The content of your HTML document begins here. --> 
</head>

<body>
<!-- Display the countdown timer in an element -->
<p id="demo"></p>

<script>
// Set the date we're counting down to
var countDownDate = new Date("Jun 13, 2036 15:37:25").getTime();

// Update the count down every 1 second
var x = setInterval(function() {

  // Get todays date and time
  var now = new Date().getTime();

  // Find the distance between now an the count down date
  var distance = countDownDate - now;

  // Time calculations for days, hours, minutes and seconds
  var days = Math.floor(distance / (1000 * 60 * 60 * 24));
  var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
  var seconds = Math.floor((distance % (1000 * 60)) / 1000);

  // Display the result in the element with id="demo"
  document.getElementById("demo").innerHTML = days + "d " + hours + "h "
  + minutes + "m " + seconds + "s ";

  // If the count down is finished, write some text 
  if (distance < 0) {
    clearInterval(x);
    document.getElementById("demo").innerHTML = "EXPIRED";
  }
}, 1000);
</script>
</body>

</html>
