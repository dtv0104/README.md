# 嵌入式系統 - 實作1

## 1-1 在TinkerCAD開一個新的Circuit, 加上一個外部的LED, 並且ON (亮) 1秒, OFF(滅) 1秒

![image](https://user-images.githubusercontent.com/89329178/131237847-d09cd842-72d1-4ebf-ad63-ce774026c608.png)

## 1-2 在TinkerCAD開一個新的Circuit, 分別使甪R, G, B三種顏色的LED, ON (亮) 0.5秒, OFF(滅) 0.5秒

![image](https://user-images.githubusercontent.com/89329178/132114077-fd422286-9aa8-4bb6-b7db-b5cc6652502e.png)


```` C
void setup()
{
  pinMode(13, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(9, OUTPUT);
}

void loop()
{
  // turn the LED on (HIGH is the voltage level)
  digitalWrite(13, HIGH);
  digitalWrite(11, HIGH);
  digitalWrite(9, HIGH);
  delay(500); // Wait for 500 millisecond(s)
  // turn the LED off by making the voltage LOW
  digitalWrite(13, LOW);
  digitalWrite(11, LOW);
  digitalWrite(9, LOW);
  delay(500); // Wait for 500 millisecond(s)
}

````
## 1-3 在TinkerCAD開一個新的Circuit, 分別使甪R, G, B三種顏色的LED, 讓LED ON, OFF的順序為R >> G >> B >> G >> R .... 無限循環

![image](https://user-images.githubusercontent.com/89329178/132114501-80d56c3b-b437-46c1-b829-c8bbb2acff5b.png)

```` c
void setup()
{
  pinMode(13, OUTPUT);
  
}

void loop()
{
  
  digitalWrite(13, HIGH);
  delay(500);
  digitalWrite(13, LOW);
  delay(500);
  digitalWrite(11, HIGH);
  delay(500);
  digitalWrite(11, LOW);
  delay(500);
  digitalWrite(9, HIGH);
  delay(500);
  digitalWrite(9, LOW);
  delay(500);
  
}
````
