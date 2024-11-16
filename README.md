# my-nuxt-app

### デプロイコマンド
- デプロイ
```
fly deploy
```

- DB作成
```
flyctl postgres create 
```

- DB接続
```
fly postgres connect -a [DBインスタンス名]
```

DB作成時のユーザ名、パスワードなどを設定する。

- 環境変数設定
```
fly secrets set HOST_URL=[デプロイ後のURL]
fly secrets set DB_CONNECT_STRING=[接続文字列]
```

### SQL

```
CREATE TABLE orders (
    id BIGSERIAL PRIMARY KEY, -- 注文ID
    order_number BIGINT, -- 注文番号
    takoyaki_quantity INT, -- たこ焼きの注文個数
    takoyaki_price INT, -- たこ焼きの売価
    dessert_takoyaki_quantity INT, -- デザートたこ焼きの注文個数
    dessert_takoyaki_price INT, -- デザートたこ焼きの売価
    order_date TIMESTAMP, -- 注文日時
    status TEXT CHECK (status IN ('preparing', 'completed')) DEFAULT 'preparing', -- 受け渡し状況（調理中または受け渡し済み）
    pass_date TIMESTAMP DEFAULT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- 作成日
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP -- 更新日
);

CREATE TABLE pricesettings (
    takoyaki_price INT DEFAULT 300, -- たこ焼きの売価
    dessert_takoyaki_price INT DEFAULT 200, -- デザートたこ焼きの売価
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- 作成日
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP -- 更新日
);

INSERT INTO pricesettings (takoyaki_price, dessert_takoyaki_price) VALUES (300, 200);
```
