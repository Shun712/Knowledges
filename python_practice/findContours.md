# 輪郭の取得

- image: 入力画像（2値画像の方が精度がいい）
- mode: 抽出モード
- method: 近似手法

```python
imges, contours, hierarchy=cv2.findContours(image,mode,method)
```

- images: 輪郭画像
- countours: 輪郭
- hierarchy: 輪郭の階層構造

### 第2引数

[![Image from Gyazo](https://i.gyazo.com/fc36560769f59a901d5331445f4b2b37.png)](https://gyazo.com/fc36560769f59a901d5331445f4b2b37)

### 第3引数

[![Image from Gyazo](https://i.gyazo.com/56370a34c278a0d4c41e5bd345be0a1e.png)](https://gyazo.com/56370a34c278a0d4c41e5bd345be0a1e)

# 参考

[[学習メモ]OpenCVを用いた平滑化,二値化, 輪郭の抽出 - qiita](https://qiita.com/ankomotch/items/74884b0ca24b739159c0)