# マスク画像を生成する

drawContours : 輪郭の検出情報をもとに、輪郭の描画を行う関数
- 第一引数 : 多次元配列(numpy.ndarray)
- 第二引数 : 輪郭を形成する画素(点)情報
- 第三引数 : 輪郭を形成する画素(点)のインデックス番号を指定する。例えば0を指定すると、1番目の輪郭を形成する画素(点)のみを描画する。1を指定すると、2番目の輪郭を形成する画素(点)のみを描画する。輪郭を形成する画素(点)を全て描画したい場合は、-1を指定する。
- 第四引数 : 輪郭を形成する画素(点)の色。BGR(Blue, Green, Red)指定
- 第五引数(任意) : 輪郭を形成する画素(点)の大きさを設定。デフォルト1。

```python
mask = np.zeros_like(img_thresh)
result = cv2.drawContours(mask, [contour], -1, color=255, thickness=-1)
```

上記は抽出した領域のみ、白色で示す。

# 参考

[RGB 関数](https://support.microsoft.com/ja-jp/office/rgb-%E9%96%A2%E6%95%B0-aa04db19-fb8a-4f58-9ad6-71a1f5a43e94)

[OpenCVで使われるdrawContoursって?具体的な活用法を徹底解説!?](https://kuroro.blog/python/xaw33ckABzGLiHDFWC3m/)
