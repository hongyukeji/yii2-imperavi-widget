# Imperavi Redactor Widget for Yii 2

[![Latest Version](https://img.shields.io/github/tag/hongyukeji/yii2-imperavi-widget.svg?style=flat-square&label=release)](https://github.com/hongyukeji/yii2-imperavi-widget/releases)
[![Software License](https://img.shields.io/badge/license-BSD-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Build Status](https://img.shields.io/travis/hongyukeji/yii2-imperavi-widget/master.svg?style=flat-square)](https://travis-ci.org/hongyukeji/yii2-imperavi-widget)
[![Coverage Status](https://img.shields.io/scrutinizer/coverage/g/hongyukeji/yii2-imperavi-widget.svg?style=flat-square)](https://scrutinizer-ci.com/g/hongyukeji/yii2-imperavi-widget/code-structure)
[![Quality Score](https://img.shields.io/scrutinizer/g/hongyukeji/yii2-imperavi-widget.svg?style=flat-square)](https://scrutinizer-ci.com/g/hongyukeji/yii2-imperavi-widget)
[![Total Downloads](https://img.shields.io/packagist/dt/hongyukeji/yii2-imperavi-widget.svg?style=flat-square)](https://packagist.org/packages/hongyukeji/yii2-imperavi-widget)

`Imperavi Redactor Widget` is a wrapper for [Imperavi Redactor](http://imperavi.com/redactor/),
a high quality WYSIWYG editor.

Note that Imperavi Redactor itself is a proprietary commercial copyrighted software
but since Yii community bought OEM license you can use it for free with Yii.

## Install

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```bash
$ php composer.phar require --prefer-dist hongyukeji/yii2-imperavi-widget "*"
```

or add

```json
"hongyukeji/yii2-imperavi-widget": "*"
```

to the require section of your `composer.json` file.


## Usage

Once the extension is installed, simply use it in your code:

### Like a widget ###

```php
echo \hongyukeji\imperavi\Widget::widget([
    'name' => 'redactor',
    'settings' => [
        'lang' => 'zh_cn',
        'minHeight' => 200,
        'plugins' => [
            'clips',
            'fullscreen'
        ]
    ]
]);
```

### Like an ActiveForm widget ###

```php
use hongyukeji\imperavi\Widget;

echo $form->field($model, 'content')->widget(Widget::className(), [
    'settings' => [
        'lang' => 'zh_cn',
        'minHeight' => 200,
        'plugins' => [
            'clips',
            'fullscreen'
        ]
    ]
]);
```

### Like a widget for a predefined textarea ###

```php
echo \hongyukeji\imperavi\Widget::widget([
    'selector' => '#my-textarea-id',
    'settings' => [
        'lang' => 'zh_cn',
        'minHeight' => 200,
        'plugins' => [
            'clips',
            'fullscreen'
        ]
    ]
]);
```

### Add images that have already been uploaded ###

```php
// DefaultController.php
public function actions()
{
    return [
        'images-get' => [
            'class' => 'hongyukeji\imperavi\actions\GetAction',
            'url' => 'http://my-site.com/images/', // Directory URL address, where files are stored.
            'path' => '@alias/to/my/path', // Or absolute path to directory where files are stored.
            'type' => GetAction::TYPE_IMAGES,
        ]
    ];
}

// View.php
echo \hongyukeji\imperavi\Widget::widget([
    'selector' => '#my-textarea-id',
    'settings' => [
        'lang' => 'zh_cn',
        'minHeight' => 200,
        'imageManagerJson' => Url::to(['/default/images-get']),
        'plugins' => [
            'imagemanager'
        ]
    ]
]);
```

### Add files that have already been uploaded ###

```php
// DefaultController.php
public function actions()
{
    return [
        'files-get' => [
            'class' => 'hongyukeji\imperavi\actions\GetAction',
            'url' => 'http://my-site.com/files/', // Directory URL address, where files are stored.
            'path' => '@alias/to/my/path', // Or absolute path to directory where files are stored.
            'type' => GetAction::TYPE_FILES,
        ]
    ];
}

// View.php
echo \hongyukeji\imperavi\Widget::widget([
    'selector' => '#my-textarea-id',
    'settings' => [
        'lang' => 'zh_cn',
        'minHeight' => 200,
        'fileManagerJson' => Url::to(['/default/files-get']),
        'plugins' => [
            'filemanager'
        ]
    ]
]);
```

### Upload image ###

```php
// DefaultController.php
public function actions()
{
    return [
        'image-upload' => [
            'class' => 'hongyukeji\imperavi\actions\UploadAction',
            'url' => 'http://my-site.com/images/', // Directory URL address, where files are stored.
            'path' => '@alias/to/my/path' // Or absolute path to directory where files are stored.
        ],
    ];
}

// View.php
echo \hongyukeji\imperavi\Widget::widget([
    'selector' => '#my-textarea-id',
    'settings' => [
        'lang' => 'zh_cn',
        'minHeight' => 200,
        'imageUpload' => Url::to(['/default/image-upload'])
    ]
]);
```

### Upload file ###

```php
// DefaultController.php
public function actions()
{
    return [
        'file-upload' => [
            'class' => 'hongyukeji\imperavi\actions\UploadAction',
            'url' => 'http://my-site.com/files/', // Directory URL address, where files are stored.
            'path' => '@alias/to/my/path' // Or absolute path to directory where files are stored.
        ],
    ];
}

// View.php
echo \hongyukeji\imperavi\Widget::widget([
    'selector' => '#my-textarea-id',
    'settings' => [
        'lang' => 'zh_cn',
        'minHeight' => 200,
        'fileUpload' => Url::to(['/default/file-upload'])
    ]
]);
```

### Add custom plugins ###

```php
echo \hongyukeji\imperavi\Widget::widget([
    'selector' => '#my-textarea-id',
    'settings' => [
        'lang' => 'zh_cn',
        'minHeight' => 200,
        'plugins' => [
            'clips',
            'fullscreen'
        ]
    ],
    'plugins' => [
        'my-custom-plugin' => 'app\assets\MyPluginBundle'
    ]
]);
```

## Testing

``` bash
$ phpunit
```

## Further Information

Please, check the [Imperavi Redactor](http://imperavi.com/redactor/) documentation for further information about its configuration options.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Credits

- [Vasile Crudu](https://github.com/hongyukeji)
- [All Contributors](../../contributors)

## License

The BSD License (BSD). Please see [License File](LICENSE.md) for more information.

> <a href="http://yiiwheels.com"><img src="http://yiiwheels.com/img/logo-big.png" alt="YiiWheels" width="150" height="100" /></a>  
[Available also on YiiWheels](http://yiiwheels.com)
