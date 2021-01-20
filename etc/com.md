# COM
## COM(Component Object Model)
* 여러 Component object를 이용해 프로그램을 개발하는 모델
* Component object는 객체지향 언어에서의 클래스로부터 만들어지는 객체와 비슷
* 프로그래밍 언어와 상관없이 개발된 객체를 사용할 수 있게 해줌.

## 예시
```py
import win32com.client

excel = win32com.client.Dispatch("Excel.Application")
excel.Visible = Ture
wb = excel.Workbooks.Add()
ws = wb.Worksheets("Sheet1")
ws.Cells(1, 1).Value = "hello world"
wb.SaveAs('C:\\test.xlsx')
excel.Quit()
```