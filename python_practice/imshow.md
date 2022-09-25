# imshow()の使い方

画像をウィンドウ上に表示するには `cv2.imshow()` という関数を使う。

```python
cv2.imshow('image',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
上記のコードは、ウィンドウに画像を表示させ、入力時間（0）ミリ秒までに何かしらのキーを押せば、ウィンドウが閉じる。

# 参考

[画像を扱う](http://labs.eecs.tottori-u.ac.jp/sd/Member/oyamada/OpenCV/html/py_tutorials/py_gui/py_image_display/py_image_display.html)