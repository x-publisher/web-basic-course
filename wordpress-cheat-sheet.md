# Wordpress CheatSheet - ျမန္မာ version
-------
### Theme creation
theme create လုပ္မယ္ဆို
အဓိက ပါရမယ့္  file ၃ ခု
```plaintext
index.php  
screenshot.png // size က 1200 px X 900 px ရွိရမယ္
style.css <=== style ထဲမွာ Theme နာမည္ေတြ info ေတြ ထည့္ရမယ္
```
--------
### wordpress loop
```php
 if (have_posts() ) : while (have_posts() ) : the_post(); ?>
  // title,content,excerpt,tags,category,author,date,permalink,author_bio
  <?php endwhile; else : ?>
		<p><?php esc_html_e( 'Sorry, There is no post' ); ?></p>
  <?php endif; ?>
```
------
### the and get
အကယ္လို႔  the  ဆိုရင္  echo ရိုက္စရာမလုိဘူး
အကယ္လို႔  get ဆိုရင္ echo ရိုက္ပါ  (မွတ္ခ်က္ PHP echo ထည့္ရမည္)
ဥပမာ

##### the
```php
the_title();
the_author();
```

##### Get
```php
echo get_title();
echo get_the_author();
```
------
### Argument ျဖတ္ျခင္း

```php
    $args = array(
		'posts_per_page'=>'8', // post ၈ ခုပဲျပမယ္
	 );

	$query = new WP_Query( $args );
	
	// ေအာက္မွာ loop ကို ျပန္ခ်ိတ္နည္း
	
 if ( $query->have_posts() ) : while ( $query->have_posts() ) : $query->the_post(); ?>
 
```
------
### URL မ်ား
`get_template_directory_uri()` // theme folder URL
`get_template_stylesheet_uri()` // style.css URL
-----
### custom page ခ်ိတ္ျခင္း
1. `page-{ကိုယ့္ page နာမည္}.php` တစ္ခု create လုပ္ရမယ္
2. file ရဲ႕ထိပ္နားမွာ `Template Name: Home Page` ကို comment အေနနဲ႔ ထည့္ရမယ္
3. backend က page update setting နားမွာ page attribute ဆိုတာရွိတယ္ အဲဒီေအာက္က default template ကိုေျပာင္းခ်ိတ္ေပးရမယ္


#### 2 ရဲ႕    ဥပမာ
```php
<?php
/*
// Template Name: Home Page
*/
```
---------
### Header ႏွင့္ Footer 
`wp-head()` ႏွင့္ `wp-footer()` သည္ wordpress original codes ေတြပါလာတဲ့ function ျဖစ္တယ္

`get_header()` နင့္ `get_footer()`  ႏွင့္မမွားေစရန္ သတိျပဳပါ။
`get_header()` နင့္ `get_footer()` ဆိုတာ ကိုယ္ create  လုပ္ထားတဲ့ header.php ႏွင့္ footer.php file ေတြပဲျဖစ္ပါတယ္။

-------





