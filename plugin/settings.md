# Plugin Settings

在 `plugins` 資料夾中建立一個 *plugin name* 資料夾, 例如 `beyond`

並建立 plugin 的 enterpoint file, 名稱需以 `Plugin` 結尾:

例如: `BeyondPlugin.php`

```php
<?php
namespace Craft;

/**
 * @author Starck Lin
 * @version 0.1
 */
class BeyondPlugin extends BasePlugin {

    public function getName()
    {
        return Craft::t('Beyond Plugin');
    }

    /**
     * Returns the plugin’s version number.
     *
     * @return string The plugin’s version number.
     */
    public function getVersion()
    {
        return "1.0";
    }

    /**
     * Returns the plugin developer’s name.
     *
     * @return string The plugin developer’s name.
     */
    public function getDeveloper()
    {
        return "beyond inc.";
    }

    /**
     * Returns the plugin developer’s URL.
     *
     * @return string The plugin developer’s URL.
     */
    public function getDeveloperUrl()
    {
        return "beyond.tw";
    }

}
```

進入 Craft CP 後, 到 Plugin 設定就會看到如下:

![](/content/images/2015/03/-----2015-03-27-16-08-45.png)


<hr/>

## Plugin Settings

```php
// 定義資料的型態
protected function defineSettings()
{
    return array(
    	// categories 為 settings 的某個 key
        // 並定義其值型態
        'categories' => array(
        	AttributeType::Mixed,
            'default' => array(
        		'Sours', 'Fizzes', 'Juleps'
            )
    	),
	);
}

// 取得 Plugin 設定頁面的 html 內容
public function getSettingsHtml()
{
	// craft 會去尋找 plugins/beyond/templates/settings.html 這個 template
    // 並代入 settings 變數後 render 其結果回傳 html 文字內容
	return craft()->templates->render('beyond/settings', array(
		'settings' => $this->getSettings()
	));
}

// 當表單發送後, 可以在儲存前修改 settings 的資料內容
public function prepSettings($settings)
{
	// Modify $settings here...
	return $settings;
}
```
