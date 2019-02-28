# Core Concepts

## Unidirectional Data Flow

Betbook FE architecture is built on top of [Redux](https://redux.js.org/) and, therefore, revolves around a strict [_unidirectional data flow_](https://redux.js.org/basics/data-flow).

## Logic-Less UI

All components in our application are intended for presentational purposes only. We are trying to avoid encapsulating any business-logic within them. Community usually call them _dumb components_.

The structure of the components should, of course, reflect the real models \(e.g. game events, bets history, user balance, etc.\), but many of them are really _atomic_ and can be re-used multiple times both in our and in any other team's application. Such components have been moved to a separate sub-project - [Betbook UI Kit](http://TDB.com).

Any data retrieval logic and/or UI events \(e.g. mouse clicks, key presses, scroll events\) handling should reside in [selectors](../selectors/) and [behaviors](../behaviors.md), correspondingly.

## Normalized Application State

Most of the UI applications are usually split into tons of components, each of which requires its own view-model. This could lead to a mess in the overall application data structure.

For instance, you have two view-models: one for My Account page and another - for a small user box with a name and a balance in the site header. On each data update \(balance or user name\) you have to update both of these models. Developers usually tend to create separate reducers, that handle these changes, update the state and pass this data to the components.

While this approach fully decouples your components and their state, in a long run you will eventually face with a big problem: you'll have to handle all events, related to your domain model, in all of your view-models \(or reducers\). This will eventually lead to the code duplication, poor code maintainability and unpredictable side-effects.

In order to eliminate this problem, we decided to store all domain models in a [normalized state](https://redux.js.org/recipes/structuring-reducers/normalizing-state-shape). Each reducer in our application only handles actions, related to some particular domain model \(e.g. user\). We are trying to completely avoid handling actions from another domain.

This way, we can be sure, that our original \(pure\) domain models contain valid data and this data can be represented identically by any UI component. Query layer in our application contains a lot of selectors, so that complex components can fetch all required data from different domain models and project it to any suitable structure.

## Decoupled Data Access Layer

One of the most challenging issues in modern applications is a client-server communication. Very often contracts change or data structure received from server doesn't fully fit UI needs. Some fields might be missing, have wrong or outdated names, contain wrong values or be of incorrect data-types. This leads to a hell of various mappers, proxies, converters and formatter throughout the code.

In order to make the application logic clearer, we decided to move as much of these routines as possible to a separate layer. These routines might be implemented as re-usable helper function, inline formatter, etc.. They can reside in a dedicated modules or right within services, that perform data fetching.

The main idea is to keep the internal application state consistent and well-structured. This state should be optimized for UI only.

## Reactive Business Logic

Due to the nature of the target application \(betting platform\) we cannot fully rely on classic behavior management approach forced by [FLUX](https://facebook.github.io/flux/) architecture principles. A lot of side effects occur in such application like ours. For instance, when user tries to place a bet, the following events might be triggered at the same time:  
 - odds get changed;  
 - game event gets removed;  
 - self restriction rules are applied and user gets signed out;  
 - etc..

In order to handle such complicated flows we have to utilize reactive approach using [redux-observable](https://redux-observable.js.org/) library, that is a JavaScript port of a very popular and mature [Rx](http://reactivex.io/) library. It seems to be a bit complicated from the first glance, but it is really powerful for solving aforementioned problems.

## Configurable Components

This is the most important feature of our application, that aimed to fulfill one of the most frequent business needs: configure application UI and/or behavior \(partially\) per brand, environment, user segment, whatever, without need to re-deploy.

The title **Configurable Components** by itself doesn't mean, that configuration should be applied to React components only. It can be used in any application layer \(reducers, middleware, actions, etc.\), but the final result will eventually be reflected on the UI components.

Please check [Configurable Components](https://betlab.gitbook.io/betbook/~/edit/drafts/-LTYa_ozTe5i-Gwyqskb/basics/core-concepts#configurable-components) section of this documentation to get the overall idea of the implementation, that lays behind this feature.

## Feature-Toggling Support

Feature-flags are a time-honored way to control the capabilities of an application or service in a large decisive way.

Our previous experience in delivering different features for multiple brands forced us to introduce this mechanism into our CI/CD pipeline. It allows us to write code, that can reside in main artifact and can easily be toggled on demand for some particular brand, user group or using any other predicate, supported by our application.

This approach allows us to follow [trunk based development](https://trunkbaseddevelopment.com) approach with short lived feature branches and flexible application configuration, that doesn't require frequent re-deploys.

More information on this topic can be found in this section: [Feature-Toggling](../../basics/core-concepts.md#feature-toggling).



