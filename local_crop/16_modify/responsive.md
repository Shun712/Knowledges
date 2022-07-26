# テーブルのレスポンシブデザイン

[![Image from Gyazo](https://i.gyazo.com/faae885144983779bc835299188c0233.png)](https://gyazo.com/faae885144983779bc835299188c0233)

```html
<div class="my-parts">
	<table>
		<tr><th>table data</th><th>table data</th><th>table data</th></tr>
		<tr><td>table data</td><td>table data</td><td>table data</td></tr>
		<tr><td>table data</td><td>table data</td><td>table data</td></tr>
		<tr><td>table data</td><td>table data</td><td>table data</td></tr>
		<tr><td>table data</td><td>table data</td><td>table data</td></tr>
	</table>
</div>
```

```css
.my-parts {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
  max-width: 100%;
}
.my-parts table {
  border-collapse: collapse;
  border: 1px solid rgba(0,0,0,.1);
  table-layout: fixed;
  width: 1300px;
}
.my-parts th, .my-parts td {
  border: 1px solid rgba(0,0,0,.1);
  padding: .6em;
  text-align: center;
  background: #fff;
}
.my-parts th {
  background: #009688;
  color: #fff;
  font-weight: bold;
}
```

# 参考

[Webパーツ屋](https://haniwaman.com/parts/post-3778/)