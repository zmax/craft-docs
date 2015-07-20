# 設定

## General Config Settings

## Multi-Environment Configs

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

> 你可以改變定義在 `index.php` 的 `CRAFT_ENVIRONMENT` 的值來改變設定環境

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