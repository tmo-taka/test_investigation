# test_investigation
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




