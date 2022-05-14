# ページネーションのテスト実装

```ruby
it 'ページネーションボタンが表示されること' do
  create_list(:crop, 30)
  # create_listした後はページ更新しなければ表示されない
  visit crops_path
  expect(page).to have_css('.page-link')
  # ページネーション'2'のボタンをクリックし、次ページへと行く
  expect { find_link('2', rel = "next").click }
  expect { find_link('1', rel = "prev").click }
end
```

# 参考

[Rails6】RSpecによるページネーション機能（kaminari）の結合テストの実装 - qiita](https://qiita.com/narimiya/items/53a956a265b99c58c309)