# confirmダイアログを含むシステムスペック

`<%= link_to user_destroy_path, method: :delete, id: "delete_button", data: {confirm: "本当に削除しますか？"} %>`

# confirmダイアログでOKを選択する

`page.accept_confirm { find('.delete-button').click }`

# confirmダイアログでキャンセルを選択する

`page.dismiss_confirm { find('.delete-button').click }`

# 参考

[【Rails】Selenium/RSpecでconfirmダイアログのテストをする - qiita](https://qiita.com/at-946/items/403d85d45cb02615c323)