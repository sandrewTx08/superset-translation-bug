# About

Fix the issue related to version **4.0.1** and **4.0** of [Superset](https://github.com/apache/superset) are not applying translation correctly

Issue related: https://github.com/apache/superset/issues/30334 

# Fixing

This solution will override English language with the language choose on  process

1. Copy the most recent language .po file of your language ex: `superset/translations/de/LC_MESSAGES/messages.po` 

1. Convert the the .po file to .json

1. Copy the JSON content to the `superset/translations/de/LC_MESSAGES/messages.json` and `superset/translations/en/LC_MESSAGES/messages.json`
# Change default language code to english

`superset/translations/utils.py`
```py
def get_language_pack(locale: str) -> Optional[dict[str, Any]]:
    """Get/cache a language pack

    Returns the language pack from cache if it exists, caches otherwise

    >>> get_language_pack('fr')['Dashboards']
    "Tableaux de bords"
    """
    locale = "en"
    pack = ALL_LANGUAGE_PACKS.get(locale)
    if not pack:
        filename = DIR + f"/{locale}/LC_MESSAGES/messages.json"
        try:
            with open(filename, encoding="utf8") as f:
                pack = json.load(f)
                ALL_LANGUAGE_PACKS[locale] = pack or {}
        except Exception:  # pylint: disable=broad-except
            # Assuming english, client side falls back on english
            pass
    return pack
```

