# Php scrapper

Simple and Easy to Use . Includes HTTP class to make http requests  :)

```Php

<?php
error_reporting(E_ALL & ~E_NOTICE);
include_once("Http.php");
include_once('PhpDom.php');


// Example 1
$http = new HTTP();
$html = $http->get('https://www.webscraper.io/test-sites/e-commerce/allinone/computers');

$document = new PhpDom($html);
$prices = $document->find('div.card-body h4.price');
$titles = $document->find('div.card-body h4 a.title');
$images = $document->find('div.card-body img.image');
if($prices){
    for( $i = 0; $i < count($titles); $i++ ){
        $title = new PhpElement($titles[$i]);
        $price = new PhpElement($prices[$i]);
        $image = new PhpElement($images[$i]);
        
        $title = $title->text()."<br>";
        $price = $price->text() ."<br>";
        $image = $image->attr('src');

        echo "
          <div>
          <img  src='https://www.webscraper.io$image' width='200' height='200'/>
          <h2>
          $title
          </h2>
          <h3>$price</h3>
          </div>
        ";
    }
}else{
    echo 'No Price Found';
}


```