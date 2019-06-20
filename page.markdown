# Can you Migrate any Legacy Code under 1 Month?
###### by Tomas Votruba

> According to [PHP Framework Trends](https://www.tomasvotruba.cz/php-framework-trends/#table) from Packagist there is over 1 258 million downloads of open-source PHP frameworks for the last 12 months. That's a great number! But how many of them are on the latest version? How many of them are stuck on version 0 or 1, that is not even on packagist? And how many of you have custom PHP framework, that you just hate? What if I tell you there is a way you all could use the latest version of your favorite framework and PHP 7.4 by the end of 2019? 

## Every PHP Framework is Dying

It all beings in a small country in the center of Europe - the Czech Republic. You might have heard about us thanks to Nette, PHPStan, or few Doctrine and Symfony contributors. 

Nette is a PHP framework that was released in 2008 and is used mostly by Czech companies. If you never heard about it, the very raw description would be "close to Symfony in features and Laravel in simplicity".

Now, the problem with the software it gets very old very fast. Do you remember the release of PHP 5.3 in June 2009? This "namespace" thing, what a cool feature, I really loved it. Now it's 2019 and nobody who cares. This is a natural process of life. Or would you prefer PHP 5.3 to be the last PHP version ever? 
 
> "Once you stop learning you start dying."
> _Albert Einstein_

PHP frameworks are also software. They get old, there is a better version of it or there is this other framework, that has clearer API, follows a recent trend and is easy to learn. 
So instead of "Nette" in this post, you can imagine Symfony 1/2/3, Doctrine 1, Zend 1/2, Laravel 3/4, PHP 5.3, 5.4... and so on.

I'll use Nette because that's the first project we migrate under... well, I'll tell you later the exact number of days.

Also, I'll use Symfony as a go-to project, because that's my personal preference. Replace it with your personal favorite framework.

## What We Did?

Now we know about the natural process of software life-cycle, so let's get technical!

We migrate [Entry.do](https://entry.do/) project - API application built on controllers, routing, Kdyby integrations of Symfony and Doctrine. The application has been running in production for the last 4 years. We migrated it from Nette 2.4 to Symfony 4.2.

![Figure 1: Entrydo website](figures/figures1.png)

### How big it is? 

Honestly, with pattern refactoring the size doesn't matter, but people tend still tend to care about it. 

If we don't count tests, migration, fixtures, etc., the application has **270 PHP files** in the length of **54 357 lines** (without comments, using [phploc](https://github.com/sebastianbergmann/phploc)).

To give you an idea, the Laravel 5.8 has 72 519 lines (without comments) at the time of writing this post. 

If you're like me, you better understand the business logic "size", like routes - this application had **151 unique routes**.

## Why we did it?

The application was written in Nette, which worked and met the technical requirements in the past.
 The main motivation for the transition **was the dying Nette ecosystem** and that over-integration of Symfony. 
 
 What does "dying ecosystem" mean? Nette released just 1 minor version since July 2016, while Symfony had **6 releases** during the same period. Also, the most promoted new feature of upcoming Nette 3.0 was added type declaration of PHP 7.1, which is not really a framework feature and only adds maintenance work.

The Entrydo project needed to developer faster, more reliable way and with less code. In an ecosystem, that is alive and kicking. 
 
## How we did it?

I offered [Honza Mikeš](http://github.com/JanMikes) a deal he couldn't refuse: 

> "We will give it a week and if we feel stuck, we'll give up soon enough".

This sentence contains 3 basic rules for successful migration of a huge project that you have to set beforehand.

### 1. Fast and Deadlined

If you have a year to write a prototype for your new startup, it will take a year. If you have a week, it will take a week.

That's why we picked 1 week as a soft deadline and 1 month as a hard deadline. If we're not finished in 1 month of work, we're closing it.   

### 2. Human Independent

Have you ever migrated or upgraded huge project? I bet you've picked full-rewrite or step-by-step refactoring, right? **I admit, I did too, but it's a complete non-sense way to refactor huge applications**.

Both of these approaches depend on human, their skills and their speed to refactor. Even if you have a team of 5 super smart developers, a manual rewrite of 10 000 000 lines of code might take them at least a year. They would tell you it's done in 3 months, but you know how it goes with developers and estimates. 

Instead, you have to think about the way based on machine-time. It's not that popular, even though it was mentioned in _Pragmatic programmer_ book.

I call it [pattern refactoring](https://www.tomasvotruba.cz/blog/2019/04/15/pattern-refactoring/) since it focuses on patterns in code, rather in size, version of the language. A pattern can be service locator, another pattern is constructor injection.

**A pattern refactoring is**... that's right: services locator to constructor injection. Does it sound hard? There is actually 4-5 way to use service locator and 2 to use constructor injection. Once you've had them covered in automated migration, you just run the scripts and it works on all the PHP code in the world, forever :). 

That sound crazy, right? Keep on reading.    

### 3. In Cooperation with Business

I think this is the #1 reason why these migrations don't happen more often.

Programmers speak about migration as something "must have" and "needed" **for them**:

- "It's dangerous to use PHP 5.3, there might be security issues."
- "PHP 7.0 is twice faster as PHP 5.6, we should upgrade"
- "We should upgrade to the Symfony 4, it has some cool new features"
- "It might take months and bring 0 value to the business..."

If I'd own the business, all I could hear would be "we want to play, give us your money for an uncertain amount of time and you'll get nothing at return".   
 
That's the problem, as programmers, we only get money for the time spent at work. When we go home after 5 PM, we don't care if the business will last next summer. 

We care about ourselves. We pay rent and expect to live the for next year with the same quality, we pay for Spotify and expect it to give us enjoyable songs for the long term. **The business owner is like us - they pay us monthly and expect long term sustainability**.

### How to be One with the Business?

Rector is not a tool to play and migrate code just because it can. **It needs to bring value to the business.**

That's why we need a mind shift from "must have" to "it's better":

- "When we migrate from Zend 1 to Symfony 4 in 30 days, we'll lose a month of work of 2 people, but the delivery of our task will drop from 4 hours to 30 minutes. In 3 month we have it paid and then we only profit."
- "When we use Symfony, it will be easier to hire new developers. Last month we had a meeting with 1 Zend developer, but 6 Symfony developers."
- "The Symfony community is much more active then Zend in our country, in numbers 12 meetups a year to 0 meetups. It will be easier to learn and to share our know-how there, that will eventually bring us more developer, better team and code quality... therefore, cheaper feature delivery" 

Having all this in mind, we started to migration from Nette to Symfony.

## Instant Migration with Rector

What were the patterns we needed to migrate?

- NEON to YAML
- Latte to Twig
- Presenter to Controller

~~~~diff
<?php declare (strict_types = 1);
 
-namespace App\Presenter;
+namespace App\Controller;
 
-use Nette\Application\AI\Presenter;
+use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
-use Nette\Http\Request;
+use Symfony\Component\HttpFoundation\Request;

-final class SomePresenter extends Presenter
+final class SomeController extends AbstractController
 {
-    public static function someAction()
+    public static function someAction(Request $request)
     {
-        $header = $this-> httpRequest-> getHeader('x');
+        $header = $request-> headers-> get('x');

-        $method = Request::POST;
+        $method = Request::METHOD_HPOST
     }
 }
~~~~

- move routes from single `RouteFactory` class to `@Route` annotation per Controller `__invoke()` action

~~~~diff
 <?php

 namespace App;
 
 use Entrydo\RestRouteList;
 use Entrydo\Restart;

 final class RouterFactory
 {
-    private const PAYMENT_RESPONSE_ROUTE = '/ payment / process';
     // 150 more!
     
     public function create()
     {
         $router = new RestRouteList();
-        $router[] = RestRoute::get(self::PAYMENT_RESPONSE_ROUTE, ProcessGPWebPayResponsePresenter::class);
          // 150 more!
          
          return $router;
      }
 }
~~~~

~~~~diff
 namespace App Presenter;
  
+use Symfony\Component\Routing\Annotation\Route;
  
 final class ProcessGPWebPayResponsePresenter
 {
+    /**
+     * @Route(path = "/payments/gpwebpay/process-response", methods="GET"})
+     */
     public function __invoke()
     {
         // ...
     }
 }
~~~~   

- change few `new <Object>`s to services

~~~~diff
 <?php

 class SomePresenter
 {
+    /**
+     * @var ResponseFactory
+     */
+    private $responseFactory;
+
+    public function __construct(ResponseFactory $responseFactory)
+    {
+        $this->responseFactory = $responseFactory;
+    }   
+
     public function someAction()
     {
-        return new OKResponse($response);
+        return $this->responseFactory->createJsonResponse($response);
     }
 }
~~~~

None of these changes were done manually. We're too lazy for that.

## How Long it Took?

On the January 27th, 2019, we met above Nette application and on February 13th, 2019 the Symfony application went to the staging server. On February 14th we celebrated a new production application in addition to Valentine's Day.

- **In less than 17 days we were done**. Done, finished, deployed, goodbye.

You're counting the estimate... 17 * 40 * 2... stop, I'll count it for you: 

- 2 * 40 hours = **80 hours**.

Roughly 50 hours took us to prepare the pattern set and 10 hours to debug one event race-condition. Now the migration of similar project would take us 15-20 hours. 

## How you can do it?

There is 0-chance you have a Nette project that you want to migrate to Symfony, but just in case, the migration set in Rector is ready. [Just use it](https://github.com/rectorphp/rector/blob/master/config/set/framework-migration/nette-to-symfony.yaml):

~~~~
vendor/bin/rector process src --set nette-to-symfony
~~~~

It's not perfect since you'll have to cover edge cases that are specific only to your code, but it will save you 80 % of the boring work, that is typical for this migration.

<br>

In the next post, I'll teach you about pattern refactoring with Rector and how you can use it to migrate any PHP code you have now to your dream code.