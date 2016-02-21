# RoxyMce - Beautiful File manager for Tinymce
This allow to integrate [TinyMce](https://github.com/tinymce/tinymce) 4 with [Roxy Fileman](http://roxyfileman.com)

User story
---
I'm try to find a good file manager for tinymce for a long time.  
elFinder is good, but too much function and it's not my style. MoxieManager maybe best with tinymce, but it's too much for me.  
One day, I saw roxyman, immediately, I know it is all I need.  
Install
---
Preferred way to install this extension through [composer](http://getcomposer.org)  
Either run
```
composer require navatech/yii2-roxymce "@dev"
```
Or add to `require` section of `composer.json` then run `composer update`
```
"navatech/yii2-roxymce" : "@dev" 
```
Configure
---
Just add to `config/web.php`
### Simple config
~~~
[php]
	'modules'    => [
		'roxymce'  => [
			'class' => '\navatech\roxymce\Module',
		]
	]
~~~
### Advanced config
~~~
[php]
	'modules'    => [
		'roxymce'  => [
			'class' => '\navatech\roxymce\Module',
			'config'=> [
			//all below is not required
				'FILES_ROOT'           => 'uploads/image', //The root directory of roxymce's resource, where can be uploaded to
				'DEFAULTVIEW'          => 'list', //default view when you call roxymce (thumb/list)
				'THUMBS_VIEW_WIDTH'    => '100', //default width of thumbs when thumb view activated
				'THUMBS_VIEW_HEIGHT'   => '100', //default height of thumbs when thumb view activated
				'MAX_IMAGE_WIDTH'      => '1000', //default maximum width of image allowed to upload
				'MAX_IMAGE_HEIGHT'     => '1000', //default maximum height of image allowed to upload
				'FORBIDDEN_UPLOADS'    => 'zip js jsp jsb mhtml mht xhtml xht php phtml php3 php4 php5 phps shtml jhtml pl sh py cgi exe application gadget hta cpl msc jar vb jse ws wsf wsc wsh ps1 ps2 psc1 psc2 msh msh1 msh2 inf reg scf msp scr dll msi vbs bat com pif cmd vxd cpl htpasswd htaccess', //default forbidden upload files extension
				'ALLOWED_UPLOADS'      => 'jpeg jpg png gif mov mp3 mp4 avi wmv flv mpeg', //default allowed upload files extension
				'FILEPERMISSIONS'      => '0644', //default file permissions
				'DIRPERMISSIONS'       => '0755', //default folder permissions
				'LANG'                 => 'en', //default language interface
				'DATEFORMAT'           => 'dd/MM/yyyy HH:mm', //default datetime format
				'OPEN_LAST_DIR'        => 'yes', //default roxymce will open last dir where you leave
			]
		],
	],
~~~
Usage
---
In your view file, call roxymce widget
### Include ActiveRecord Model
```
[php]
//example in action create
$model = new Post(); 
//example in action update
$model = Post::findOne(['id' => 1]); 
echo \navatech\roxymce\widgets\RoxyMceWidget::widget([
	'model'       => $model, //your Model, REQUIRED
	'attributess' => 'content', //attribute name of your model, REQUIRED if using 'model' section
	'name'        => 'Post[content]', //defaul name of textarea which will be generated, NOT REQUIRED if using 'model' section
	'value'       => isset($_POST['Post']['content']) ? $_POST['Post']['content'] : $model->content, //default value of current textarea, NOT REQUIRED
	'action'      => Url::to(['roxymce/default']), //default roxymce action route, NOT REQUIRED
	'options'     => [],//TinyMce options, NOT REQUIRED, see https://www.tinymce.com/docs/
	'htmlOptions' => [],//html options of this widget, NOT REQUIRED
]);
```
### Sample HTML without ActiveRecord Model
```
[php]
echo \navatech\roxymce\widgets\RoxyMceWidget::widget([
	'name'        => 'content', //defaul name of textarea which will be generated, REQUIRED if not using 'model' section
	'value'       => isset($_POST['content']) ? $_POST['content'] : '', //default value of current textarea, NOT REQUIRED
	'action'      => Url::to(['roxymce/default']), //default roxymce action route, NOT REQUIRED
	'options'     => [],//TinyMce options, NOT REQUIRED, see https://www.tinymce.com/docs/
	'htmlOptions' => [],//html options of this widget, NOT REQUIRED
]);
```
Screenshot & Demo
---
### Demo
Please referrence to [RoxyFileMan demo](http://www.roxyfileman.com/demo) and scroll down to TinyMce section
### Thumb view
![thumbview](http://i.imgur.com/mEascq0.png)
### List view
![listview](http://i.imgur.com/IkA92kK.png)
### Upload view
![upload](http://i.imgur.com/9zvpFTM.png)

Credits
---
Thanks to [TinyMce](http://tinymce.com), [RoxyFileMan](http://roxyfileman.com)
