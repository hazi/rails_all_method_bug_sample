# README

`#all?` が `nil` を返すバグを再現する為に作成されたリポジトリです。
力及ばず原因を特定することができませんでした。

具体的には下記の様なコードまで絞り込むことができました。

```ruby
redis = Redis.new(url: 'redis://localhost:6379/0')
(0..0).all? { |_| redis.get('A'); false }
```

元々のコードでは `HogeModel.where(..)#all? { ... }` といったコードでした。
`Array#all?` では再現できず、色々試して行き着いたのが `Range#all?` でした。

また、この現象は Ruby 2.5.0 から確認されています。
Ruby 2.4.4 および、2.4.5、2.3.7 では確認できませんでした。

# 再現環境

実際の実行結果は CircleCI でも確認できます。

[![CircleCI](https://circleci.com/gh/hazi/rails_all_method_bug_sample.svg?style=svg)](https://circleci.com/gh/hazi/rails_all_method_bug_sample)

master: https://circleci.com/gh/hazi/rails_all_method_bug_sample/tree/master
MULTI_VIRSION: https://circleci.com/gh/hazi/rails_all_method_bug_sample/tree/MULTI_VIRSION

# EXAMPLE

run `./example`
