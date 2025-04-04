# Introduction to Angular and modern design patterns

[Angular](https://angular.io) (aka Angular 2, 4, 5, 6...) is a new framework completely rewritten from the ground up,
replacing the now well-known [AngularJS](https://angularjs.org) framework (aka Angular 1.x).

More that just a framework, Angular should now be considered as a whole _platform_ which comes with a complete set of
tools, like its own [CLI](https://github.com/angular/angular-cli), [debug utilities](https://augury.angular.io) or
[performance tools](https://github.com/angular/angular/tree/master/packages/benchpress).

Angular has been around for some time now, but I still get the feeling that it’s not getting the love it deserved,
probably because of other players in the field like React or VueJS. While the simplicity behind these frameworks can
definitely be attractive, they lack in my opinion what is essential when making big, enterprise-grade apps: a solid
frame to lead both experienced developers and beginners in the same direction and a rational convergence of tools,
patterns and documentation. Yes, the Angular learning curve may seems a little steep, but it’s definitely worth it.

## Getting started

#### Newcomer

If you're new to Angular you may feel overwhelmed by the quantity of new concepts to apprehend, so before digging
into this project you may want to start with [this progressive tutorial](https://angular.io/tutorial) that will guide
you step by step into building a complete Angular application.

#### AngularJS veteran

If you come from AngularJS and want to dig straight in the new version, you may want to take a look at the
[AngularJS vs 2 quick reference](https://angular.io/guide/ajs-quick-reference).

#### Cheatsheet

Until you know the full Angular API by heart, you may want to keep this
[cheatsheet](https://angular.io/guide/cheatsheet) that resumes the syntax and features on a single page at hand.

## Style guide

This project follows the standard [Angular style guide](https://angular.io/guide/styleguide).

More that just coding rules, this style guide also gives advices and best practices for a good application architecture
and is an **essential reading** for starters. Reading deeper, you can even find many explanations for some design
choices of the framework.

## Going deeper

Even though they are not mandatory, Angular was designed for the use of design patterns you may not be accustomed to,
like [reactive programming](#reactive-programming), [unidirectional data flow](#unidirectional-data-flow) and
[centralized state management](#centralized-state-management).

These concepts are difficult to resume in a few words, and despite being tightly related to each other they concern
specific parts of an application flow, each being quite deep to learn on its own.

You will essentially find here a list of good starting points to learn more on these subjects.

#### Reactive programming

You may not be aware of it, but Angular is now a _reactive system_ by design.
Although you are not forced to use reactive programming patterns, they make the core of the framework and it is
definitely recommended to learn them if you want to leverage the best of Angular.

Angular uses [RxJS](http://reactivex.io/rxjs/) to implement the _Observable_ pattern.

> An _Observable_ is a stream of asynchronous events that can be processed with array-like operators.

##### From promises to observables

While AngularJS used to rely heavily on [_Promises_](https://docs.angularjs.org/api/ng/service/$q) to handle
asynchronous events, _Observables_ are now used instead in Angular. Even though in specific cases like for HTTP
requests, an _Observable_ can be converted into a _Promise_, it is recommended to embrace the new paradigm as it can a
lot more than _Promises_, with way less code. This transition is also explained in the
[Angular tutorial](https://angular.io/tutorial/toh-pt6#!%23observables).
Once you have made the switch, you will never look back again.

##### Learning references

- [What is reactive programming?](http://paulstovell.com/blog/reactive-programming), explained nicely through a simple
  imaged story _(5 min)_

- [The introduction to reactive programming you've been missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754),
  the title says it all _(30 min)_

- [Functional reactive programming for Angular 2 developers](http://blog.angular-university.io/functional-reactive-programming-for-angular-2-developers-rxjs-and-observables/),
  see the functional reactive programming principles in practice with Angular _(15 min)_

- [RxMarbles](http://rxmarbles.com), a graphical representation of Rx operators that greatly help to understand their
  usage

#### Unidirectional data flow

In opposition with AngularJS where one of its selling points was two-way data binding which ended up causing a lot of
major headaches for complex applications, Angular now enforces unidirectional data flow.

What does it means? Said with other words, it means that change detection cannot cause cycles, which was one of
AngularJS problematic points. It also helps to maintain simpler and more predictable data flows in applications, along
with substantial performance improvements.

**Wait, then why the Angular documentation have mention of a
[two-way binding syntax](https://angular.io/guide/template-syntax#binding-syntax-an-overview)?**

If you look closely, the new two-way binding syntax is just syntactic sugar to combine two _one-way_ bindings (a
_property_ and _event_ binding), keeping the data flow unidirectional.

This change is really important, as it was often the cause of performance issues with AngularJS, and it one of the
pillars enabling better performance in new Angular apps.

While Angular tries to stay _pattern-agnostic_ and can be used with conventional MV\* patterns, it was designed with
reactive programming in mind and really shines when used with reactive data flow patterns like
[redux](http://redux.js.org/docs/basics/DataFlow.html),
[Flux](https://facebook.github.io/flux/docs/in-depth-overview.html#content) or
[MVI](http://futurice.com/blog/reactive-mvc-and-the-virtual-dom).

#### Centralized state management

As applications grow in size, keeping track of the all its individual components state and data flows can become
tedious, and tend to be difficult to manage and debug.

The main goal of using a centralized state management is to make state changes _predictable_ by imposing certain
restrictions on how and when updates can happen, using _unidirectional data flow_.

This approach was first made popular with React with introduction of the
[Flux](https://facebook.github.io/flux/docs/in-depth-overview.html#content) architecture. Many libraries emerged then
trying to adapt and refine the original concept, and one of these gained massive popularity by providing a simpler,
elegant alternative: [Redux](http://redux.js.org/docs/basics/DataFlow.html).

Redux is at the same time a library (with the big _R_) and a design pattern (with the little _r_), the latter being
framework-agnostic and working very well with Angular.

The _redux_ design pattern is based on these [3 principles](http://redux.js.org/docs/introduction/ThreePrinciples.html):

- The application state is a _single immutable_ data structure
- A state change is triggered by an _action_, an object describing what happened
- Pure functions called _reducers_ take the previous state and the next action to compute the new state

The core concepts behind these principles are nicely explained in
[this example](http://redux.js.org/docs/introduction/CoreConcepts.html) _(3 min)_.

##### Which library to use?

You can make Angular work with any state management library you like, but your best bet would be to use
[@ngrx/store](https://github.com/ngrx/store). It works the same as the popular [Redux](http://redux.js.org) library,
but with a tight integration with Angular and [RxJS](http://reactivex.io/rxjs/), with some nice additional developer
utilities.

Here are some resources to get started:

- [Build a better Angular 2 application with redux and ngrx](http://onehungrymind.com/build-better-angular-2-application-redux-ngrx/),
  a nice tutorial for @ngrx/store _(30 min)_

- [Comprehensive introduction to @ngrx/store](https://gist.github.com/btroncone/a6e4347326749f938510), an in-depth
  walkthrough to this library usage in Angular _(60 min)_

##### When to use it?

You may have noticed that the starter template does not include a centralized state management system out of the box.
Why is that? Well, while there is many benefits from using this pattern, the choice is ultimately up to your team and
what you want to achieve with your app.

Keep in mind that using a single centralized state for your app introduces a new layer a complexity
[that might not be needed](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367), depending of your
goal.

## Optimizing performance

While the new Angular version resolves by design most of the performance issues that could be experienced with
AngularJS, there is always room for improvements. Just keep in mind that delivering an app with good performance is
often a matter of common sense and sane development practices.

Here is [a list of key points](https://github.com/mgechev/angular-performance-checklist) to check for in your app to
make sure you deliver the best experience to your customers.

After going through the checklist, make sure to also run an audit of your page through
[**Lighthouse**](https://developers.google.com/web/tools/lighthouse/), the latest Google tool that gives you meaningful
insight about your app performance, accessibility, mobile compatibility and more.
