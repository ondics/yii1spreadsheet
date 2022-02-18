Yii1 Spreadsheet Extensions
===========================

Provides very easy Excel-Output for Yii1

* works with CArrayDataProvider
* works with CActiveDataProvider
* provides flexible value formatting with PHP closures (see below)

This yii1 extension is a light backport of https://github.com/yii2tech/spreadsheet to Yii1.


Tested with Yii1 version 1.1.25

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

## Credits

Thanks to https://patreon.com/klimov_paul and yii2tech which provide https://github.com/yii2tech/spreadsheet

## Author

githubler@ondics.de

(C) 2022, Ondics GmbH

