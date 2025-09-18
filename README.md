<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Spin & Win Game</title>
  <style>
    body { text-align:center; font-family:Arial; background:#f0f0f0; }
    #wheelCanvas { margin:20px auto; display:block; }
    button { padding:10px 20px; font-size:18px; cursor:pointer; background:#28a745; color:white; border:none; border-radius:8px; }
    #result { font-weight:bold; font-size:18px; margin-top:10px; }
  </style>
</head>
<body>
  <h2>🎯 Spin & Win 🎯</h2>

  <!-- PopUnder Ad -->
  <script type="text/javascript" src="//data156.click/f9352e31b31d83333899/41d6fe59db/?placementName=default"></script>

  <canvas id="wheelCanvas" width="300" height="300"></canvas>
  <button onclick="spinWheel()">SPIN</button>
  <p id="result"></p>

  <script>
    const canvas=document.getElementById("wheelCanvas"),ctx=canvas.getContext("2d");
    const options=["💰 10 Coins","❌ Try Again","⭐ Bonus","🎁 Gift","🔥 Jackpot","💎 50 Coins"];
    const colors=["#f54242","#42f554","#4287f5","#f5a142","#d142f5","#42f5e6"];
    let startAngle=0,arc=Math.PI/(options.length/2),spinTimeout=null,spinAngleStart=10,spinTime=0,spinTimeTotal=0;

    function drawRouletteWheel(){
      ctx.clearRect(0,0,300,300);
      for(let i=0;i<options.length;i++){
        let angle=startAngle+i*arc;
        ctx.fillStyle=colors[i];
        ctx.beginPath();
        ctx.arc(150,150,150,angle,angle+arc,false);
        ctx.arc(150,150,0,angle+arc,angle,true);
        ctx.fill();
        ctx.save();
        ctx.fillStyle="white";
        ctx.translate(150+Math.cos(angle+arc/2)*100,150+Math.sin(angle+arc/2)*100);
        ctx.rotate(angle+arc/2+Math.PI/2);
        ctx.fillText(options[i],-ctx.measureText(options[i]).width/2,0);
        ctx.restore();
      }
    }

    function rotateWheel(){spinTime+=30;if(spinTime>=spinTimeTotal){stopRotateWheel();return;}
      let spinAngle=spinAngleStart-easeOut(spinTime,0,spinAngleStart,spinTimeTotal);
      startAngle+=(spinAngle*Math.PI/180);
      drawRouletteWheel();
      spinTimeout=setTimeout(rotateWheel,30);
    }

    function stopRotateWheel(){clearTimeout(spinTimeout);
      let degrees=startAngle*180/Math.PI+90,arcd=arc*180/Math.PI,index=Math.floor((360-degrees%360)/arcd);
      document.getElementById("result").innerHTML="Result: "+options[index];
    }

    function easeOut(t,b,c,d){let ts=(t/=d)*t,tc=ts*t;return b+c*(tc-3*ts+3*t);}
    function spinWheel(){spinAngleStart=Math.random()*10+10;spinTime=0;spinTimeTotal=Math.random()*3000+4000;rotateWheel();}
    drawRouletteWheel();
  </script>
</body>
</html>