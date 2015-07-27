---
author: fangrenbin
comments: true
date: 2012-07-25 06:58:58+00:00
layout: post
slug: get-select-value
title: get select value
wordpress_id: 377
categories:
- javascript
---

<script language="javascript" type="text/javascript">     
window.onload = selectedOption;       
function selectedOption(){      
var optionValues = ['${queryCondition.channel}',       
'${queryCondition.phoneOsVersion}',       
'${queryCondition.screenResolution}',       
'${queryCondition.softwareVersion}'];      
  
var optionIds = ['channel', 'phoneOsVersion',       
'screenResolution', 'softwareVersion'];      
  
initSel(optionValues, optionIds);      
}      
  
function initSel(dymanicValue, optionId){       
for(j = 0; j < dymanicValue.length; j++){      
var oSel = document.getElementById(optionId[j]);      
  
for (var i = 0; i < oSel.length; i++){      
if (dymanicValue[j] == oSel[i].value){      
oSel[i].selected = true;       
break;       
}      
}      
}      
}      
</script>
