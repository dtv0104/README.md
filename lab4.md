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

## Lab 4-3 LCD顯示"Hello" + 你的英文名字
![image](https://user-images.githubusercontent.com/89329178/139427847-0fad0a1b-598d-4436-abf9-c1af8c8f2939.png)
```` c
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("hello, ETHAN!");
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the number of seconds since reset:
  lcd.print(millis() / 1000);
}
````
## Lab 4-4 整合超音波感測器 + LCD: 參考之前的實作, 完成以下任務:
1. **將超音波感測器傳回的距離, 在LCD上面顯示,** 
2. **同時也和之前的實作一樣, 在序列輸出.** 
3. **另外, 當物體的距離小於150cm時, 則亮紅色LED, 否則亮綠色LED**
![image](https://user-images.githubusercontent.com/89329178/139428114-e28dce74-a0b4-4f5b-a2ea-8c639d41a549.png)
````c
#include <LiquidCrystal.h> //LCD library

#define echo 7
#define trig 7

float  duration; // time taken by the pulse to return back
float  dd; // oneway distance travelled by the pulse
int RLED = 9;
int GLED = 8;
LiquidCrystal lcd(12, 11, 5, 4, 3, 2); 

void setup() {
  pinMode(RLED, OUTPUT);
  pinMode(GLED, OUTPUT);
  Serial.begin(9600);
  lcd.begin(16, 2);

}

void loop() { 

  time_Measurement();
  dd = duration * 0.01723;   
  lcd.clear();
  lcd.setCursor(0, 0);
  Serial.print("Distance, cm: ");
  Serial.print(dd);
  Serial.println();
  
 
  if(dd<150){
    digitalWrite(RLED, HIGH);
    digitalWrite(GLED, LOW);
  }
  else{
    digitalWrite(RLED, LOW);
    digitalWrite(GLED, HIGH);
  }
}

void time_Measurement()
{ //function to measure the time taken by the pulse to return back
  pinMode(trig, OUTPUT);
  digitalWrite(trig, LOW);
  delayMicroseconds(2);  
  digitalWrite(trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(trig, LOW);
  pinMode(echo, INPUT);  
  duration = pulseIn(echo, HIGH);
}

