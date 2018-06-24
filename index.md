<html>

<head>
	<meta name="viewport" content="width=device-width">
	<h1 style="font-size:300%; font-family:impact; font-color:#000000;text-align:center;">Bubba's Freedom</h1>
	<p style="text-align:center;">Bubba will reagain his freedom in:</p>
	
</head>
<script type="text/javascript">
//###################################################################
// Author: ricocheting.com
// Version: v3.1
// Date: 2017-01-03
// Description: displays the amount of time until the "dateFuture" entered below.

var CDown = function() {
	this.state=0;// if initialized
	this.counts=[];// array holding countdown date objects and id to print to {d:new Date(2013,11,18,18,54,36), id:"countbox1"}
	this.interval=null;// setInterval object
}

CDown.prototype = {
	init: function(){
		this.state=1;
		var self=this;
		this.interval=window.setInterval(function(){self.tick();}, 1000);
	},
	add: function(date,id){
		this.counts.push({d:date,id:id});
		this.tick();
		if(this.state==0) this.init();
	},
	expire: function(idxs){
		for(var x in idxs) {
			this.display(this.counts[idxs[x]], "Now!");
			this.counts.splice(idxs[x], 1);
		}
	},
	format: function(r){
		var pre='',post='',divide=', ',
			out="";
		out += pre+r.y +" "+((r.y==1)?"year":"years")+post+divide;</ br>
		out += pre+r.w +" "+((r.w==1)?"week":"weeks")+post+divide;</ br>
		out += pre+r.d +" "+((r.d==1)?"day":"days")+post+divide;</ br>
		out += pre+r.h +" "+((r.h==1)?"hour":"hours")+post+divide;</ br>
		out += pre+r.m +" "+((r.m==1)?"min":"mins")+post+divide;</ br>
		out += pre+r.s +" "+((r.s==1)?"sec":"secs")+post+divide;

		return out.substr(0,out.length-divide.length);
	},
	math: function(work){
		var	y=w=d=h=m=s=ms=0;

		ms=(""+((work%1000)+1000)).substr(1,3);
		work=Math.floor(work/1000);//kill the "milliseconds" so just secs

		y=Math.floor(work/31536000);//years (no leapyear support)
		work=work%31536000;

		w=Math.floor(work/604800);//weeks
		work=work%604800;

		d=Math.floor(work/86400);//days
		work=work%86400;

		h=Math.floor(work/3600);//hours
		work=work%3600;

		m=Math.floor(work/60);//minutes
		work=work%60;

		s=Math.floor(work);//seconds

		return {y:y,w:w,d:d,h:h,m:m,s:s,ms:ms};
	},
	tick: function(){
		var now=(new Date()).getTime(),
			expired=[],cnt=0,amount=0;

		if(this.counts)
		for(var idx=0,n=this.counts.length; idx<n; ++idx){
			cnt=this.counts[idx];
			amount=cnt.d.getTime()-now;//calc milliseconds between dates

			// if time is already past
			if(amount<0){
				expired.push(idx);
			}
			// date is still good
			else{
				this.display(cnt, this.format(this.math(amount)));
			}
		}

		// deal with any expired
		if(expired.length>0) this.expire(expired);

		// if no active counts, stop updating
		if(this.counts.length==0) window.clearTimeout(this.interval);
		
	},
	display: function(cnt,msg){
		document.getElementById(cnt.id).innerHTML=msg;
	}
};

window.onload=function(){
	var cdown = new CDown();

	cdown.add(new Date(2036,5,20,14,00,00), "countbox1");
};
</script>
<div id="countbox1"></div>
<div id="countbox1" style="font:36pt Impact; color:#000000; text-align:center;"></div>
