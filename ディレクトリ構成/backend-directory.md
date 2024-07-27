```
laravel/app/
├─┬ Exceptions/  #共通の例外処理
│ └── Handler.php
├─┬ Http/
│ ├─┬ Requests/
│ │ ├─┬ User/
│ │ │ ├── StoreRequest.php
│ │ │ └── UpdateRequest.php
│ ├─┬ Resources/
│ │ ├── UserResource.php
│ ├─┬ Controllers/
│ │ ├── UserController.php
│ │ └── Controller.php
│ └── Middleware/
├─┬ Models
│ ├── User.php
├── Providers/
└─┬ UseCases/
  ├─┬ User/  #ドメインのビジネスロジック
  │ ├── StoreAction.php
  │ └── UpdateAction.php
  └─┬ Exceptions/  #そのドメインのみの例外処理
    └── PostLimitExceededException.php


laravel/tests
├── Feature/  #Controllerのテスト
│   ├── Http/
│   │   ├── Controllers/ #Controllerと同様のディレクトリ分け
│   │   ├── Middleware/
│   │   └── Routes/
│   ├── Console/
│   └── useCase/
├── Unit/ #単体テスト
│   ├── Models/ #modelと同様のディレクトリ分け
│   ├── useCase/ #useCaseと同様のディレクトリ分け
│   └── Helpers/
└── Integration/ #結合テスト
    ├── Database/
    ├── API/
    └── External/
```

