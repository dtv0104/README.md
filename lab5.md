# 嵌入式系統 - 實作5: Servo伺服馬達, 溫度感應器 + LCD 顯示器

## 5-1 請使用兩個伺服馬達同步從 0 度逐步掃描到 180 度之後再逐步掃描回0度, 每步的間隔時間為50ms (0.05秒), 細節請參考以下Demo.
![138579717-8ab59a55-bed2-4267-868f-d6cf6a252260](https://user-images.githubusercontent.com/89329178/139423694-5853ab0f-070f-4dd8-9580-025351aa2a79.gif)
```` c
#include <Servo.h>

int pos = 0;

Servo servo_9;

void setup()
{
  servo_9.attach(9, 500, 2500);
  
}

void loop()
{
 
  for (pos = 0; pos <= 180; pos += 1) {

    servo_9.write(pos);
       

    delay(50); 
  }
  
  for (pos = 180; pos >= 0; pos -= 1) {
 
    servo_9.write(pos);
        

    delay(50); 
  }
}
````

## 5-2 LCD顯示溫度感應器的溫度;若溫度<38 綠LED亮; 若大於38度, 紅色LED亮, 細節請參考以下Demo


https://user-images.githubusercontent.com/89329178/139429888-e8885466-229d-4051-8d32-32254fa5af9f.mp4

```` c
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
int RLED = 9;
int GLED = 8;

void setup() 
{
  lcd.begin(16, 2);
  Serial.begin(9600);	
  pinMode(A1, INPUT); // Read analog voltage level (2^10)

}

void loop() 
{
  int reading = analogRead(A1);  // read analog level level (2^10)
  lcd.setCursor(0,0);  
  lcd.print("TMP Sensor Demo");

  float voltage = (reading/1024.0) * 5.0;
  float tempC = (voltage - 0.5) * 100.0;
  if(tempC<38)
  {
    digitalWrite(RLED, LOW);
    digitalWrite(GLED, HIGH); 
  }
  else
    {
      digitalWrite(RLED, HIGH);
      digitalWrite(GLED, LOW);
    }
  lcd.setCursor(0,1);
  lcd.print("Tmp:");
  lcd.print(tempC);
  lcd.print(" C");
  delay(500);
  lcd.clear();
  Serial.println(reading);
  Serial.println(voltage);  
}
````
