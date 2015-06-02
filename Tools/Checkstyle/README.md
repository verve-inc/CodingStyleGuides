# Eclipseへの設定手順

1. 環境設定 - Checkstyle を選択

2. "Global Check Configurations"欄の"New"ボタンをクリック

3. "Check configuration"ダイアログに、以下のように選択・入力して"OK"ボタンをクリック
  Type: Remote Configuration
  Name: VERVE
  Location: https://raw.githubusercontent.com/verve-inc/CodingStyleGuides/master/Tools/Checkstyle/verve_java.xml

4. "Global check configurations"欄に"VERVE"という設定が追加されるので、それを選択して"Set as Default"ボタンをクリック。

5. "OK"ボタンをクリック