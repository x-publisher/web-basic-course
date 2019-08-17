# Wordpress CheatSheet - မြန်မာ version
-------
### Theme creation
theme create လုပ်မယ်ဆို
အဓိက ပါရမယ့်  file ၃ ခု
```plaintext
index.php  
screenshot.png // size က 1200 px X 900 px ရှိရမယ်
style.css <=== style ထဲမှာ Theme နာမည်တွေ info တွေ ထည့်ရမယ်
```
--------
### wordpress loop
```php
 <?php if (have_posts() ) : while (have_posts() ) : the_post();
 
  // title,content,excerpt,tags,category,author,date,permalink,author_bio
  
  endwhile; else : ?>
		<p><?php esc_html_e( 'Sorry, There is no post' ); ?></p>
  <?php endif; ?>
```
------
### the and get
အကယ်လို့  the  ဆိုရင်  echo ရိုက်စရာမလိုဘူး
အကယ်လို့  get ဆိုရင် echo ရိုက်ပါ  (မှတ်ချက် PHP echo ထည့်ရမည်)
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
### Argument ဖြတ်ခြင်း

```php
    $args = array(
		'posts_per_page'=>'8', // post ၈ ခုပဲပြမယ်
	 );

	$query = new WP_Query( $args );
	
	// အောက်မှာ loop ကို ပြန်ချိတ်နည်း
	
 if ( $query->have_posts() ) : while ( $query->have_posts() ) : $query->the_post(); ?>
 
```
------
### URL များ
`get_template_directory_uri()` // theme folder URL
`get_stylesheet_uri()` // style.css URL

-----
### custom page ချိတ်ခြင်း
1. `page-{ကိုယ့် page နာမည်}.php` တစ်ခု create လုပ်ရမယ်
2. file ရဲ့ထိပ်နားမှာ `Template Name: Home Page` ကို comment အနေနဲ့ ထည့်ရမယ်
3. backend က page update setting နားမှာ page attribute ဆိုတာရှိတယ် အဲဒီအောက်က default template ကိုပြောင်းချိတ်ပေးရမယ်


#### 2 ရဲ့    ဥပမာ
```php
<?php
/*
// Template Name: Home Page
*/
```
---------
### Header နှင့် Footer 
`wp-head()` နှင့် `wp-footer()` သည် wordpress original codes တွေပါလာတဲ့ function ဖြစ်တယ်

`get_header()` နင့် `get_footer()`  နှင့်မမှားစေရန် သတိပြုပါ။
`get_header()` နင့် `get_footer()` ဆိုတာ ကိုယ် create  လုပ်ထားတဲ့ header.php နှင့် footer.php file တွေပဲဖြစ်ပါတယ်။

-------
### Feature Image ထည့်

Feature image ထည့်မယ်ဆို functions.php ထဲမှာ ဒီ code လေးထည့်ရမယ်
```php
add_theme_support( 'post-thumbnails' ); 
```
-------

### Custom Field ထည့်

add new post ရဲ့ အပေါ်က screen options ထဲမှာ custom field ကိုသွားပြီး အမှန်ခြစ်ပေးရတယ်


**ပြန်ခေါ်သုံးမယ်ဆိုရင်**

```php
<?php echo get_post_meta(get_the_ID(), 'နာမည်', TRUE); ?>
```

-------

### Wordpress Migration ( Wordpress ရွှေ့ခြင်း )

1. database ထုတ်မယ်
2. **wp-content** ကိုကူးမယ်
3. **config.php** ထဲမှာ database user password တွေပြောင်းမယ်
4. database -> wp-options ထဲက **site url** နဲ့ **home url** ကိုပြောင်းပေးရမယ်


