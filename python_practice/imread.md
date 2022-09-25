# imread()の使い方

- 画像ファイルを読み込むには `cv2.imread()`という関数を使う。

- 第2引数は画像の読み込む方法を指定するためのフラグである。

  - cv2.IMREAD_COLOR : カラー画像として読み込む．画像の透明度は無視される．デフォルト値
  - cv2.IMREAD_GRAYSCALE : グレースケール画像として読み込む
  - cv2.IMREAD_UNCHANGED : アルファチャンネルも含めた画像として読み込む

※上記のフラグを使う代わりに、単に`1`, `0`, ``-1` の整数値を与えて指定することもできる。

# 参考

[画像を扱う](http://labs.eecs.tottori-u.ac.jp/sd/Member/oyamada/OpenCV/html/py_tutorials/py_gui/py_image_display/py_image_display.html)