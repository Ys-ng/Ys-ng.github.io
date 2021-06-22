---
layout: post
title: Processing
subtitle: cafa
categories: processing
tage: [processing]
---

2021/06/23

## CAFA


<html>
<head>
<script src="https://sciencelove.com/attachment/cfile23.uf@994D3E435C2B1ACB02DF23.js"></script>   
</head>
<body>
<script type="application/processing">
void setup()
{
  size(500,500);
}

 

void draw()
{
  fill(0,5);
  noStroke();
  rect(0, 0, width, height);
  translate(width/2,height/2);
  float mx = mouseX - width/2;
  float my = mouseY - height/2;
  float pmx = pmouseX - width/2;
  float pmy = pmouseY - height/2;

    stroke(255);
    for(int i=0;i < 4; i++)
    {
      rotate(i*PI/2);
      float d = dist(mx,my,pmx,pmy);
      //float sw = map(d,1,10,10,1);
      if(d!=0){
        
      if(i == 0){stroke(255);}
      if(i == 1){stroke(70,92,255);}
      if(i == 2){stroke(255,50,50);}
      if(i == 3){stroke(80,80,80,200);}
      
      line(mx,my,pmx,pmy);
      line(mx/2,my/2,pmx/2,pmy/2);
      line(mx,my,pmx/2,pmy/2);line(mx,my,pmx/2,pmy/2);//line
      
      //yellow
      stroke(255,255,0,200);
      line(mx/3+10,my/3+10,pmx/3+10,pmy/3+10);
      line(mx/3+10,my/3+10,15,15);

      //white for remove
      stroke(255,10);
      line(mx,my,pmx,pmy);
      line(mx/2,my/2,pmx/2,pmy/2);
      line(mx/4,my/4,pmx/4,pmy/4);
      }
    }
}
</script>
<canvas width="400" height="200"></canvas>


</body>
</html>


