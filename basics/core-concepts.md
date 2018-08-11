# Core Concepts

## Configurable Components

Imagine your component has multiple variations of rendering for different brands, platforms or for different conditions, that can be accessed from the current application state:

{% code-tabs %}
{% code-tabs-item title="LoginForm.jsx" %}
```javascript
const LoginForm = (props) => {
  const showTermsAndConditionsLink = () => {
    if (!props.brand === 'ru') {
      return null;
    }
    
    const links = { 'com': '/terms-and-conditions', 'cy': '/terms' };
    const link = links[props.brand];
    
    return <a href={ link }>Terms and Conditions</a>;
  };
  
  return (
    <form>
      <input type="text" name="login" />
      <input type="password" name="password" />
      <input type="submit" name="login" />
      { showTermsAndConditionsLink() }
    </form>
  );
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This approach requires you to hold all possible variations within your source code. Adding new variation \(say, for the terms and condition link `href` attribute\) requires you to update the source code and to re-deploy the whole application bundle.

In order to simplify such a configuration you would like to pass all required options directly to the component properties and to be able to manage this configuration without affecting the source code:

{% code-tabs %}
{% code-tabs-item title="LoginForm.jsx" %}
```javascript
const config = api.get('/config/login-form.json);

const LoginForm = (props) => {
  const showTermsAndConditionsLink = () => {
    if (props.config.terms.show === false) {
      return null;
    }
    
    return <a href={ props.config.terms.href }>props.config.terms.title</a>;
  };
  
  return (
    <form>
      <input type="text" name="login" />
      <input type="password" name="password" />
      <input type="submit" name="login" />
      { showTermsAndConditionsLink() }
    </form>
  );
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

And your configuration file would look like this:

{% code-tabs %}
{% code-tabs-item title="login-form.json" %}
```javascript
{
    "terms": {
        "show": false,
        "href": "/terms",
        "title": "Terms and Conditions"
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Having this approach implemented, you can easily configure your component in a run-time. No re-builds, no re-deploys!

Different configurations for different brands and/or platforms can be stored in different files. And instead of resolving current brand and/or platform directly on the client side, you might also want to use a dedicated service, that does this job for you and provides proper configuration automatically.

That's where the [Config Manager](../reference/config-manager.md) service comes in. It stores and serves predefined configuration files provided by CMS, manually or by any other service.

More on this can be found in the [Config Manager](../reference/config-manager.md) section.

## Feature Toggling

In previous section the problem of configuring the representation of the component has been covered. Feature toggling, by turn, allows you make your application more flexible from the behavioral point of view.

Let's say you want to toggle some particular implementation of the application logic based on various conditions \(e.g. current user status, current brand, platform, etc.\):

{% code-tabs %}
{% code-tabs-item title="LoginForm.jsx" %}
```javascript
const LoginForm = (props) => {
  const submit = (event) => {
    if (props.brand === 'com') {
      // Experimental login feature.
      const isValid = api.validate(event);
      
      if (isValid) {
        api.newLogin(event);
      }
    } else {
      api.login(event);
    }
  };
  
  return (
    <form onSumbit={ sumbit }>
      <input type="text" name="login" />
      <input type="password" name="password" />
      <input type="submit" name="login" />
    </form>
  );
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In this example some experimental login feature has been introduce for a specific brand. In order to enable this feature for all brands and to get rid of old implementation, you'll have to update you source code, re-build and then re-deploy the application artifact. Instead, you could use the following approach:

{% code-tabs %}
{% code-tabs-item title="login.js" %}
```javascript
// Experimental login feature implementation.
export const newLogin = (event) => {
  const isValid = api.validate(event); 
  
  if (isValid) {
    api.newLogin(event);
  }
};

// Default login feature implementation.
export const oldLogin = (event) => {
  api.login(event);
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="api.js" %}
```javascript
import { newLogin, oldLogin } from './features/login';

export const resolveLoginFeatureImplementation = (params) => {
  if (api.isFeatureEnabled('newLogin')) {
    newLogin(params);
  } else {
    oldLogin(params);
  }
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="LoginForm.jsx" %}
```javascript
const LoginForm = (props) => {
  const submit = (event) => {
    api.resolveLoginFeatureImplementation(event);
  };
  
  return (
    <form onSumbit={ sumbit }>
      <input type="text" name="login" />
      <input type="password" name="password" />
      <input type="submit" name="login" />
    </form>
  );
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This will allow you to easily switch between implementations depending on the configuration, that might look like this:

{% code-tabs %}
{% code-tabs-item title="features.json" %}
```javascript
{
    "newLogin": {
        "enabledFor": {
            "brands": ["com", "cy"]
        }
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Splitting out the core components \(and not only components\) logic between files and including them on demand does the following:

* simplifies your code;
* makes your code cleaner;
* makes you code more testable and more maintainable;
* allows you to control you application bundles in a more flexible way.

Feature toggles by nature are intended to be used by release managers to solve business needs, but it's not forbidden to use them for the development needs also \(e.g. introducing some improved API implementation, that does not affect the end user\).

{% hint style="info" %}
You may ask _"Why can't I configure everything in a single configuration?"_. The answer is simple: features toggles \(or feature flags\) can have impact on the whole build process \(e.g. eliminating a set of non-required implementations/modules from the bundle\), while the components configuration is intended to be used for run-time configuration only and it can't be used for toggling the application behavior.

Also, same feature toggles might be used by different teams/components at the same time. For instance, if you want to disable login functionality both on UI and server sides.
{% endhint %}

Feature toggling topic is covered in more details in this section [Flip-Flop](../reference/flip-flop.md).

## Single Artifact

## Trunk Based Development

## TDD

## CI/CD/CD

## Unified App State Management



