# Core Concepts

## Configurable Components

Imagine your component has multiple variations of rendering for different brands, platforms or for different conditions, that can be accessed from the current application state:

```javascript
const LoginForm = (props) => {
  const showTermsAndConditionsLink = () => {
    if (!props.brand === 'com') {
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

This approach requires you to hold all possible variations within your source code. Adding new variation \(say for terms and condition link `href` attribute\) requires you to update the source code and to re-deploy the whole application bundle.

In order to simplify such a configuration you would like to pass all required options directly to the component properties and to be able to manage this configuration without affecting the source code:

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

And your configuration file would look like this:

{% code-tabs %}
{% code-tabs-item title="login-form.json" %}
```javascript
{
    "terms": {
        "show": false,
        "href": "/terms"/,
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

## Single Artifact

## Trunk Based Development

## TDD

## CI/CD/CD

## Unified App State Management



