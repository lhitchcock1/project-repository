if(typeof ZERG == "undefined") {
    var ZERG = {};
}
if ( typeof ( ZERG.crc ) === "undefined" ) {
	ZERG.crc = {};
	ZERG.crcArr = [];
}
ZERG.zergInterval = false;
ZERG.gebcn = (typeof document['getElementsByClassName'] == "function");
ZERG.infiniteZerg = function( poll ) {
    var widgets = [];
    if ( ZERG.gebcn ) {
        widgets = document.getElementsByClassName( "zergnet-widget" );
    } else {
        var qsa = (typeof document['querySelectorAll'] == "function");
        if ( !qsa ) {
            var d=document, s=d.createStyleSheet();
            d.querySelectorAll=function(r,c,i,j,a){a=d.all,c=[],r=r.replace(/\[for\b/gi,'[htmlFor').split(',');for(i=r.length;i--;){s.addRule(r[i],'k:v');for(j=a.length;j--;)a[j].currentStyle.k&&c.push(a[j]);s.removeRule(0)}return c};
        }
        widgets = document.querySelectorAll(".zergnet-widget");
    }
	if ( typeof( ZERG.counters ) === "undefined" ) {
		ZERG.counters = {};
	}
	if ( typeof( ZERG.counters['61747'] ) === "undefined" ) {
		ZERG.counters['61747'] = 0;
	}

    var wArr = [];
    var lastData = "";
    var dupeCount = 0;
    var dupeTryLimit = 5;
	var widgetId = '61747';

    var loadWidget = function() {
        var randcallback = Math.floor((Math.random() * 9999999) + 1);
        var timestamp = new Date().getTime()+wArr.length;
        var JSONP = (function(){var a=randcallback,c,f,b,d=this;function e(j){var i=document.createElement("script"),h=false;i.src=j;i.async=true;i.onload=i.onreadystatechange=function(){if(!h&&(!this.readyState||this.readyState==="loaded"||this.readyState==="complete")){h=true;i.onload=i.onreadystatechange=null;if(i&&i.parentNode){i.parentNode.removeChild(i)}}};if(!c){c=document.getElementsByTagName("head")[0]}c.appendChild(i)}function g(h,j,k){f="?";j=j||{};for(b in j){if(j.hasOwnProperty(b)){f+=encodeURIComponent(b)+"="+encodeURIComponent(j[b])+"&"}}var i="json"+(++a);d[i]=function(l,z){k(l,z);try{delete d[i]}catch(m){}d[i]=null;};e(h+f+"callback="+i);return i}return{get:g}}());

		if ( typeof ZERG['running'] === "undefined" ) {
			ZERG['running'] = 1;
		} else if ( ZERG['running'] ) {
			setTimeout( loadWidget, 200 );
			return false;
		} else if ( ZERG['running'] == 0 ) {
			ZERG['running'] = 1;
		}
		var payload = {id:widgetId,time:timestamp,c:ZERG.counters[widgetId],t:"inf",sc:1};
		if ( ZERG.crcArr.length ) {
			payload['crc'] = JSON.stringify( ZERG.crcArr );
		}
        if(typeof(ZERG['nocookie'])!=='undefined'){payload['nocookie']=1;}
        JSONP.get( 'https://www.zergnet.com/output.js', payload, function(data, crc){
			ZERG['running'] = 0;
            if ( data == lastData && dupeCount < dupeTryLimit ) {
                dupeCount++;
                loadWidget();
                return;
            }
            if (typeof window.opera != 'undefined') {
                document.write(data);
            } else {
                if ( Object.prototype.toString.call( wArr ) === '[object Array]' && wArr.length ) {
                    var c = wArr.shift();
                    c.innerHTML = data;
                    lastData = data;
                }
            }
			if ( typeof( crc ) !== "undefined" && crc.length ) {
				for ( var i = 0; i < crc.length; i++ ) {
					ZERG.crc[crc[i]] = crc[i];
					ZERG.crcArr.push( crc[i] );
					if ( ZERG.crcArr.length > 30 ) {
						var val = ZERG.crcArr.shift();
						if ( typeof( ZERG.crc[val] ) ) {
							delete( ZERG.crc[val] );
						}
					}
				}
			}
        });
		ZERG.counters[widgetId]++;
    };

    for ( var i = 0; i < widgets.length; i++ ) {
        var w = widgets[i];
        if ( w.className.indexOf( "widget-loaded" ) == "-1" ) {
            w.className += " widget-loaded";

            wArr.push( w );

            if ( wArr.length == 1 ) {
                loadWidget();
            } else {
                setTimeout( loadWidget, (wArr.length-1)*200 );
            }
        }
    }

    ZERG.zergInterval = false;
    if ( poll === true ) {
        ZERG.zergInterval = setTimeout( ZERG.infiniteZerg, 1000 );
    }
};
ZERG.triggerInfiniteZerg = function() {
    if ( !ZERG.zergInterval ) {
        ZERG.zergInterval = setTimeout( ZERG.infiniteZerg, 500 );
    }
};
ZERG.init = function() {
    if (window.addEventListener) { // W3C DOM
        window.addEventListener("scroll",ZERG.triggerInfiniteZerg,false);
		ZERG.triggerInfiniteZerg();
    } else if (window.attachEvent) { // IE DOM
        window.attachEvent("onscroll", ZERG.triggerInfiniteZerg);
		ZERG.triggerInfiniteZerg();
    } else {
        ZERG.infiniteZerg( true );
    }
};
ZERG.init();
