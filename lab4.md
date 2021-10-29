# 嵌入式系統 - 實作4: 七段顯示器, LCD 顯示器 + 超音波感測器
## Lab 4-1 用七段顯示器來顯示數字"8."
![4-1](https://user-images.githubusercontent.com/89329178/137322943-c163975a-7aaa-4606-8f92-1d2fd04f7470.jpg)
```` c
void setup()
{
for(int x = 1; x < 9; x++) 
  {
    pinMode(x,OUTPUT);
  }
}

void seg71(int a, int b, int c, int d, int e, int f, int g, int h)
{
  digitalWrite(1, a);
  digitalWrite(2, b);
  digitalWrite(3, c);
  digitalWrite(4, d);
  digitalWrite(5, e);
  digitalWrite(6, f);
  digitalWrite(7, g);
  digitalWrite(8, h);
  delay(500);
}

void loop()
{
  //    a, b, c, d, e, f, g, h
  seg71(0, 0, 0, 0, 0, 0, 0, 0); // OFF
  seg71(1, 1, 1, 1, 1, 1, 1, 1); // 8
}
````

## Lab 4-2 如下圖的Demo, 用七段顯示器, 顯示 . →1→ ... → 9 → 0 → 全滅, 狀態改變的間隔時間為0.5秒

https://user-images.githubusercontent.com/89329178/139417617-84e5bc66-4aa7-4394-a0ab-bbbeb7e37fbc.mp4

```` c
void setup()
{
for(int x = 1; x < 9; x++) 
  {
    pinMode(x,OUTPUT);
  }
}

void seg71(int a, int b, int c, int d, int e, int f, int g, int h)
{
  digitalWrite(1, a);
  digitalWrite(2, b);
  digitalWrite(3, c);
  digitalWrite(4, d);
  digitalWrite(5, e);
  digitalWrite(6, f);
  digitalWrite(7, g);
  digitalWrite(8, h);
  delay(500);
}

void loop()
{
  //    a, b, c, d, e, f, g, h
  seg71(0, 0, 0, 0, 0, 0, 0, 0); // OFF
  seg71(1, 1, 1, 1, 1, 1, 0, 1); // 0
  seg71(0, 1, 1, 0, 0, 0, 0, 1); // 1
  seg71(1, 1, 0, 1, 1, 0, 1, 1); // 2
  seg71(1, 1, 1, 1, 0, 0, 1, 1); // 3
  seg71(0, 1, 1, 0, 0, 1, 1, 1); // 4
  seg71(1, 0, 1, 1, 0, 1, 1, 1); // 5
  seg71(1, 0, 1, 1, 1, 1, 1, 1); // 6
  seg71(1, 1, 1, 0, 0, 0, 0, 1); // 7
  seg71(1, 1, 1, 1, 1, 1, 1, 1); // 8
  seg71(1, 1, 1, 1, 0, 1, 1, 1); // 9 }
````
