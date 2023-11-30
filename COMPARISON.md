# vitestとjestの比較

## わかいりやすい記事
https://jiko21-tech-blog.monster/blog/2022-02-13/vitest-compare-jest

## メリット
- テスト実行時間の高速化
- configファイルを一元で管理できる  
→ jestの場合はwebpackのconfig, jestのconfigファイル等を触るなど複数ファイルを跨ぐ必要があった
- HMRの有効活用できる   
→ watchでテストを回す際にHMRでうまく処理できているので手元でテストを試す際に高速化できる（初めてテストを書く人にとって手元でのテスト実行が高速なためストレス軽減）
- Nuxt3のデフォルトビルドツールがviteのため導入がスムーズ
- TypeScriptとjsxをサポート
- DOMを用いたテストをする際にjestではデフォルトでjsdomが入っているが、vitestには入っていない。そのため新規に[happydom](https://www.npmjs.com/package/happy-dom)(jsdomより格段に処理が高速)を導入できる  
→Bunのテストツールも同様構成
- 日付のモック作成機能などデフォルトで入っている
- coverage reportをHTMLで見やすく表示することも可能
  ブラウザベースのテストランナー(Cypress,WebdriverIO)との親和性が高い 

## なぜ人気がでているのか
- 多くのフロントフレームワークでViteが使用されることが多いため。
- テストツールで人気のjestと同様のAPIを導入しているためjestからの移行がスムーズ

## Nuxtとの親和性
- AutoImportへの対応が[unplugin-auto-import](https://github.com/unplugin/unplugin-auto-import)  
→ jestの場合は自作でglobalファイルを作成してパス解決していた。。。
[参考](https://github.com/unplugin/unplugin-auto-import/issues/33)

## 自分の考えた結論
### vitestの導入を推奨
以下観点からです。
- Nuxt3的の観点
  - テストを導入していくNuxt3のデフォルトのビルドツールがViteのため。
  - Nuxt3でよく使用されるautoImportへの対応がやりやすいため。
- WC的の観点
  - テスト経験者がおらずはじめのうちはローカル環境でテストを実行することが多いため、watchの高速化が作業効率に繋がるため。
  - WCのサイト上Compoentが100個や200個もあるようなサイトがないため、わかいりやすい記事のような大幅な速度違いはでないと思われるため。

## 最後にテストにおいて
vitestはjestに比べまだやりやすいというレベル感です。かつvitestやjestはテストのベースとなるツールなだけでそれを基に多くのライブラリを追加していく必要があります。そのためフロンエンドのテストは少し難しいです。
また[公式](https://nuxt.com/docs/getting-started/testing)に記載ある通り、Nuxt3はまだテストユーティリティはまだ開発中とのことで完全に保証はしてくれていません。
