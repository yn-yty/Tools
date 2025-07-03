# 変換元フォルダと保存先フォルダのパスを指定
$sourceFolder = "C:\変換元"
$destFolder = "C:\変換後"

# 一太郎アプリケーションのCOMオブジェクトを作成
$jr = New-Object -ComObject "Justsystem.JustRight"

# フォルダ内のすべての.jtdファイルを取得
Get-ChildItem -Path $sourceFolder -Filter *.jtd | ForEach-Object {
    $srcFile = $_.FullName
    $baseName = $_.BaseName
    $destDocx = Join-Path $destFolder "$baseName.docx"

    # 一太郎でファイルを開く
    $jr.Open($srcFile)

    # Word形式で保存
    $jr.SaveAs($destDocx, "DOCX")

    # ファイルを閉じる
    $jr.Close()
}

# 一太郎を終了
$jr.Quit()
