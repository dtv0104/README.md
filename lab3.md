# 嵌入式系統 - 實作3: 使用超音波感測器 + LED控制, 常用的C語言程式介紹

## Lab 3-1: Ultrasonic Sensor (3-pin) + 測距 (以公分顯示即可) + RS232 Output
![134792769-7eabd026-aaa9-4aa3-9968-621f0fa25cb6](https://user-images.githubusercontent.com/89329178/137321280-882646be-bb0f-43a9-b541-1f2bfaad2f6a.gif)
![134793142-4b1ba02e-e7a9-4f89-b46a-6eb0acbe36cd](https://user-images.githubusercontent.com/89329178/137321299-6c20f752-fa98-4629-b620-1215975c605c.gif)
```` c
int inches = 0;

int cm = 0;

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT); 
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  Serial.begin(9600);
}

void loop()
{
  cm = 0.01723 * readUltrasonicDistance(7, 7);
  
  inches = (cm / 2.54);
  Serial.print(inches);
  Serial.print("in, ");
  Serial.print(cm);
  Serial.println("cm");
  delay(100);
}
````

## Lab 3-2: 超音波感測器 + LED (紅色LED:亮<70cm, 緑色LED: 亮>270cm, 藍色LED:亮, 介於70cm ~ 270cm之間) + RS232 Output
![3-1](https://user-images.githubusercontent.com/89329178/137321828-f0a5e222-e8fb-46b0-86e7-51b851cf9c5d.gif)
```` c
const int Red = 12;
const int Green = 8;
const int Blue = 10;

int inches = 0;

int cm = 0;

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT); 
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  return pulseIn(echoPin, HIGH);
}

void changColor(int type){
  analogWrite(Red,0);
  analogWrite(Green,0);
  analogWrite(Blue,0);
  switch (type){
    case 1:
    analogWrite(Red,255);
    analogWrite(Green,0);
    analogWrite(Blue,0);
    break;
    case 2:
    analogWrite(Red,0);
    analogWrite(Green,255);
    analogWrite(Blue,0);
    break;
    case 3:
    analogWrite(Red,0);
    analogWrite(Green,0);
    analogWrite(Blue,255);
    break;
  }
}

void setup()
{
  Serial.begin(9600);

}

void loop()
{
  
  cm = 0.01723 * readUltrasonicDistance(7, 7);

  if(cm <70)
  {
    changColor(1);
  }
  else if(cm>= 270)
  {
    changColor(2);
  }
  else if(cm>= 70&& cm<270)
  {
    changColor(3);
  }
  
  inches = (cm / 2.54);
  Serial.print(inches);
  Serial.print("in, ");
  Serial.print(cm);
  Serial.println("cm");
  delay(100); 
}
````

## Lab 3-3:請使用Arudino, 通過Serial印出9X9乘法表, 計算時亮紅色LED, 綠色LED慢慢變亮亮完成時全亮, 並且紅色LED OFF, 細節可參考以下Demo作法:
![3-4](https://user-images.githubusercontent.com/89329178/137322279-becb2bd5-73fd-4838-8c8c-196954041802.jpg)
```` c
int RLED = 13;
int GLED = 11;


int result, result2, result3;
String d0 = "****** 9X9 Table ******";
String d1, d2, d3;
void setup()
{
  pinMode(RLED, OUTPUT);   // Configure PIN13
  pinMode(GLED, OUTPUT);   // Configure PIN11
  
  Serial.begin(9600);

}

void loop()
{
  int aa = 0;

  Serial.println(d0); 
  
  digitalWrite(RLED, HIGH);
  analogWrite(GLED, aa); 
  
  for (int i=1;i<=9; i=i+3){
    for (int j=1;j<=9; j++){
      
      result = i*j;
      result2 = (i+1)*j;
      result3 = (i+2)*j;
      
      d1 = String(String(i) + "X" + String(j) + "=" + String(result));
      d2 = String(String(i+1) + "X" + String(j) + "=" + String(result2));
      d3 = String(String(i+2) + "X" + String(j) + "=" + String(result3));
      
      Serial.println(d1 + ", " + d2 + ", " + d3);


       
      aa+=1;
      
      delay(100);
    } // loop j
    analogWrite(GLED, aa*3); 
    Serial.println("");
  } // loop i

  digitalWrite(RLED, LOW);
  analogWrite(GLED, 255); 
  delay(2000);	
  analogWrite(GLED, 0);
}
````

