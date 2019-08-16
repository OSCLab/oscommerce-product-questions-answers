# Product Questions & Answers - osCommerce add-on

An absolutely simple way to establish reliable relations with your potential customers providing them the possibility to ask questions about any product in your osCommerce store.

* Get details of visitor who has asked question about product.
* Answer it, post it on product page and send answer to visitor via email.
* Answer of question posted on product page will update the page with fresh content and so SEO will improve.

Compatible With:

* Community Edition version: All 
* Official version: 2.3.4+ (catalog design is not supported)
* Minimum PHP Version: 7.0

## Installation

1. Backup all files and database!

2. Unzip the archive and upload the files on server.

3. Manually make changes.

In admin/customers.php 

After

```php
       if (isset($cInfo->number_of_reviews) && ($cInfo->number_of_reviews) > 0) $contents[] = array('text' => '<br />' . tep_draw_checkbox_field('delete_reviews', 'on', true) . ' ' . sprintf(TEXT_DELETE_REVIEWS, $cInfo->number_of_reviews));
```

Add

```php
       $contents[] = tep_get_customers_number_questions_answers($cInfo->customers_id); // products questions answers add-on
```

In admin/includes/application_top.php and includes/application_top.php

At the end of the file add

```php
  require 'includes/functions/questions_answers.php'; // products questions answers add-on
```

In admin/includes/functions/general.php

After

```php
     tep_db_query("delete from " . TABLE_REVIEWS . " where products_id = '" . (int)$product_id . "'");
```

Add

```php
     tep_db_query("delete from questions_answers where products_id = '" . (int)$product_id . "'"); // products questions answers add-on
```

In admin/includes/languages/english/customers.php

At the end of the file add

```php
// start products questions answers add-on
  define('TEXT_DELETE_QUESTIONS', '%s question(s) and all answers');
  define('TEXT_DELETE_ANSWERS', '%s answer(s)');
// end products questions answers add-on
```

In product_info.php

After

```html
  </form>
```
Add

```html
  <div class="row is-product">
    <?php echo $oscTemplate->getContent('product_info_bottom'); ?>
  </div>
```

4. Open Administration Tool (Backend) in menu Catalog click Questions Answers Start

5. Install module:

- in menu "Modules" -> "Content" -> button "Install Module" -> select "Questions & Answers To Product" (group product_info_bottom) -> button "Install Module"
