```
src/
├── App.tsx                             # 最終的に描画されるページ
├── pages/                              # 各ページ (Feature Element)
│   ├── Home/                           # ホームページ (Feature Element)
│   │   ├── components/                 # ホームページ固有のコンポーネント (Presentation Layer)
│   │   │   ├── molecules/              # Molecules（分子）－ ホームページ専用の小さなコンポーネントの組み合わせ
│   │   │   ├── organisms/              # Organisms（有機体）－ ホームページ専用の複雑なコンポーネント
│   │   │   └── templates/              # Templates（テンプレート）－ ホームページのレイアウトテンプレート
│   │   │       └── index.tsx           # そのページの完成形
│   │   ├── hooks/                      # ホームページのカスタムフック (Business Logic Layer)
│   │   └── api/                        # ホームページ関連API呼び出し (Data Access Layer)
│   └─── Profile/                       # プロフィールページ (Feature Element)
│       ├── components/                 # プロフィールページ固有のコンポーネント (Presentation Layer)
│       │   ├── molecules/              # Molecules（分子）－ プロフィールページ専用の小さなコンポーネントの組み合わせ
│       │   ├── organisms/              # Organisms（有機体）－ プロフィールページ専用の複雑なコンポーネント
│       │   ├── templates/              # Templates（テンプレート）－ プロフィールページのレイアウトテンプレート
│       ├───  hooks/                    # プロフィールページのカスタムフック (Business Logic Layer)
│       └───  api/                      # プロフィール関連API呼び出し (Data Access Layer)
├── components/                         # 共通コンポーネント (Presentation Layer)
│   ├───    atoms/                      # Atoms（原子）－ グローバルな基本UI要素
│   ├───    molecules/                  # Molecules（分子）－ グローバルな小さなコンポーネントの組み合わせ
│   ├───    organisms/                  # Organisms（有機体）－ グローバルな複雑なコンポーネント
│   └───    templates/                  # Templates（テンプレート）－ グローバルなページレイアウトテンプレート
├── hooks/                              # グローバルなカスタムフック (Business Logic Layer)
├── api/                                # グローバルなAPI通信ロジック (Data Access Layer)
├── providers/                          # アプリケーションのすべてのプロバイダー(認証ロジックなどを記載する)
├── routes/                             # ルーティングの設定
├── stores/                             # 状態管理 (Business Logic Layer)
├── tests/                              # テストに使用するディレクトリ
│   ├── stub/                           # テストに使用するstubファイル
│   ├── components/                     # コンポーネントに対する単体テスト
│   ├── pages/                          # 各ページに対する単体テスト
│   ├── store/                          # ストアに対する単体テスト
│   └─── hooks/                         # カスタムフックに対する単体テスト
└─── styles/                            # スタイルシート


* atoms : ボタンやテキストフィールドなどの最小単位のパーツ
    * pages配下には置かない
* molecules : ロジックを含まないコンポーネント
    * ここで指すロジックとは、条件によって表示を変更する処理
* organisms : ロジックを含むコンポーネント
    * ここで指すロジックとは、条件によって表示を変更する処理
* templates : moleculesとorganismsのみが記載されているコンポーネント
```