For this challenge, I had to execute XXE attack.

### Understanding the website

To know where to inject the XXE code, we have to first understand how the website works. 

First you go to the website, click on a product you're interested in and you add it to your wishlist which gets registered as "wish #\_" which in this case is wish #21. Then you go to your cart and checkout after entering the address.

### Burp Suite

To intercept the HTTP requests, we use a tool called Burp Suite. After the initial setup, we can see the GET requests being made to the website when we carry out the same functions. When we add an item to our wishlist, we can see a POST wishlist.php log which contains the following XML code - 

```
<wishlist>
  <user_id>1</user_id>
     <item>
       <product_id>1</product_id>
     </item>
</wishlist>
```

We can see the id of the product we've added to our wishlist here. Since `libxml_disable_entity_loader(_)` is false, we can load external entities into it which allows for an XXE attack. The following lines are added to the first two lines and the product id number is changed to `&payload;` to get the desired response.

```
<!--?xml version="1.0" ?-->
<!DOCTYPE foo [<!ENTITY payload SYSTEM "/etc/hosts"> ]>
```

We can see in the responses the contents of the `/etc/hosts` file. 

Since the XXE injection was successful, we can try to do more and look at people's wishes. Generally, the path for webpages of a website are in `/var/www/html`. To try and get the details of the wishes (which was only accessible to the admins), we can replace `/etc/hosts` with `/var/www/html/wishes/wish_1.txt` for wish #1. It works, so we can do the same for the wishes that follow.

### The flags

After sifting through the wishes, I found one of the flags in wish #15 which was `THM{Brut3f0rc1n6_mY_w4y}`.

After looking at the CHANGELOG webpage in the website, I found the second flag - `THM{m4y0r_m4lw4r3_b4ckd00rs}`.
