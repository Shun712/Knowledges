# threshで閾値を設定

画像の2値化処理するために設定する。

```python
ret, th=cv2.threshold(img,thresh,maxval,type)
```
- ret: threshと同じ値
- th: 2値化した画像
- img: 入力画像(グレイスケール)
- thresh: 閾値
- maxval: 閾値以上の値を持つ値に対して割り当てる値を指定
- type: `THRESH_BINARY_INV`の場合しきい値よりも大きな値であれば0、それ以外はmaxvalの値にする。

[![Image from Gyazo](https://i.gyazo.com/f45fd226239002da86a5d516f32c7ea3.png)](https://gyazo.com/f45fd226239002da86a5d516f32c7ea3)

引用：[OpenCV – 画像処理の2値化の仕組みと cv2.threshold() の使い方](https://pystyle.info/opencv-image-binarization/)

# 参考

[【初心者向け】PythonとOpenCVで画像処理を体験してみよう](https://tech-blog.rakus.co.jp/entry/20201225/open-cv)

[[学習メモ]OpenCVを用いた平滑化,二値化, 輪郭の抽出 - qiita](https://qiita.com/ankomotch/items/74884b0ca24b739159c0)

[【Python】OpenCVで画像の閾値処理（2値化）をする](https://www.learning-nao.com/?p=1866)
