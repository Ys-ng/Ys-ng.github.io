---
layout: post
title: 韩国视觉文化与物质文化研究专题课程作品
subtitle: CAFA Design
categories: processing
tage: [processing, art]
---


#### 中央美术学院 设计学院 艺术与科技专业
#### 韩国视觉文化与物质文化研究专题课程作品
梁圣喜 设计学院 231704010 

作品介绍：
这个作品应用了韩国的五方色（白,黑,蓝,红,黄）和八角纹样为元素，用了编程语言和数学公式来呈现的互动纹样。

互动方式：
这个纹样接到画面里鼠标的运动方向来改变自己的形状。并且每个鼠标的位置决定每个线条的运动方式。


<html>
<head>
<script src="https://sciencelove.com/attachment/cfile23.uf@994D3E435C2B1ACB02DF23.js"></script>   
</head>
<body>
<script type="application/processing">

float t;
float theta=0f;
float k = 90f;
float r = 150;

final float RATE=0.0003;

void setup()
{
  size(600,600);
}

 

void draw()
{
  theta += RATE;
  fill(0,3);
  noStroke();
  rect(0, 0, width, height);
  translate(width/2,height/2);
  float mx = mouseX - width/2;
  float my = mouseY - height/2;
  float pmx = pmouseX - width/2;
  float pmy = pmouseY - height/2;
    stroke(255);
    for(int i=0;i < 8; i++)
    {
      rotate(i*PI/4);
      
      float d = dist(mx,my,pmx,pmy);
      println(d);
      if(d < 1)
      {
        //println(mx,my);
        mx = mx/20 + x1(t);
        my = my/20 + y1(t);
        pmx = x1(t);
        pmy = y1(t);
        
      }
      
      float d2 = dist(mx, my, 0, 0 );
      strokeWeight(0.02*d2);
        if(i == 0 ||i == 7){stroke(255);}
        if(i == 1 ||i == 6){stroke(90,90,90,230);}
        if(i == 2 ||i == 5){stroke(255,50,50);}
        if(i == 3 ||i == 4){stroke(70,92,255);}
        
        line(mx,my,pmx,pmy);
        //line(mx/2,my/2,pmx/2,pmy/2);
        //line(mx,my,pmx/2,pmy/2);
        line(mx*1.5-50,my*1.5+50,pmx/1.5+30,pmy/1.5+30);//line
        line(mx*2+50,my*2+50,pmx*3-20,pmy*3-20);
        
        //yellow
        stroke(255,255,0,200);
        //line(mx/3+20,my/3+20,pmx/2.5+30,pmy/2.5-30);
        line(mx/3+20,my/3+20,15,15);
  
        //white for remove
        stroke(255,5);
        //fill(0,1);
        line(mx,my,pmx,pmy);
        line(mx/2,my/2,pmx/2,pmy/2);
        strokeWeight(2);
        rect(mx/4,my/4,pmx/4,pmy);
        rect(mx/8,my/8,pmx*0.5+30,pmy*0.5+30);
        rect(mx*1+40,my*1+40,pmx+40,pmy+40);
        rect(mx*1+80,my*1+80,pmx+80,pmy+80);
        rect(mx*2+80,my*2+80,pmx-140,pmy-140);
        
        rect(mx*3+10,my*3+10,pmx-200,pmy-200);
        rect(mx*4+50,my*4+50,pmx/2-100,pmy/2-100);
        
    }
    t += 0.0001;
}

float x1(float t)
{
  return cos(t*k)*cos(theta)*r;
}

float y1(float t)
{
  return cos(t*k)*sin(theta * 60)*r;
}

</script>
<canvas width="400" height="200"></canvas>


</body>
</html>


