{
  "plugin_type": "widget",
  "name": "Countdown Timer",
  "edit_page_url": "www.optimizely.com",
  "form_schema": [
    {
      "default_value": "2018/09/30",
      "field_type": "text",
      "name": "date",
      "label": "Date",
      "options": null
    },
    {
      "default_value": "this clock hits zero!!!",
      "field_type": "multi_text",
      "name": "offer_content",
      "label": "Offer Content",
      "options": null
    },
    {
      "default_value": ".justify-content-start",
      "field_type": "selector",
      "name": "selector",
      "label": "Placement",
      "options": null
    },
    {
      "default_value": "rgba(230, 246, 62, 1)",
      "field_type": "color",
      "name": "backgroundcolor",
      "label": "Background Color",
      "options": {
        "mode": "rgba"
      }
    }
  ],
  "description": "Countdown to a specified deadline in DD.HH.MM.SS",
  "options": {
    "html": "<div id=\"optimizely-widget-{{ widget.$instance }}\" id=\"countdown\" class=\"countdown\">\n  <div id=\"clockdiv\" style=\"background-color:{{widget.backgroundcolor}}\">\n    You have <span class=\"days bold\"></span> days, <span class=\"hours bold\"></span> hours, <span class=\"minutes bold\"></span> minutes and  \n    <span class=\"seconds bold\"></span> seconds until {{widget.offer_content}}\n\t</div>\n</div>\n",
    "css": ".countdown_timer {\n  width: 100%;\n}\n\n#clockdiv{\n  width: 100%;\n  margin: auto;\n  font-family: sans-serif;\n  color: #000000;\n  display: inline-block;\n  font-weight: 100;\n  text-align: center;\n  font-size: 1.5em;\n  padding-top:1%;\n  padding-bottom:1%; \n}\n\n.bold {\n\tfont-weight: bold;\n  color: red;\n}",
    "apply_js": "var utils = optimizely.get('utils');\nvar selector = widget.selector;\n\nutils.waitForElement(selector).then(function(element){\n  var html = widget.$html;\n  var deadline = widget.date;\n\n  element.insertAdjacentHTML('beforebegin', html);\n\n  function getTimeRemaining(endtime){\n    var t = Date.parse(endtime) - Date.parse(new Date());\n    var seconds = Math.floor( (t/1000) % 60 );\n    var minutes = Math.floor( (t/1000/60) % 60 );\n    var hours = Math.floor( (t/(1000*60*60)) % 24 );\n    var days = Math.floor( t/(1000*60*60*24) );\n    return {\n      'total': t,\n      'days': days,\n      'hours': hours,\n      'minutes': minutes,\n      'seconds': seconds\n    };\n\t}\n  \n  function initializeClock(id, endtime){\n    var clock = document.getElementById(id);\n    var daysSpan = clock.querySelector('.days');\n    var hoursSpan = clock.querySelector('.hours');\n    var minutesSpan = clock.querySelector('.minutes');\n    var secondsSpan = clock.querySelector('.seconds');\n      function updateClock(){\n        var t = getTimeRemaining(endtime);\n          daysSpan.innerHTML = t.days;\n          hoursSpan.innerHTML = ('0' + t.hours).slice(-2);\n          minutesSpan.innerHTML = ('0' + t.minutes).slice(-2);\n          secondsSpan.innerHTML = ('0' + t.seconds).slice(-2);\n        if(t.total<=0){\n          clearInterval(timeinterval);\n        }\n      }\n\n\t\tupdateClock(); // run function once at first to avoid delay\n\t\tvar timeinterval = setInterval(updateClock,1000);\n\t}\n\n\tinitializeClock('clockdiv', deadline);\n});",
    "undo_js": "var extensionHtml = document.querySelector('.countdown');\nif (extensionHtml){\n\textensionHtml.remove();\n}\n"
  }
}
