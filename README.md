# test_investigation

## テストのデメリット ##
- コードを修正したら、テストコードを修正するという手間が発生する(保守する手間)
- 知識がないと着手しづらい
- 多くのテストライブラリやテストタイプがでてきており判断が難しい
- ドキュメントほとんど英語もしくは中国語問題

## テストのメリット ##
- バグの発生を早期に発見できる
- サイト品質を担保するため(リグレッションを防ぐ)
- チーム開発におけるレビュー依頼の材料になり円滑なコラボレーションを果たせる
- コードの見直し、コードの整理を果たせる

## テストで重要なこと
- チーム内でルール、テスト粒度を決めること
- 最小限のテストにすること
- チーム内でしっかりと導入すること

## テスト事例調査 ##
- [メルペイ](https://engineering.mercari.com/blog/entry/20211208-test-automation-policy-in-merpay-frontend/?utm_source=pocket_saves)：
    - 使用ライブラリ： Nuxt
    - テストツール：　Cypress
    - 使用テスト：VueコンポーネントのテストVuexのテストは基本しない。ユニットテストとインテグレーションテストがメイン

- [サイボウズ](https://blog.cybozu.io/entry/2022/08/29/110000)
    - 使用ライブラリ： Next.js/React
    - テストツール：　Jest / Testing Library / Mock Service Worker (MSW)
    - 使用テスト：ほぼ全体的にテスト　そのケースにあったテストを実行
    - [他参考記事](https://blog.cybozu.io/entry/2022/11/14/120000)

- [WEAR](https://techblog.zozo.com/entry/wear-web-test-config2023)
    - 使用ライブラリ： React
    - テストツール： Vitest
    - 使用テスト：ビジュアルインテグレーションテストがメインでサブで単体テストを細々と

- [Atrae](https://atraetech.hatenablog.com/entry/2022/09/30/105747)
    - 使用ライブラリ： React
    - テストツール： Jest
    - 使用テスト：Jestでの単体テスト、静的解析 (導入を徐々に初めて行っている)




