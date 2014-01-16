Stripe - Payment Suite
=====

[![SensioLabsInsight](https://insight.sensiolabs.com/projects/b1e1520a-dab9-463e-9e9d-602c3e55a801/mini.png)](https://insight.sensiolabs.com/projects/b1e1520a-dab9-463e-9e9d-602c3e55a801)
[![Build Status](https://travis-ci.org/mmoreram/PaymillBundle.png?branch=master)](https://travis-ci.org/dpcat237/StripeBundle)
[![Scrutinizer Quality Score](https://scrutinizer-ci.com/g/dpcat237/StripeBundle/badges/quality-score.png?s=10dab38a47f5ca4c11a2de2e4f1237555c5e8660)](https://scrutinizer-ci.com/g/dpcat237/StripeBundle/)
[![Latest Stable Version](https://poser.pugx.org/dpcat237/stripe-bundle/v/stable.png)](https://packagist.org/packages/dpcat237/stripe-bundle)
[![Latest Unstable Version](https://poser.pugx.org/dpcat237/stripe-bundle/v/unstable.png)](https://packagist.org/packages/dpcat237/stripe-bundle)
[![Dependency Status](https://www.versioneye.com/user/projects/52c075aaec1375db6000015e/badge.png)](https://www.versioneye.com/user/projects/52c075aaec1375db6000015e)
[![Total Downloads](https://poser.pugx.org/dpcat237/stripe-bundle/downloads.png)](https://packagist.org/packages/dpcat237/stripe-bundle)

Table of contents
-----

1. [Install Payment Environment](https://github.com/mmoreram/PaymentCoreBundle/wiki/Configure-Payment-Environment)
2. [Creating StripeBundle](https://github.com/mmoreram/PaymentCoreBundle/wiki/Crating-payment-Platforms)
3. [Configuration](#configuration)
4. [Router](#router)
5. [Display](#display)
6. [Customize](#customize)
7. [Testing and more documentation](#testing-and-more-documentation)
8. [Contribute](http://github.com/mmoreram/PaymentCoreBundle/blob/master/Resources/docs/contribute.md)

About Stripe Bundle
-----

This bundle bring you a possibility to make simple payments through [Stripe](https://stripe.com). StripeBundle is payment method for Symfony2 Payment Suite and it's built following [PaymentCore](https://github.com/mmoreram/PaymillBundle) specifications. PaymentCore brings for developers easy way to implement several payment methods.

Configuration
-----

Configure the StripeBundle parameters in your `config.yml`.

``` yml
stripe:

    # stripe keys
    public_key: XXXXXXXXXXXX
    private_key: XXXXXXXXXXXX

    # By default, controller route is /payment/stripe/execute
    controller_route: /my/custom/route

    # Configuration for payment success redirection
    #
    # Route defines which route will redirect if payment success
    # If order_append is true, Bundle will append cart identifier into route
    #    taking order_append_field value as parameter name and
    #    PaymentOrderWrapper->getOrderId() value
    payment_success:
        route: cart_thanks
        order_append: true
        order_append_field: order_id

    # Configuration for payment fail redirection
    #
    # Route defines which route will redirect if payment fails
    # If cart_append is true, Bundle will append cart identifier into route
    #    taking cart_append_field value as parameter name and
    #    PaymentCartWrapper->getCartId() value
    payment_fail:
        route: cart_view
        cart_append: false
        cart_append_field: cart_id
```

About Stripe `public_key` and `private_key` you can learn more in [Stripe documentation page](https://stripe.com/docs/tutorials/dashboard#api-keys)

Router
-----

StripeBundle allows developer to specify the route of controller where stripe payment is processed.  
By default, this value is `/payment/stripe/execute` but this value can be changed in configuration file.  
Anyway StripeBundle's routes must be parsed by the framework, so these lines must be included into `routing.yml` file.

``` yml
stripe_payment_routes:
    resource: .
    type: stripe
```

Display
-----

Once your StripeBundle is installed and well configured, you need to place your payment form.

StripeBundle gives you all form view as requested by the payment module.

``` twig
{% block content %}

        <div class="payment-wrapper">

            {{ stripe_render() }}

        </div>

{% endblock content %}

{% block foot_script %}

    {{ parent() }}

    {{ stripe_scripts() }}

{% endblock foot_script %}
```


Customize
-----

`stripe_render()` just print a basic form.

As every project need its own form design, you can overwrite default form located in: `app/Resources/StripeBundle/views/Stripe/view.html.twig` following [Stripe documentation](https://stripe.com/docs/tutorials/forms).

In another hand, Stripe [recommend](https://stripe.com/docs/tutorials/forms#create-a-single-use-token) use [jQuery form validator](https://github.com/stripe/jquery.payment).


Testing and more documentation
-----
 
For testing you can use [these examples](https://stripe.com/docs/testing).
More detail about Stripe API you can find in this [web](https://stripe.com/docs/api/php).
