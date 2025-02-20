# About

Fix the issue related to version 4.0.1 and 4.0 of Superset are not applying translation correctly

Issue related: https://github.com/apache/superset/issues/30334 

# Fixing

This solution will override English language with the language choose on  process

1. Copy the most recent language .po file of your language ex: superset/translations/de/LC_MESSAGES/messages.po 

1. Convert the the .po file to .json

1. Copy the JSON content to the superset/translations/de/LC_MESSAGES/messages.json and superset/translations/en/LC_MESSAGES/messages.json
