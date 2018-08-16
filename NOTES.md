# 1. XSS

## 1.1 Types of xss (danger zone)

- **stored xss:** code that executes attacker's script is persisted

- **reflected xss:** transient response from server causes script to execute (i.e. validation errors)

- **dom based xss:** no server involvement is required (i.e. pass code via queryParams)

- **blind xss:** exploit vulnerability in another app (i.e. log-reader), that the attackers can't see or access under the normal means

## 1.2 Place of xss

- under generated rich text (i.e. WYSIWYG)
- enbedded content
- anywhere the users have control over a url
- anywhere the users have input that relected back (i.e. "could not found xxx")
- query parameter rendered into a dom
- element.innerHTML = xxx

## In test project

user1:
test@test.com
Abcd1234
