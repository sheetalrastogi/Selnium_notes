```java
Option Explicit

Dim inputText, dict, arr, item
Dim fso, outFile

inputText = "USA, China, UAE, Bangladesh, Saudi Arabia, Thailand, Malaysia, the UK, Indonesia, and Germany, " & _
            "UAE, Belgium, Indonesia, Egypt, USA, Turkey, Republic of Korea, Russian Federation, Bangladesh, " & _
            "Germany, Italy, Belgium, Egypt, Nepal, Thailand, Russia, Canada, Japan, and Sri Lanka"

Set dict = CreateObject("Scripting.Dictionary")

' Split by comma and collect unique values
arr = Split(inputText, ",")

For Each item In arr
    item = Trim(item)

    ' Remove leading "and "
    If LCase(Left(item, 4)) = "and " Then
        item = Trim(Mid(item, 5))
    End If

    If item <> "" Then
        If Not dict.Exists(item) Then
            dict.Add item, item
        End If
    End If
Next

' Write unique values to file
Set fso = CreateObject("Scripting.FileSystemObject")
Set outFile = fso.CreateTextFile("UniqueCountries.txt", True)

For Each item In dict.Keys
    outFile.WriteLine item
Next

outFile.Close

WScript.Echo "Unique countries written to UniqueCountries.txt"
```
