# 設定

## General Config Settings

可參考預設的設定與說明：
`craft/core/app/etc/config/defaults/general.php`

## Multi-Environment Configs

`craft/config/general.php`:

```php
return array(
    'omitScriptNameInUrls' => true,
    'devMode' => ($_SERVER['SERVER_NAME'] == 'example.dev' ? true : false),
);
```

可以使用 `*` 來代表共通的設定:

```php
return array(
    '*' => array(
        'omitScriptNameInUrls' => true,
    )
);
```

接下來，依據不同的網域規則來決定不同的設定環境：

```php
return array(
    '*' => array(
        'omitScriptNameInUrls' => true,
    ),

    'example.dev' => array(
        'devMode' => true,
    ),

    'example.com' => array(
        'cooldownDuration' => 0,
    )
);
```

Craft 將會根據 `$_SERVER['SERVER_NAME']` 的值來決定該讀取哪一個設定環境。

> 你可以修改定義在 `index.php` 的 `CRAFT_ENVIRONMENT` 值來改變設定環境

因為 Craft 是用局部比對的方式來判斷網域，所以你可以用 Top-Level Domain 作為判斷依據：

```php
return array(
    '*' => array(
        'omitScriptNameInUrls' => true,
    ),

    '.dev' => array(
        'devMode' => true,
    ),

    '.com' => array(
        'cooldownDuration' => 0,
    )
);
```

### 多環境的資料庫設定

`craft/confgi/db.php`:

```php
return array(
    '*' => array(
        'tablePrefix' => 'craft',
    ),
    '.dev' => array(
        'server' => 'localhost',
        'user' => 'root',
        'password' => 'letmein',
        'database' => 'buildwithcraft',
    ),
    '.com' => array(
        'server' => 'localhost',
        'user' => 'av12345',
        'password' => '$uP3r$3jp3t',
        'database' => 'av12345-buildwithcraft',
    ),
);
```

### 環境自定義變數

```php
return array(
    '*' => array(
        // ...
    ),

    'example.dev' => array(
        // ...

        'environmentVariables' => array(
            'basePath' => '/users/brandon/Sites/example.dev/public/',
            'baseUrl'  => 'http://example.dev/',
        )
    ),

    'example.com' => array(
        // ...

        'environmentVariables' => array(
            'basePath' => '/storage/av12345/www/public_html/',
            'baseUrl'  => 'http://example.com/',
        )
    )
);
```

![environment variables](http://buildwithcraft.com/assets/images/docs/_527xAUTO_crop_center-center/environment-variables.2x.png)
