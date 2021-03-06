インストール
============

インストールは二つの部分から成ります。すなわち、composer パッケージの取得と、アプリケーションの構成です。

## エクステンションをインストールする

このエクステンションをインストールするのに推奨される方法は [composer](http://getcomposer.org/download/) によるものです。

下記のコマンドを実行してください。

```
php composer.phar require --prefer-dist yiisoft/yii-twig
```

または、あなたの `composer.json` ファイルの `require` セクションに、

```
"yiisoft/yii-twig": "^3.0"
```

を追加してください。

## アプリケーションを構成する

Twig を使い始めるためには、`view` コンポーネントを下記のように構成する必要があります。

```php
[
    'view' => [
        '__class' => 'yii\web\View',
        'renderers' => [
            'twig' => [
                'class' => '__yii\twig\ViewRenderer',
                'cachePath' => '@runtime/Twig/cache',
                // Twig のオプションの配列
                'options' => [
                    'auto_reload' => true,
                ],
                'globals' => [
                    ['__class' => '\yii\helpers\Html'],
                ],
                'uses' => ['yii\bootstrap'],
            ],
            // ...
        ],
    ],
]
```

構成が終った後、拡張子 `.twig` を持つファイルにテンプレートを作成することが出来ます。
(別のファイル拡張子を使う場合は、それに応じてコンポーネントの構成を修正してください。)
通常のビュー・ファイルとは異なって、Twig を使用する場合は、コントローラで `$this->render()` を呼ぶときにファイル拡張子を含めなければなりません。

```php
return $this->render('renderer.twig', ['username' => 'Alex']);
```
