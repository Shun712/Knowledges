# ファイル生成を制限

```
puts class Application < Rails::Application

 #以下のように、generateコマンド時に生成されるファイルに制限をかける
   config.generators do |g|
     g.assets  false # CSS, JSが自動生成されない
     g.test_framework  false # Minitestが自動生成されない
     g.skip_routes  true # ルーティングが自動生成されない
   end
 end
```

# 参考

[https://qiita.com/ryota21/items/643737b54f331b0aaa72 - qiita](https://qiita.com/ryota21/items/643737b54f331b0aaa72#%E8%87%AA%E5%8B%95%E7%94%9F%E6%88%90%E3%81%99%E3%82%8B%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AB%E5%88%B6%E9%99%90%E3%82%92%E3%81%8B%E3%81%91%E3%82%8B)
