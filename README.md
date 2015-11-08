# KExcelAPI [![Build Status](https://travis-ci.org/webarata/KExcelAPI.svg?branch=master)](https://travis-ci.org/webarata/KExcelAPI)

Kotlin用のApache POIのラッパーです。皆さん大好きなExcelをできるだけ簡単にアクセスできるように考えています。

このライブラリーは[GExcelAPI](https://github.com/nobeans/gexcelapi)から影響を受けて作成しています。

## 使い方

シートから、セル名かセルのインデックスを指定して直感的にアクセスできます。
データの取得には方が必要なので、toInt、toDouble、toStr等のメソッドで値を取得します。
データのセットの場合には型が自明なため、「=」でExcel上に値をセットできます。

```kotlin
// 簡単にファイルオープン、クローズ
KExcel.open("file/book1.xlsx").use { workbook ->
    val sheet = workbook.getSheetAt(0)

    // セルの読み込み
    // セル名でのアクセス
    println("""B7=${sheet["B7"].toStr()}""")
    // セルのインデックスでのアクセス [x, y]
    println("B7=${sheet[1, 6].toDouble()}")
    println("B7=${sheet[1, 6].toInt()}")

    // セルの書き込み
    sheet["A1"] = "あいうえお"
    sheet[3, 7] = 123

    // ファイルの書き込みも簡単に
    KExcel.write(workbook, "file/book2.xlsx")
}
```

## ライセンス
Apache 2.0 License

