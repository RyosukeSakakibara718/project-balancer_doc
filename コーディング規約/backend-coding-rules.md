# コーディングルール

Laravel Pint のデフォルトのプリセットに準拠
詳しくは[ここ](https://qiita.com/aosan/items/333d048f412bc293dc53)

## PHP コーディングルール

### use

- 改行を開けずにアルファベット順

```php=
use App\Models\User;
use Illuminate\Http\Request;
```

### 変数宣言

- 変数名はキャメルケース

```php=
$userData
```

- イコールにはスペースを入れる

```php=
$sample = 'sample';
```

### 配列

- 配列は `array()` ではなく `[]` を使用する
- ダブルアローにスペースを入れる

```php=
$samples = [
    'tokyo' => 1,
    'osaka' => 2,
];
```

### メソッドチェーン

- メソッドチェーンにはスペースを入れない
- 複数メソッドチェーンを使用する時は、一つインデントを下げて折り返す

```php=
$this->userModel
    ->where('id', $id)
    ->get();
```

### 型宣言

- 引数と戻り値には必ず型を書く
- 引数と戻り値のプリミティブ型（string int bool...etc）は小文字
- null許容する場合は型の前に `?` を用いる

```php=
public function sample(?int $id, string $name): ?string
{
    if (!$id) {
        return;
    }

    return `{$id} のユーザーは {$name} です`;
}
```

### 例外処理

- 例外が起きそうな箇所は必ず例外処理を入れる

```php=
if ($isFollow) {
    throw new Exception('すでにフォロー済みです。');
}
```

### PHPDoc

ただのコメントではなく、静的解析でも活用
クラス、関数全てに必須

- @param が引数
- @return が戻り値
- @throws が例外処理

```php=
/**
 * sampleの実装
 *
 * @param int|null $id
 * @param string $name
 *
 * @return string|null
 *
 * @throws Exception
 */
public function sample(?int $id, string $name): ?string
{
    // 省略
    
    if ($isFollow) {
        throw new Exception('すでにフォロー済みです。');
    }
    
    // 省略
}
```

## Laravel コーディングルール

### 構成

- Controller
  - Controller は `単数形` + `Controller`
    - `例: SampleController`
  - バリデーション処理は書かないこと->Requestにバリデーションは記載
  - `php artisan make:controller UserController`コマンドで作成  
  -> invokableやresourceようなオプションは必要時には追記で作成(<https://readouble.com/laravel/10.x/ja/controllers.html>)

- Model
  - 基本的には以下の責務以外は書かない
    - プロパティ（定数含む）
    - リレーション
    - DB操作（Eloquent）
  - ビジネスロジックは UseCasesディレクトリだけ切って，ドメインごとに単一責務なクラスを置く
  - `php artisan make:model Flight`コマンドで作成  
  -> mfscなどのオプションは必要時には追記で作成(<https://readouble.com/laravel/11.x/ja/eloquent.html>)

- Request
  - バリデーション処理はRequestに書くこと
  - `php artisan make:request StorePostRequest`コマンドで作成(<https://readouble.com/laravel/10.x/ja/validation.html#:~:text=%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E3%83%90%E3%83%AA%E3%83%87%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3-,%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E4%BD%9C%E6%88%90,-%E3%82%88%E3%82%8A%E8%A4%87%E9%9B%91%E3%81%AA>)

  ```php=
    public function rules()
    {
    return [
        'name' => 'required',
        'age' => 'integer | between:0,150',
        'sex' => ['max:1', 'regex:/^[男|女]+$/u'],
    ];
    }
  ```

- Resource
  - responseに関してはResourceで整理する
  - `php artisan make:resource UserResource`コマンドで作成(<https://readouble.com/laravel/10.x/ja/eloquent-resources.html>)

  ```php=
  class UserResource extends JsonResource

    {
        /**
        *Transform the resource into an array.
        *
        *@return array<string, mixed>
        */
        public function toArray(Request $request): array
        {
            return [
                'id' => $this->id,
                'name' => $this->name,
                'email' => $this->email,
                'created_at' => $this->created_at,
                'updated_at' => $this->updated_at,
            ];
        }
    }

  ```

- UseCases
  - ビジネスロジックはここに書く（複雑な処理やリレーション間の保存を制御など）
  - ドメインごとに単一責務なクラスを置く

- api（ルーティング）
  - なるべく `group()` でまとめる
  - メソッドチェーンで書く
  - `name()` を必ず使用する

### メソッド・コンストラクタインジェクション

- new は基本的に使用せずにメソッドインジェクションを使用する
- クラス内で2つ以上同じメソッドインジェクションをしている場合はコンストラクトに移行すること

> 以下、メソッドインジェクションを2つ以上使用している時の例

🙅‍♂️ ダメな例

```php=
public function index(User $userModel) {
  return $userModel;
}

public function show(User $userModel) {
  return $userModel;
}
```

🙆‍♂️ ナイスな例

```php=
private $userModel;

public function __construct(User $userModel) {
  $this->userModel = $userModel;
}

public function index() {
  return $this->userModel;
}

public function show() {
  return $this->userModel;
}
```

### トランザクション

- 保存や削除が保証されて欲しい箇所や複数を跨ぐ保存処理などはトランザクションを貼る
- どこもかしこも貼る必要はない

```php=
return DB::transaction(function () use ($userId) {
    return $this->create([
        'user_id' => $userId,
    ]);
});
```

### マイグレーションの書き方

- 親テーブル > 小テーブル > 中間テーブル の順で作成すること
- `$table->id` や `$table->timestamps()` など以外は comment()を書く
- 外部キーは `id` の次に書く
  - 外部キーは `$table->foreignId('user_id')->constrained()` の様に書く
- created_at や deleted_at などの timestamp は下の方に書く

> 例

```php=
public function up()
{
    Schema::create('user_information', function (Blueprint $table) {
        $table->id();
        $table->foreignId('user_id')->constrained();
        $table->string('muttering')->nullable()->comment('一言コメント');
        $table->string('icon')->nullable()->comment('プロフィールアイコン');
        $table->timestamps();
    });
}
```

### 定数の扱い

- Model（テーブル）と紐づくデータは `app/Models/` 配下のModelに書く
- グローバルで扱いたいデータは `app/Const/` に書く

> 例

`Modelに書くパターン`

```php=
class User extends Model
{
    private const CLASSIFICATION = [
        1 => '一般',
        2 => '学生'
    ];
}
```

`app/Const/GlobalConst`

```php=
namespace App\Consts;

class GlobalConst
{
    public const PREEFECTURE = [
        '北海道',
        '青森',
        // 省略
    ]
}
```
