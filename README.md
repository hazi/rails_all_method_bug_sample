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

実際の実行結果は CircleCI でも確認できます。

[![CircleCI](https://circleci.com/gh/hazi/rails_all_method_bug_sample.svg?style=svg)](https://circleci.com/gh/hazi/rails_all_method_bug_sample)


# EXAMPLE

run `./example`
