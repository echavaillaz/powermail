# TYPO3 Extension powermail

Powermail is a well-known, editor-friendly, powerful
and easy to use mailform extension for TYPO3 with a lots of features
(spam prevention, marketing information, optin, ajax submit, diagram analysis, etc...)

## TYPO3 10

We're working hard on a release for TYPO3 10 (see branch feature/8.0.0). This release will run only for TYPO3 10 because
of a lot of breaking changes in the core. Roadmap:

* done [TASK] Update for TYPO3 10 (Backendroutes, Conditions, Validators, UserFuncs in Tca)
* done [TASK] Remove code dependencies to former TYPO3 versions
* done [TASK] Add typehints for PHP 7.2
* done [TASK] Use a different way for GET/POST params (to respect routing)
* done [TASK] Rename _field.pages to .page and _page.forms to .form and add an upgrade wizard for it
* done [TASK] Save mails in future with sys_language_uid=-1 and add an upgrade wizard for it
* done [TASK] Some modernization and code cleanup (Own exceptions, remove AbstractUtility)
* done [TASK] Update unit tests
* [TASK] Update behaviour tests
* [TASK] Manual tests (especially in backend context)
* [TASK] Update documentation from rst to markdown

## 1. Installation

Please look at the manual for a detailed documentation at [official extension documentation of TYPO3](https://docs.typo3.org/typo3cms/extensions/powermail)

Quick guide:
- Just install this extension - e.g. `composer require in2code/powermail`
- Add a static typoscript template to your root template
- Add a new form (with one or more pages and with some fields to a page or a folder)
- Add a new pagecontent (plugin) with type "powermail" and choose the former saved form
- That's all, you can view the result in the frontend

## 2. Administration corner

### 2.1. Versions and Support

| Powermail           | TYPO3      | PHP       | Support/Development                     |
| ------------------- | ---------- | ----------|---------------------------------------- |
| 8.x (released soon) | 10.x       | >= 7.2    | Features, Bugfixes, Security Updates    |
| 7.x                 | 8.7 - 9.x  | 7.0 - 7.x | Bugfixes, Security Updates              |
| 6.x                 | 8.7 - 9.x  | 7.0 - 7.x | Support dropped                         |
| 5.x                 | 8.7 - 9.x  | 7.0 - 7.x | Support dropped                         |
| 4.x                 | 7.6 - 8.7  | 5.5 - 7.2 | Security Updates                        |
| 3.x                 | 7.6 - 8.7  | 5.5 - 7.2 | Support dropped                         |
| 2.18 - 2.25         | 6.2 - 7.6  | 5.5 - 7.0 | Support dropped                         |
| 2.2 - 2.17          | 6.2 - 7.6  | 5.3 - 7.0 | Support dropped                         |

Do you need free support? There is a kind TYPO3 community that could help you.
You can ask questions at https://stackoverflow.com and tag your question with `TYPO3` and `Powermail`.
In addition there is a slack channel in the TYPO3 slack `ext-powermail`.

### 2.2. Changelog

Please look into the [official extension documentation in changelog chapter](https://docs.typo3.org/typo3cms/extensions/powermail/Changelog/Index.html)

### 2.3. Suggested Extensions for powermail

- **email2powermail** Automatically convert emails to a link to a powermail form [Link](https://github.com/einpraegsam/email2powermail)
- **powermailrecaptcha** Google recaptcha [Link](https://github.com/einpraegsam/powermailrecaptcha)
- **invisiblerecaptcha** Google invisible recaptcha [Link](https://github.com/einpraegsam/invisiblerecaptcha)
- **powermailextended** Is just an example extension how to extend powermail with new fields or use signals [Link](https://github.com/einpraegsam/powermailextended)
- **powermail_cond** Add conditions (via AJAX) to powermail forms for fields and pages [Link](https://github.com/einpraegsam/powermail_cond)
- **powermail_fastexport** Extend powermail for faster export to .xlsx / .csv files. This is useful if you have many records to be exported. [Link](https://github.com/bithost-gmbh/powermail_fastexport)

### 2.4. Product Owner

The product owner and author of the extension is Alex Kellner from [in2code](https://www.in2code.de). Beside that every
in2code colleague is allowed to support further development if she/he wants. In addition there are a lot of other
contributors that helped to improve the extension with their *Pull Requests* - thank you for that!

### 2.5. Release Management

Powermail uses **semantic versioning** which basically means for you, that
- **bugfix updates** (e.g. 1.0.0 => 1.0.1) just includes small bugfixes or security relevant stuff without breaking changes.
- **minor updates** (e.g. 1.0.0 => 1.1.0) includes new features and smaller tasks without breaking changes.
- **major updates** (e.g. 1.0.0 => 2.0.0) normally includes basic refactoring, new features and also breaking changes.

We try to mark breaking changes in the [changelog](https://docs.typo3.org/typo3cms/extensions/powermail/Changelog/Index.html)
with a leading **!!!** and try to explain what to do on an upgrade (e.g. VieHelper name changed from vh:foo to vh:bar in templates).

In addition powermail is using [Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) as Git workflow.
That means that there is one branch which contains new and untested code: **develop**.
The branch **master** only contains tested code which will also be tagged from time to time.

Based on `release early, release often` we try to release new versions as often as possible into TER and to github/packagist.

### 2.6. Automatic Testing

#### Behaviour tests

There is a huge testparcours that have to be passed before every release. For example there is an
[automatic test](https://github.com/einpraegsam/powermail/blob/develop/Tests/Behavior/Features/Pi1/Validation/Input/JsPhpValidation.feature)
where the browser tries to submit 18 different strings and numbers to a field that accepts only phone numbers to test
serverside validation. After that the same process is done for clientside valiation.
There are also some smaller tests like "Is it possible to submit a form on a page where two different forms are stored?".

See [readme.md](https://github.com/einpraegsam/powermail/tree/develop/Tests/Behavior) for some more information about behat and selenium tests on powermail.

#### Unit tests

At the moment powermail offers 543 (and growing) unit tests that have to be passed before every release. See more information
about unit tests or code coverage in powermail in the [readme.md](https://github.com/einpraegsam/powermail/tree/develop/Tests/Unit)

### 2.7. Code quality

Beside respecting PSR-2 and TYPO3 coding guidelines, it's very important for the project to leave a file cleaner as before.
Especially because it's a really large extension with a lot of functionality and a history of 10 years (!) and of course some
technical debts, that have to be fixed step by step (e.g. moving logic completely to Domain folder, ...).
Look at [Sonarqube](https://ter-sonarqube.marketing-factory.de/dashboard?id=powermail) for some interesting details on that.

### 2.8. Contribution

**Pull requests** are welcome in general! Nevertheless please don't forget to add a description to your pull requests. This
is very helpful to understand what kind of issue the **PR** is going to solve.

- Bugfixes: Please describe what kind of bug your fix solve and give us feedback how to reproduce the issue. We're going
to accept only bugfixes if I can reproduce the issue.
- Features: Not every feature is relevant for the bulk of powermail users. In addition: We don't want to make powermail
even more complicated in usability for an edge case feature. Please discuss a new feature before.


### 2.9. Development

Compile and minify (uglify) JavaScript, compress CSS:

```
$ cd Resources/Private
$ npm install
$ ./node_modules/.bin/gulp
```


## 3. Screenshots

### 3.1. Example form with bootstrap classes:

![Example form](https://box.everhelper.me/attachment/445407/3910b9da-83f9-477d-83b1-f7e21ead9433/262407-KmKJsSfGKDz6bnVO/screen.png "Example Form")


### 3.2. Backend module mail list:

![Backend Module](https://box.everhelper.me/attachment/445409/3910b9da-83f9-477d-83b1-f7e21ead9433/262407-HFuHtr8E9DoGfJE6/screen.png "Backend Module")
