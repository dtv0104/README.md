# 嵌入式系統 - 實作2: 會呼吸的RGB LED,  按鍵控制, 狀態輸出

## 實作2-1, analogWrite(): 並且觀查LED亮度變化是否有像"呼吸的效果"和示波器的波形有什麼關連性?

![image](https://user-images.githubusercontent.com/89329178/132114919-f1e603a5-2194-420e-8102-efb3a75ba1c4.png)

```` c
int brightness = 0;

void setup()
{
  pinMode(13, OUTPUT);
}

void loop()
{
  
  digitalWrite(13, HIGH);
  delay(1000); 
  digitalWrite(13, LOW);
  delay(1000);
}
````

## 實作2-2, RGB LED燈全彩模組, 分別讓LED輪流表現正紅、正綠、正藍，三個顏色，時間間隔1秒鐘。並且觀查LED顏色和波形或是電壓有什麼關連性? 可將個人說明在更新GitHub時一起加入

![image](https://user-images.githubusercontent.com/89329178/132970668-29336a84-abff-4f1d-adb7-7f249dc64099.png)


```` c
int R = 9;
int G = 10;
int B = 11;

void setup()
{
  pinMode(R, OUTPUT);
  pinMode(G, OUTPUT);
  pinMode(B, OUTPUT);  
}

void loop()
{
	analogWrite(R, 255);
	analogWrite(G, 0);
	analogWrite(B, 0);
  	delay(1000);
	analogWrite(R, 0);
	analogWrite(G, 255);
	analogWrite(B, 0);
  	delay(1000);
	analogWrite(R, 0);
	analogWrite(G, 0);
	analogWrite(B, 255);
  	delay(1000);  
}
````

## 實作2-3, 讓你的RGB LED燈全彩模組也可會"呼吸", LED顏色變化是否有像"呼吸的效果"和示波器的波形有什麼關連性?

![image](https://user-images.githubusercontent.com/89329178/132971010-cab194d1-7f3d-422e-942d-b6105dbc4b4d.png)

```` c
int Red = 11;
int Green = 10;
int Blue = 9;
int i = 0;
int j = 0;
void swapLED(int j, int i) {
  switch (j) {
    case 1:
    analogWrite(Red, 0);
    analogWrite(Green, i);
    analogWrite(Blue, 0);
    break;
    case 2:
    analogWrite(Red, 0);
    analogWrite(Green, 0);
    analogWrite(Blue, i);
    break;
    default:
    analogWrite(Red, i);
    analogWrite(Green, 0);
    analogWrite(Blue, 0);
    break;
  }
}

void setup()
{
  pinMode(Red, OUTPUT);
  pinMode(Green, OUTPUT);
  pinMode(Blue, OUTPUT);
}

void loop()
{
  if (j > 3) {
  	j = 0;
  }
  for (i = 1; i <= 255; i += 5) {
    swapLED(j, i);
    delay(300);
  }
  for (i = 255; i >= 1; i -= 5) {
    swapLED(j, i);
    delay(300);
  }
  j++;
}
````
