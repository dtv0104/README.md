# 嵌入式系統 - 實作6: 4X4鍵盤 + LCD 顯示器 + 回顧 + AI-based嵌入式系統?
## Lab 6-1 用16X2 LCD 顯示器來顯示4X4鍵盤輸入的數字 (0, 1, 2, .., 9), 若輸入的字數≥16則換到下一列, 若兩皆滿, 則清除劃面重新由Row=0, Col=0開始, 細節請參考以下Demo.
![139566852-556bef99-a665-4681-aaa3-21bf622c3cd7](https://user-images.githubusercontent.com/89329178/146677913-1a1bc44e-e189-4e76-91b4-e73fccb3490f.gif)

```` c++
#include <Keypad.h>
#include <LiquidCrystal.h>

LiquidCrystal lcd(5, 4, 3, 2, A4, A5);

const byte ROWS = 4; 
const byte COLS = 4; 
char keys[ROWS][COLS] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};

byte rowPins[ROWS] = {A0, A1, 11, 10}; 
byte colPins[COLS] = {9, 8, 7, 6}; 

int LCDCol = 0;
int LCDRow = 0;

Keypad keypad = Keypad( makeKeymap(keys), rowPins, colPins, ROWS, COLS );

void setup(){
   Serial.begin(9600);
   lcd.begin(16, 2);
   lcd.setCursor(LCDCol, LCDRow);
   }
  
void loop(){
  char key = keypad.getKey(); 

if (key){
    
    Serial.println(key);
  
if ( LCDCol > 15  )
    {   
     ++LCDRow; 
      
      if (LCDRow>1)
      { LCDRow=0; LCDCol = 0 ;  lcd.clear(); } 
   
    LCDCol = 0 ;
    }
         
    lcd.setCursor (LCDCol, LCDRow); 
    
       lcd.print(key);
    
    ++LCDCol;
} 
} 
````
