# test_investigation

## はじめに ##
フロントエンドではテストを実施される機会は少ないかと思われます。
理由としては、下記が挙げられるかと思われます。
 - UIが都度代わりそれによってテストを書き直しの手間が発生。そのスパンが短いため最終的にコスパが悪い
 - アクセスシビリティの観点や機能面、インタラクション面、表示崩れ、セキュリティ面など多くの観点からテストを必要があるため、煩わしさが出る
 - 多くのテストツールがあり、学習コストがかかる
 - 弊社ではフロントメンバーではあまりチーム開発をやっていないため何と無く作業者がコードを理解しているため、わざわざ書き起こす必要がない

正直自分もそうです。そのためテストを書くなら、多くの改修をこなした方が良いかと思います。

しかし最近ではこのようなことが発生する機会が多くなったと思います。
 - **新しいサイトにアサインされた方**  
   →ゾンビファイルやゾンビコードこれらは本当に消して良いのか？と迷ったこと
   
 - **Nuxt3へ移行をしていく方**  
   → この関数ではこの入力の場合はこの出力で良いのか？　他の入力された場合は。。。多分大丈夫。。。  
   → 移行前と機能面で差異ないよね？多分  
   
 - **チーム開発をしている方(チーム開発になっていきそうな場合)**  
 → コードレビューに時間を取りすぎていないか? その際にテストコードもあればそこまで時間はかかっていないのでは？
 
 これらを解決するために必要最低限のテストを書いていければ良いかと思っております。
 
## テストの種類 (メインどころ) ##
| テスト種類                   | テストコスト | 信用性 | テスト内容                                                               | 
| ---------------------------- | ------------ | ------ | ------------------------------------------------------------------------ | 
| 単体テスト                   | 低           | 低     | 一つのモジュールで与えた入力に対して、予想する出力が返ってくるかのテスト | 
| 結合テスト                   | 中           | 中     | 複数のモジュールを組み合わせて予想する結果になるか                       | 
| E2Eテスト(End to End テスト) | 高           | 高     | ユーザー視点からアプリケーションを触りテスト(インタラクションテスト)     | 

例
単体テスト：Nuxtでいう1つのComponent入出力の確認や1関数での入手力の確認
結合テスト：複数のコンポーネントや複数の関数を組み合わせたテスト、Nuxtで言うpage単位でのテストなど
E2Eテスト：我々がdev環境などで実際にテスト環境をぽちぽちしていくテスト

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
- アクセスシビリティの見直しができる

## テストで重要なこと
- チーム内でルール、テスト粒度を決めること
- 最小限のテストにすること
- チーム内でしっかりと導入すること

## 上記テストの種類 例 ##

**単体テスト、結合テスト**  
有名どころのツール：Jest, Vitest
1. テストファイルに必要なコンポーネントファイルなどをimportする
2. テストファイルに必要なライブラリも必要
3. 1のファイルをmount(テスト実行のためセット)
4. 2を使ってテスト明記
5. npmコマンドなどでテストファイルごともしくは全てのテスト実行

テストコード例

```typescript
import { describe, expect, test } from 'vitest';
import { mount } from '@vue/test-utils'
import Top from '../components/Top.vue'

describe('TopComponent', () => {
　　 // TOPコンポーネントをマウント
    const wrapper = mount(Top);
    
    // TOPコンポーネントの初期描画の際にリアクティブデータのcounterが初期値0かのテスト
    test('first refs of counter = 0', () =>{
        expect(wrapper.vm.counter).toBe(0);
    })
    
    // TOPコンポーネントでincrement関数(counter ＋１する処理)を実行した際にリアクティブデータのcounterが1になっているかテスト
    test('after increment refs of counter = 1', async() =>{
        await wrapper.vm.increment();
        await expect(wrapper.vm.counter).toBe(1);
    })
});
```

**E2Eテスト**  
有名どころのツール：PlayWright  
1. APIでのdocker環境の立ち上げ
2. アプリケーション(Nuxt)でのdocker環境立ち上げ
3. テストファイルにページアクセス時のURLなど記載したり、ページアクセスの記載をしたりする
4. 3のファイルをnpmコマンドで実行する(複雑な遷移をすればするほど複雑に)

## テストの種類 (他) ##
| テスト種類                     | テストコスト | 信用性 | テスト内容                                                                                       | 
| ------------------------------ | ------------ | ------ | ------------------------------------------------------------------------------------------------ | 
| インタラクションテスト         | 中〜高       | 中〜高 | ユーザー操作によって想定するフィードバックが返ってくるかのテスト                                 | 
| アクセスシビリティテスト             | 中〜高       | 中〜高 | アクセスシビリティ に関するテスト                                                                 | 
| ビジュアルリグレッションテスト | 高           | 高     | コードを変更した際にコード変更前後のスクショをとりUIによるリグレッションがないかを確認するテスト | 

## テスト事例調査 ##
 ### [メルペイ](https://engineering.mercari.com/blog/entry/20211208-test-automation-policy-in-merpay-frontend/?utm_source=pocket_saves)
 
 | 項目           | 内容                                                                                                | 
| -------------- | --------------------------------------------------------------------------------------------------- | 
| 使用ライブラリ | Nuxt                                                                                                | 
| テストツール   | - Cypress(E2E) <br>- Jest(結合テストなど)                                                       | 
| テスト方針     | VueコンポーネントのテストVuexのテストは基本しない。結合テスト(ユニットテストとインテグレーションテスト)がメイン | 

### [サイボウズ](https://blog.cybozu.io/entry/2022/08/29/110000)
 - [他参考記事](https://blog.cybozu.io/entry/2022/11/14/120000)

| 項目           | 内容                                                                                                                                            | 
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | 
| 使用ライブラリ | Next.js/React                                                                                                                                   | 
| テストツール   | - Jest(ユニットテストなど) <br>- Testing Library(UIテスト) <br>- Mock Service Worker(APIモック) <br>- Storybook(ビジュアルリグレッションテスト) | 
| テスト方針     | QAチームによってほぼ全体的にテスト実施                                                                                                          | 
### [WEAR](https://techblog.zozo.com/entry/wear-web-test-config2023)

| 項目           | 内容                                                                                          | 
| -------------- | --------------------------------------------------------------------------------------------- | 
| 使用ライブラリ | React                                                                                         | 
| テストツール   | - Vitest(単体テスト) <br>- Playwright(ビジュアルリグレッションテスト)                         | 
| テスト方針     | ビジュアルインテグレーションテストがメインでサブで単体テストを細々と。E2EはQAチームによるもの | 

### [Atrae](https://atraetech.hatenablog.com/entry/2022/09/30/105747)

| 項目           | 内容                                                             | 
| -------------- | ---------------------------------------------------------------- | 
| 使用ライブラリ | React                                                            | 
| テストツール   | - Jest(単体テスト) <br>- testing-library(インタラクションテスト) | 
| テスト方針     | Jestでの単体テスト、静的解析 (導入を徐々に初めて行っている)      | 

## 参考
本：[フロントエンド開発のためのテスト入門 今からでも知っておきたい自動テスト戦略の必須知識](https://www.amazon.co.jp/%E3%83%95%E3%83%AD%E3%83%B3%E3%83%88%E3%82%A8%E3%83%B3%E3%83%89%E9%96%8B%E7%99%BA%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E3%83%86%E3%82%B9%E3%83%88%E5%85%A5%E9%96%80-%E4%BB%8A%E3%81%8B%E3%82%89%E3%81%A7%E3%82%82%E7%9F%A5%E3%81%A3%E3%81%A6%E3%81%8A%E3%81%8D%E3%81%9F%E3%81%84%E8%87%AA%E5%8B%95%E3%83%86%E3%82%B9%E3%83%88%E6%88%A6%E7%95%A5%E3%81%AE%E5%BF%85%E9%A0%88%E7%9F%A5%E8%AD%98-%E5%90%89%E4%BA%95-%E5%81%A5%E6%96%87/dp/4798178187)　

サイト：https://codezine.jp/article/detail/17672

