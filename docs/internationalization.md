---
category: Develop
---
# Internationalization

<!-- Meta (to be deleted)
Purpose:
- describe how to make plugins/contributions available in different languages,
- describe how to use internationalization in twig templates & in PHP code,
- describe how to create new translation keys (ie, reuse as much as possible),
- describe how plugin developers can use otrance (possible?)

Audience: plugin developers

Expected Result: 

Notes: 

What's missing? (stuff in my list that was not in when I wrote the 1st draft)
- plugin developers + otrance
-->

## About this guide

**Read this guide if**

* you'd like to know **how to make your plugin available in other languages**
* you'd like to know **how to make your contribution to Piwik Core available in other languages**

**Guide assumptions**

This guide assumes that you:

* can code in PHP and JavaScript,
* can create Twig templates,
* know what [internationalization](http://en.wikipedia.org/wiki/Internationalization_and_localization) is,
* and have a general understanding of extending Piwik (if not, read our [Getting Started](/guides/getting-started-part-1) guide).

## The Basics

Internationalization is accomplished in Piwik by replacing text in the code with string IDs. String IDs are associated with text translated in languages that Piwik supports. These translations are stored in the JSON files in the `lang/` directory.

The string IDs are called **translation tokens** and have the following format: `MyPlugin_DescriptionOfThisText`.

To replace a token with translated text, Piwik will look into the JSON file for the current language. If no entry can be found, Piwik will use the english translation by default.

Translated text entries are allowed to contain `sprintf` parameters, for example, `"This translated text is uses a %s parameter"` or `"This translated text %1$s uses %2$s parameters."`. Every translate function will accept extra parameters that get passed to `sprintf` with the text.

### Using internationalization in PHP

To translate text in PHP, use the [Piwik::translate()](/api-reference/Piwik/Piwik#translate) function. For example:

```php
$translatedText = Piwik::translate('MyPlugin_MyText');
```

or

```php
$translatedText = Piwik::translate('MyPlugin_MyParagraphWithALink', '<a href="http:://piwik.org">', '</a>');
```

### Using internationalization in Twig templates

To translate text in Twig templates, use the `translate` filter. For example,

```twig
{{ 'MyPlugin_MyText'|translate }}
```

or

```twig
{{ 'MyPlugin_MyParagraphWithALink'|translate('<a href="http://piwik.org">', '</a>') }}
```

### Using internationalization in JavaScript

Translating text in the browser is a bit more complicated than on the server. The browser doesn't have access to the translations and we don't want to send every translation file to every user just so a couple lines of text can be translated.

Piwik solves this problem by allowing plugins to define which translation tokens should be available in the browser. It can then send only those translations in the current language to the browser.

To make a translation token available on the client side, use the [Translate.getClientSideTranslationKeys](/api-reference/events#translategetclientsidetranslationkeys) event:

```php
// an event handler in MyPlugin.php
public function getClientSideTranslationKeys(&$translationKeys)
{
    $translationKeys[] = 'MyPlugin_MyText';
    $translationKeys[] = 'CorePlugin_SomeCoreText';
}
```

To use these translations in JavaScript, use the global `_pk_translate()` JavaScript function:

```javascript
var translatedText = _pk_translate('MyPlugin_MyText');
```

## Adding translation tokens

**If you are developing a plugin or theme** add the translation token to your plugin's language files. The language files should be added to a `lang/` subdirectory of your plugin (e.g. `plugins/MyPlugin/lang/en.json`).

**If you are developing a contribution for Piwik Core** add the translation token and the english translation to `lang/en.json`. Do not add translations for other languages as those as managed through a separate tool.

### Guidelines for new translation tokens

Follow these guidelines when creating your own translation tokens:

1. **Reuse!** If a core plugin contains a translation you can use, use that instead. If there's a translation you want to use but can't because it's in the wrong case, try using functions like `lcfirst` and `ucfirst`.
2. **Reduce redundancy in your translated text.** If the same text appears in multiple translated text entries, try to move the translated text out by using sprintf parameters. For example, if you have text entries like:

  `"You cannot use commas."`
  and `"You cannot use underscores."`

  Try to split them up into something like:

  `"You cannot use %s."`
  `"commas"`
  and `"underscores"`.

  This guideline is more important for contributions to Piwik Core than for new plugins.
