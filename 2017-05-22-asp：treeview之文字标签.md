---
layout: post
title: "asp：treeview之文字标签"
date: 2017-05-22 12:00:00 +0800
categories: c#
tag: [asp.net]
---   

### 文字标签

由于本人无法在原有图层的基础上添加label，故新建了图层，在该图层上添加label标签。以下所有内容都是基于openlayers2库的基础上拓展的。

1.新建图层
```
// allow testing of specific renderers via "?renderer=Canvas", etc
var renderer = OpenLayers.Util.getParameters(window.location.href).renderer;
renderer = (renderer) ? [renderer] : OpenLayers.Layer.Vector.prototype.renderers;

vectorLayer = new OpenLayers.Layer.Vector("Simple Geometry", {
    styleMap: new OpenLayers.StyleMap({
        'default': {
            /*
            strokeColor: "#00FF00",
            strokeOpacity: 1,
            strokeWidth: 3,
            fillColor: "#FF5500",
            fillOpacity: 0.5,
            pointRadius: 6,
            pointerEvents: "visiblePainted",
            // label with \n linebreaks*/

            label: "${name}",

            fontColor: "${favColor}",
            fontSize: "12px",
            fontFamily: "Courier New, monospace",
            fontWeight: "bold",
            labelAlign: "${align}",
            labelXOffset: "${xOffset}",
            labelYOffset: "${yOffset}",
            labelOutlineColor: "white",
            labelOutlineWidth: 3
        }
    }),
    renderers: renderer
});
map.addLayer(vectorLayer);
```
2.添加图标文字
```
function drawTLabel2(lnglats) {
    features3 = [];
    if(lnglats){
        for (var i = 0; i < lnglats.length; i = i + 1) {
            // Create a point feature to show the label offset options
            var labelOffsetPoint = new OpenLayers.Geometry.Point(lnglats[i].LGTD, lnglats[i].LTTD);
            var labelOffsetFeature = new OpenLayers.Feature.Vector(labelOffsetPoint);
            labelOffsetFeature.attributes = {
                name:lnglats[i].STNM,
                favColor: 'black',
                align: "cm",
                // positive value moves the label to the right
                xOffset: 4,
                // negative value moves the label down
                yOffset: -10
            };
            features3.push(labelOffsetFeature);
        }
       vectorLayer.addFeatures(features3);
     }
}
```

- [openlayer站点下标](http://dev.openlayers.org/examples/vector-features-with-text.html)
- [openlayers2:vector-features-with-text.html](https://github.com/crschmidt/openlayers/blob/master/examples/vector-features-with-text.html)