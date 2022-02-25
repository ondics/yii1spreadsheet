Yii1 Spreadsheet Extensions
===========================

Provides very easy Excel-Output for Yii1

* works with `CArrayDataProvider`
* works with `CActiveDataProvider`
* provides flexible value formatting with PHP closures (see below)

Tested with Yii1 version 1.1.25

## Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist ondics/yii1spreadsheet
```

or add

```json
"ondics/spreadsheet": "*"
```

to the `require` section of your composer.json.

## Usage

    $dataProvider = new CArrayDataProvider([
        [
            'name' => 'some name',
            'price' => '9879',
        ],
        [
            'name' => 'name 2',
            'price' => '79',
        ],
    ]);
    $exporter = new Spreadsheet();
    $exporter->dataProvider = $dataProvider;
    $exporter->columns = [
        'name',
        [
            'attribute' => 'price',
            'header' => 'Price with VAT',
            'value' => function($model,$key,$index,$x) {
                return $model->price * 1.19;
              },
              'visible' => ($model->price  > 20),
    ];
    $exporter->send('myexcelfile.xlsx');

## Application Notes

This yii1 extension is a light backport of https://github.com/yii2tech/spreadsheet to Yii1. Some ii2 base classes and freatures are provided
with this extensions and can be used during Excel export, e.g.

* In `colums` a closure can be used as value. This closue differs from the closure in Yii1. See the example above how to use this closure.
* The columns array is backported from Yii2 so see Yii2 docs for information

The `send` method cannot not use xsendfile to send a file directyle to the browser but has go over memory. This may affect very large Excel exports.

## Credits

Thanks to https://patreon.com/klimov_paul and yii2tech which provide https://github.com/yii2tech/spreadsheet

## Author

githubler@ondics.de

(C) 2022, Ondics GmbH

