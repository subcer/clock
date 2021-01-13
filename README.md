# clock
![GITHUB]( https://github.com/subcer/clock/blob/main/clock.jpg "clock")

```js
var longCount = 0 //記述長針次數
var shortCount = 0 //記述短針次數
var longRotate = 0 //存取長針角度
var shortRotate = 0 //存取短針角度
var long60 = 0 //存取長針滿60
var reciprocal = 0 //時間倒數
var bgcolor = 0 //存取背景色

function bgchange(){ //更換背景
  bgcolor = $("body,html").css("background-color")
  if(bgcolor == "rgb(12, 68, 117)"){
    $("body,html").css("background-color","rgb(74, 0, 128)")
  }
  else if(bgcolor == "rgb(74, 0, 128)"){
    $("body,html").css("background-color","rgb(128, 0, 0)")
  }
  else if(bgcolor == "rgb(128, 0, 0)"){
    $("body,html").css("background-color","rgb(0, 128, 128)")
  }
  else if(bgcolor == "rgb(0, 128, 128)"){
    $("body,html").css("background-color","rgb(12, 68, 117)")
  }    
  
}

function addtime(){ //增加時間 長短針部分 
  longCount += 6
  //console.log(longCount)
  longRotate = 180 + longCount
  $(".long").css("transform","rotate("+longRotate+"deg)")
  if(parseInt(longCount/360)){
    shortCount=parseInt(longCount/360)*6
    shortRotate = 180 + shortCount
    $(".short").css("transform","rotate("+shortRotate+"deg)")
  }
  long60 = longCount % 360      
  $(".timeText").text("倒數計時: "+parseInt(longCount/360)+":"+(long60/6))
}
function reducetime(){  //減少時間 短針部分
  //console.log(longCount)  
  if(parseInt(longCount/360)){
    shortCount=parseInt(longCount/360)*6
    shortRotate = 180 + shortCount
    $(".short").css("transform","rotate("+shortRotate+"deg)")
  }
  else{
    shortCount=0
    shortRotate = 180 + shortCount
    $(".short").css("transform","rotate("+shortRotate+"deg)")
  }
  long60 = longCount % 360
  $(".timeText").text("倒數計時: "+parseInt(longCount/360)+":"+(long60/6))
}
function resetTime(){ //重置時間
  stopTime()
  reciprocal = 0
  longCount = 0
  shortCount = 0
  longRotate = 0
  shortRotate = 0  
  $(".short").css("transform","rotate("+180+"deg)")
  $(".long").css("transform","rotate("+180+"deg)")
  $(".timeText").text("倒數計時: 0:0")
}
function stopTime(){ //關閉時間
  clearInterval(reciprocal)
  reciprocal = 0
}
$(function(){   
  $(window).keydown(function(evt){ //按鍵觸發 
    //console.log(evt.key)
    if(reciprocal != 0){
      if(evt.key == "ArrowUp"){
        return false
      }
      if(evt.key == "ArrowDown"){
        return false
      }
      if(evt.key == "Enter"){              
        return false
      }
      if(evt.key == " "){
        stopTime()
      }
      if(evt.key == "r" || evt.key == "R"){
        resetTime()
      }
    }
    else{
      if(evt.key == "ArrowUp"){
        addtime()
      }
      if(evt.key == "ArrowDown"){
        if(longRotate>180){
          longCount -= 6
          longRotate = 180 + longCount
          $(".long").css("transform","rotate("+longRotate+"deg)")
        }        
        reducetime()
      }
      if(evt.key == " "){
        stopTime()
      }
      if(evt.key == "r" || evt.key == "R"){
        resetTime()
      }
      if(evt.key == "Enter"){
          reciprocal = setInterval(function(){
          if(longRotate>180){
            longCount -= 6
            longRotate = 180 + longCount
            $(".long").css("transform","rotate("+longRotate+"deg)")
          }
          else{
            stopTime()
            bgchange()
          }
          reducetime()
        },1000)
      }
    }        
  })
})
```

時間倒數
