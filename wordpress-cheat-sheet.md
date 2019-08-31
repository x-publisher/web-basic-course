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

--------

### Wordpress Pagination
1. **posts_per_page** argument ထည့်ရမယ် `( e.g "posts_per_page" => 4 )`
2. **paged** argument ထည့်ရမယ် `( e.g "paged" => $paged )`
3. အောက်က **No 3** က codes ကို **endif;** အောက်မှာထည့်ပေးရမယ်

#### 1
```php
$args = array(
    'posts_per_page'=>4,
);
```

#### 2
```php

$paged = ( get_query_var( 'paged' ) ) ? get_query_var( 'paged' ) : 1;
$args = array(
    'paged'=> $paged,
);
```

#### 3
```php

  $total_pages = $query->max_num_pages;
  if ($total_pages > 1){
      $current_page = max(1, get_query_var('paged'));
      echo paginate_links(array(
          'base' => get_pagenum_link(1) . '%_%',
          'format' => '/page/%#%',
          'current' => $current_page,
          'total' => $total_pages,
          'prev_text'    => __('« prev'),
          'next_text'    => __('next »'),
      ));
  }  
  
```

------

## WP_QUERY

WP_Query ဆိုသည်မှာ wordpress posts တွေထဲမှာကိုယ်ထည့်ချင်တဲ့ဟာကို argument ဖြတ်ပြီးထည့်တဲ့ query ။ သူ့ကိုခေါ်သုံးမယ်ဆိုရင် `new WP_Query($arg)` 
လို့ရေးရမယ်။

ဥပမာ

```php
$arg = array(
    'post_type'=>'product', // product အမျိုးအစားကိုပဲရွေးမယ်
    'category__not_in'=> [1] // ID 1 ဆိုတဲ့ category ကိုပဲချန်ခဲ့မယ်
);

$query = new WP_Query($arg);
```

#### category အတွက် ဖြတ်နိုင်တဲ့ argument များ

* cat (int): ခေါ်သုံးမယ့် category (နံပါတ်)
* category_name (string): ခေါ်သုံးမယ့် category (နာမည်)
* category__and (array): ခေါ်သုံးမယ့် category ပေါင်း (နံပါတ် အစုလိုက်)
* category__in (array): ခေါ်သုံးမယ့် category များ (နံပါတ် အစုလိုက်)
* category__not_in (array): ဖြုတ်မယ့် category များ (နံပါတ် အစုလိုက်)

#### tag အတွက် ဖြတ်နိုင်တဲ့ argument များ

* tag (string): ခေါ်သုံးမယ့် tag (နာမည်)
* tag_id (int): ခေါ်သုံးမယ့် tag (နံပါတ်)
* tag__and (array): ခေါ်သုံးမယ့် tag ပေါင်း (နံပါတ်အစုလိုက်)
* tag__in (array): ခေါ်သုံးမယ့် tag များ (နံပါတ်အစုလိုက်)
* tag__not_in (array): ဖြုတ်မယ့် tag များ (နံပါတ်အစုလိုက်)
* tag_slug__and (array): ခေါ်သုံးမယ့် tag ပေါင်း (slug နာမည်အစုလိုက်)
* tag_slug__in (array): ခေါ်သုံးမယ့် tag များ (slug နာမည်အစုလိုက်)

