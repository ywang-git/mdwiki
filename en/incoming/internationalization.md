#Internationalization (i18n) Best Practices

(from KNET training)

Globalization is a unified approach to create global products or features, especially those that support multiple geographies simultaneously.

Globalization = Internationalization + (localization + translation) + marketing + legal + fulfillment + taxation + support + sales

internationalization is an architecture.

## Internationalization Best Practices

### handle non ASCII character correctly
Unicode +UTF8
### use i18n API for formatting
MessageFormat API, etc.
### externalize resources: never hardcode strings
numbers, date, image, currency, time, measurement
### avoid string concatenation
### allow for text expansion
font size, string length
### are images appropriate?
### test other locales
globalizer (internal statistic analyzer)
external equivalent??

### design for I18N

1. what character encoding will the API use? does data structure locale-independent? enough room to store international data?
2. what languages are provided for translation? other requirement of changes for different locale other than language? (branding, imaging, etc.)
3. different data or functionality in different locale?


> Written with [StackEdit](https://stackedit.io/).