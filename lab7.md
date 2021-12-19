# 實作7: AI-based ES? AI? ML? DL? 要如何入門 (How To Learn)?
## Lab 7-1 在你的Google Drive建立你的第一個Colab Notebook
###1.安裝Colab
###2.新增ES2021的Folder
###3.在此Folder下, 建立你的第一個Colab Notebook (i.e. 'hello-ai'). 將你的Google Drive和Google VM (Virtual Machine)掛接
###4.在你Colab Notebook顯示以下訊息(OOO: 你的英文名字; e.g., Joe biden)
###5.新增文字儲存格 (請用你的英文名字)
![image](https://user-images.githubusercontent.com/89329178/146678378-c76be253-fcb7-448e-9614-dd776bc9a3b9.png)

# Lab 7-2 暖身: 一起來十分鐘學會Python
```` c
# task 1: string variable
name = "Ethan"
print(name)

# task 2: number variable
number = 26
print(number)
print(number*3)
print(number/2)
print(number + number)
print(number - number)

# task 3: function

def printName(firstName, lastName):
  print(lastName + ' ' + firstName)

printName('Ethan', 'Ethan')

# task 4: if else

def printName(firstName, lastName, isCool):
  if isCool:
    print(lastName + ' ' + firstName + ' very cool!')
  else:
    print(lastName + ' ' + firstName + ' not cool!')

# Start
printName('Ethan', 'Ethan', True)
printName('Ethan', 'Ethan', False)

# task 5: for loop

def printName(firstName, lastName, isCool, num):
  for i in range(1, num):
    if isCool:
      print(i, lastName + ' ' + firstName + ' very cool!')
    else:
      print(i, lastName + ' ' + firstName + ' not cool!')

# Start
printName('Ethan', 'Ethan', True, 10)
````
![223216](https://user-images.githubusercontent.com/89329178/146678779-51d86533-9af5-4027-b042-3759cc1086df.png)

# Lab 7-3 確認Lab7完成的兩個Notebook都成功的存在你的雲端硬碟/ES2021目錄下
![141666966-a2d44ad3-e4bc-4670-b562-2a75dd01c19a](https://user-images.githubusercontent.com/89329178/146678785-ef5f131c-cd45-4b97-8a92-cc1be0ed0549.png)

