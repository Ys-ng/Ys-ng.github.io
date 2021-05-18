---
layout: post
title: My first Test
subtitle: this is a subtitle
categories: processing
tage: [test]
---

Testing Text!!!!!!

**bold**

| number | 1 | 2 |
| :- | :- | :- |
| 3 | 4 | 5 |
|one|two|three|


```java
int num;
num = 1;
```


## Boxes

### Notification


<html>
<head>
<script src="https://sciencelove.com/attachment/cfile23.uf@994D3E435C2B1ACB02DF23.js"></script>   
</head>
<body>
<script type="application/processing">
int num = 60;
float mx[] = new float[num];
float my[] = new float[num];

void setup() {
  size(640, 360);
  noStroke();
  fill(255, 153); 
}

void draw() {
  background(51); 
  
  int which = frameCount % num;
  mx[which] = mouseX;
  my[which] = mouseY;
  for (int i = 0; i < num; i++) {
    int index = (which+1 + i) % num;
    ellipse(mx[index], my[index], i, i);
    if (mousePressed){
       ellipse(mx[index], my[index], i, i);
    }
  }
}
</script>
<canvas width="400" height="200"></canvas>


</body>
</html>


