# Heading for Step 2

Now we can access the Wordpress in port 20080 by accessing the following link:
https://[[HOST_SUBDOMAIN]]-20080-[[KATACODA_HOST]].environments.katacoda.com

1.	Wordpress Setup:
We first set up the wordpress account with username `user` and password `user`. Other details can be filled in your interest.
![wordpress_account_setup](./assets/wordpress_account_setup.png)

2.	User account creation:
Then we go to login with the `user` credentials. 
Choose `Users -> Add New` from the left panel.
We setup another user with username `malicioususer`, password `malicioususer` and role `subscriber`.
![malicious_account_setup](./assets/malicious_account_setup.png)
We also setup another user with username `victimuser`, password `victimuser` and role `subscriber`.
![victim_account_setup](./assets/victim_account_setup.png)
These accounts will be used later for demo use.

3. WooCommerce plugin setup:
Choose `Plugins -> Add New` from the left panel.
Search `WooCommerce`, and select `Install Now` and `Activate` after installation.
Then it will be redirected to the WooCommerce setup page.
Enter other details can be filled in your interest, except those specified below:
Choose `Fashion, apparel, and accessories` in Step 2.
![woocommerce_setup_step2](./assets/woocommerce_setup_step2.png)
Choose `Physical Products` in Step 3.
![woocommerce_setup_step3](./assets/woocommerce_setup_step3.png)
Choose `1-10` in `How many products do you plan to display?`, `No` in `Currently selling elsewhere?`, 
and uncheck `I'm setting up a store for a client` in Step 4.
![woocommerce_setup_step4](./assets/woocommerce_setup_step4.png)
Uncheck `Add recommended business features to my site` in Step 5.
![woocommerce_setup_step5](./assets/woocommerce_setup_step5.png)
Press `Continue'.
Select `Storefront` and press `Choose`.
In left panel, choose `WooCommerce -> Home`.
Choose `Add my products`, `Start with a template`, `Physical product`.
Enter the product name `T-Shirt`.
![product_setup](./assets/product_setup.png)

Now, we finished the setup of Wordpress part.