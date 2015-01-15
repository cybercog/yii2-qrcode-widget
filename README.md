yii2-uploadify-widget
=====================

composer.json
-----
```json
"require": {
        "xj/yii2-uploadify-widget": "*"
},
```

example:
-----
Widgetֱ������QR
-----
```php
use xj\qrcode\QRcode;
use xj\qrcode\widgets\Text;
use xj\qrcode\widgets\Email;
use xj\qrcode\widgets\Card;

//Widgetֱ������QR
Text::widget([
    'outputDir' => '@webroot/upload/qrcode',
    'outputDirWeb' => '@web/upload/qrcode',
    'ecLevel' => QRcode::QR_ECLEVEL_L,
    'text' => 'test',
    'size' => 6,
]);

//Widgetͨ��Action����QR
Text::widget([
    'text' => 'aaaa@gmail.com',
    'size' => 3,
    'margin' => 4,
    'ecLevel' => QRcode::QR_ECLEVEL_L,
]);

//����һ��EMAIL��ά��
Email::widget([
    'email' => 'aaaa@gmail.com',
    'subject' => 'myMail',
    'body' => 'do something',
]);

//��Ƭ
Card::widget([
    'actions' => ['clientQrcode'],
    'name' => 'SB',
    'phone' => '1111111111111',
    //here jpeg file is only 40x40, grayscale, 50% quality! 
    'avatar' => '@webroot/avatar.jpg',
]);

//SMS����
Smsphone::widget([
    'actions' => ['clientQrcode'],
    'phone' => '131111111111',
]);
//Tel��绰
Telphone::widget([
    'actions' => ['clientQrcode'],
    'phone' => '131111111111',
]);

```

Widget��������URL+IMG ͨ��Action��Ⱦ
----
Action:
----
```php
public function actions() {
    //deny widget set size & margin & ecLevel
    'qrcode' => [
        'class' => QRcodeAction::className(),
        'enableCache' => false,
        //
        'allowClientEclevel' => false,
        'ecLevel' => QRcode::QR_ECLEVEL_H,
        //
        'defaultSize' => 4,
        'allowClientSize' => false,
        //
        'defaultMargin' => 2,
        'allowClientMargin' => false,
    ],

    //allow widget set size & margin & ecLevel
    'qrcode' => [
        'class' => QRcodeAction::className(),
        //you can disable cache
        'enableCache' => true,
        //
        'allowClientEclevel' => true,
        'ecLevel' => QRcode::QR_ECLEVEL_H,
        //
        'defaultSize' => 4,
        'allowClientSize' => true,
        'maxSize' => 10,
        //
        'defaultMargin' => 2,
        'allowClientMargin' => true,
        'maxMargin' => 10,
        'outputDir' => '@webroot/upload/qrcode',

        //closure, you can ignore this selection.
        'onGetFilename' => function (QRcodeAction $data) {
            /* @var $data QRcodeAction */
            //dosomething
            return sha1($data->text) . '.png';
        }
    ],
}
```
