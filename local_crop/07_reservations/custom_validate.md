# 予約時間のバリデーションをつける

過去の日時を選択できないようにバリデーションを設ける

# モデルにバリデーションを設定

validateを単数形にする

```ruby
class Reservation < ApplicationRecord
  validate :received_at_check

  def received_at_check
    return unless date_passed?

    errors.add(:received_at, 'は現在時刻より遅い時間を選択してください')
  end
end
```

# 参考

[カスタムバリデーションを実行する - Railsガイド](https://railsguides.jp/active_record_validations.html#%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%A0%E3%83%90%E3%83%AA%E3%83%87%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%92%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B)

[RailsでCustom Validatorの実装例 - qiita](https://qiita.com/nobuo_hirai/items/8b0661808a022f85c10c)

[【Rails】開始時間(datetime型)と終了時間にバリデーションをつける - qiita](https://qiita.com/nindendon/items/fe77535a0af36261cefd)