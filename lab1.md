# 嵌入式系統 - 實作1

## 1-1 在TinkerCAD開一個新的Circuit, 加上一個外部的LED, 並且ON (亮) 1秒, OFF(滅) 1秒

![image](https://user-images.githubusercontent.com/89329178/131237847-d09cd842-72d1-4ebf-ad63-ce774026c608.png)

## 1-2 在TinkerCAD開一個新的Circuit, 分別使甪R, G, B三種顏色的LED, ON (亮) 0.5秒, OFF(滅) 0.5秒

![image](https://user-images.githubusercontent.com/89329178/132113733-e90cc111-f28e-4434-9865-7a913199dd96.png)

```` C

void setup()
{
  pinMode(LED_BUILTIN, OUTPUT);
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
