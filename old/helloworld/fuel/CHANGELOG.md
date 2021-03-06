# Changelog

## v1.2

[Full List of core changes since 1.1](https://github.com/fuel/core/compare/1.1/master...1.2/master)

### Removed code (because it was deprecated in v1.1)

* All `factory()` methods. The have been replaced by `forge()`.
* __Agent__::is_mobile(). Replaced by `is_mobiledevice()`.
* __Arr__::element(). Replaced by `get()`.
* __Arr__::elements(). Replaced by `get()`.
* __Arr__::replace_keys(). Replaced by `replace_key()`.
* __Controller__::render(). Is no longer used as actions need to return a Response object now.
* __Database_Connection__::transactional(). Was already a NOOP.
* __DB__::transactional(). Called Database_Connection::transactional().
* __Fieldset__::errors(). Replaced by `error()`.
* __Fieldset__::repopulate(). Undocumented parameter was removed, functionality is offered by `populate()`.
* __Fuel__::find_file(). Replaced by `Finder::search()`.
* __Fuel__::list_files(). Replaced by `Finder::instance()->list_files()`.
* __Fuel__::add_path(). Was used by `find_file()`, no longer needed.
* __Fuel__::get_paths(). Was used by `find_file()`, no longer needed.
* __Fuel__::add_package(). Replaced by `Package::load()`.
* __Fuel__::remove_package(). Replaced by `Package::unload()`.
* __Fuel_Exception__ class. Replaced by `FuelException`.
* __Input__::get_post(). Replaced by `param()`.
* __Lang__::line(). Replaced by `get()`.
* __Request404Exception__ class. Is replaced by `HttpNotFoundException`.
* __Uri__ properties $uri and $segments are now protected. Use Uri::get() and Uri::get_segment() or Uri::get_segments().
* __Validation__::errors(). Replaced by `error()`.
* __Viewmodel__ property $_template. Is replaced by `$_view`.
* __Viewmodel__::set_template(). Replaced by `set_view()`.

### Code deprecated in v1.2 (to be removed in v1.3)

* __Pagination__: Class will be removed and replaced by a new `Paginate` class.
* __Fuel__::add_module(). Is replaced by `Module::load()`.
* __Fuel__::module_exists(). Is replaced by `Module::exists()`.
* __Theme__::asset(). Replaced by `asset_path()`.
* __Theme__::info(). Replaced by `get_info()`.
* __Theme__::all_info(). Replaced by `load_info()`.

### Security related

* Security class now __requires__ you to define the `security.output_filter` application config setting. An exception is thrown if it isn't present.
* Security::htmlentities() now defaults to use ENT_QUOTES instead of ENT_COMPAT as flag. This is configurable in the second argument for the method and the default can be overwritten in config as `security.htmlentities_flags`.

### System changes

* __Controller__: action methods, or the controllers `after()` method if present, now must return a `Response` object.
* __Controller__: `before()` and `after()` methods are now optional, as documented.
* __Controller_Hybrid__: combines `Controller_Template` and `Controller_Rest` in a single base controller for mixed HTTP and REST responses.
* __Controller_Rest__: added a fallback to `"action_"` when no HTTP method action is found.
* __Controller_Rest__: you can now define custom HTTP status codes.
* __Controller_Template__: the `$auto_render` setting has been removed, to prevent rendering return whatever you want to use instead.
* __Database__: The PDO driver now supports `list_columns()`.
* __Module__: new `Module` class to load or unload modules.
* __Uri__: the URL extension is no longer part of the URI. A new `extension()` method allows you to fetch it.
* __Request__: `Request_Curl` now properly deals with succesful requests that return a 4xx or 5xx HTTP status.
* __Request__: `Request_Curl` and `Request_Soap` now supports returning header information. A `get_headers()` has been added to fetch them manually.
* __Router__: can now be configured to treat URI's without regards to case.

### Specific classes

* __Arr__: `Arr::to_assoc()` now throws a BadMethodCallException on bad input.
* __Arr__: `Arr::assoc_to_keyval()` now requires all parameters and first parameter must be an array or implement `Iterator`.
* __Arr__: Added `reverse_flatten()`, `is_assoc()` and `insert_before_key()` methods.
* __Arr__: Added `in_array_recursive()` to do a recursive `in_array()` lookup.
* __Asset__: Separated into the static front (`Asset`) and dynamic instance (`Asset_Instance`).
* __Asset__: Separated into the static front (`Asset`) and dynamic instance (`Asset_Instance`).
* __Asset__: `css()`, `js()` and `img()` methods are now chainable.
* __Asset__: you can now specify a URL as location, for CDN support.
* __Asset__: new `fail_silently` config value allows you to skip missing assets.
* __Cli__: now supports ANSICON on Windows for colored commandline output.
* __Config__: is now driver based to support `php`, `ini`, `yaml` and `json` type configs.
* __Config__: now allow you to load a file by FQFN.
* __Cookie__: all cookie data can now be fetched like Input class does.
* __Date__: All fuel notices have been replaced by `UnexpectedValueException`s.
* __Date__: On windows an extra fallback has been added for the `create_from_string()` method.
* __Date__: new `display_timezone()' and `get_timezone_abbr()`, and changes to support working with multiple timezones.
* __DB__: `cache()` now has the option not to cache empty resultsets.
* __DB__: `where()` do now support closures to specify the where clause.
* __DB__: Update now supports `limit()` and `order_by()`.
* __DB__: now tries to reconnect when a disconnected DB connection is detected.
* __DButil__: `create_database()` now supports 'IF NOT EXIST'.
* __DButil__: Better support for the CONSTRAINT keyword.
* __DButil__: new `add_foreign_key()` and `drop_foreign_key()` methods.
* __Event__: shutdown events are now also executed after `exit` and `die` statements.
* __Fieldset__: added `set_fieldset_tag()` to define the fieldset tag.
__Fieldset__: added `add_before()` and `add_after()` methods to insert a new field before/after a specific field.
* __Fieldset_Field__: added `add_description()` method and `{description}` tag to templates.
* __Fieldset_Field__: added `add_error_message()` method to create error message overwrites per field.
* __File__: `download()` now allows you to continue processing after calling it.
* __Form__: Separated into the static front (`Form`) and dynamic instance (`Form_Instance`).
* __Inflector__: now supports Hungarian accepted characters when converting to ascii.
* __Input__: `method()` now supports the `X-HTTP-Method-Override` header.
* __Input__: new `json()` and `xml()` methods to fetch json or xml from the HTTP request body.
* __Lang__: `load()` method now supports overwriting when merging language files.
* __Lang__: now allow you to load a file by FQFN.
* __Lang__: is now driver based to support `php`, `ini`, `yaml` and `json` type language files.
* __Lang__: language files can now be saved (as `php`, `ini`, `yaml` or `json`) using `save()`.
* __Migrate__: now tracks individual migrations, so they don't have to have a sequence number anymore.
* __Model_Crud__: now supports `created_at` and `updated_at` fields, like `ORM\Model` does.
* __Model_Crud__: now has full callback support.
* __Model_Crud__: you can now run validation separately (`::validates`) and skip validation when saving a model.
* __Profiler__: profiler logging methods are now NO-OP's when the profiler is not loaded.
* __Profiler__: now writes it's output under the page content, instead of using an overlay.
* __Session__: Added session task to create and remove sessions table.
* __Session__: New sessions are not saved until there is data present in the session.
* __Theme__: Separated into the static front (`Theme`) and dynamic instance (`Theme_Instance`).
* __Theme__: now supports installation outside the docroot (for views).
* __Theme__: now uses the `Asset` class to load theme assets.
* __Theme__: instances now support templates, template partials and partial chrome templates.
* __Validation__: You can now disable fallback to global input using the 'validation.global_input_fallback' config setting.

### Packages

* __Auth__: Auth login drivers no have a `validate_user` method to validate a user/password without setting up a logged-in session.
* __Auth__: SimpleAuth `SimpleUserUpdateException`s are now numbered to be able to identify the exact error after catching the exception.
* __Email__: Now handles SMTP timeouts properly.
* __Email__: You can now specify the return address.
* __Email__: Now handles BCC lists correctly when using SMTP.
* __Email__: Respects new lines in alt body better.
* __Email__: You can now specify the return address.
* __Oil__: Use `phpunit.xml` from `APPPATH` if present when running unit tests.
* __Oil__: Reinstated `oil package` command to install packages from git repositories.
* __Oil__: You can define the environment the command has to run in using the `-env` commandline switch.
* __Oil__: Scaffolding now supports both `Model_Crud` and `Orm\Model`.
* __Oil__: Scaffolding now supports adding created-at and updated-at.
* __Oil__: Scaffolding now supports skipping the creation of a migration file using `-no-migration`.
* __Oil__: There is now a core task to generate the table for the database session store.
* __Orm__: New model method `is_fetched()` checks if relation data is fetched without triggering a new query.
* __Orm__: Validation section of the properties has a new key `skip` to indicate the field should not be validated.

## v1.1

[Full List of core changes since 1.0.1](https://github.com/fuel/core/compare/1.0/master...1.1/master)

### System changes

* Deprication of `Request::show_404()`, replaced with `throw new HttpNotFoundException` that has a handle method to show the 404
* Support for `handle()` method that is run when an exception isn't caught before `Error::exception_handler()` catches it.
* Support for special `_404_` route now in `public/index.php` thus no longer part of the core but still supported as a 'official default'
* Closures are now also supported in routes, thus routing to a Closure instead of a controler/method uri. Also added support for any type of callable in Route extensions you write yourself.
* Closure support in all getters & setters: if you get a value and also input a default the default can also be a Closure and you'll get the result of that. For setters the input can also be a closure and the result of the Closure will be set. (except for `View::set()` as one might want to pass a closure to the View)
* Moved the Environment setting from the `app/config/config.php` file to the `app/bootstrap.php` file.
* All `factory()` methods have been renamed to `forge()`.  This name better states the method's function.  The `factory()` methods are still there for backwards compatibility, but are deprecated and will log warning messages when used.
* The `$this->response` Response object is now deprecated.  Your action methods should return either a string, View object, ViewModel object or a Response object.
* Added the `fuel/app/vendor` directory to the default install.
* You can now have an unlimited number of sub-directories for your controllers. (e.g. `classes/controller/admin/users/groups.php` with a class name of `Controller_Admin_Users_Groups` would be at `site.com/admin/users/groups`)
* There is no longer a default controller for directories.  It used to be that going to something like `site.com/admin` would bring up `Controller_Admin_Admin` in `classes/controller/admin/admin.php`.  Now you must place that controller at it's expected location `classes/controller/admin.php` with a name of `Controller_Admin`.
* A `Controller::after()` method now gets passed the response of the controller, it must return that response (or modified) as well.
* Added new *function* `get_real_class()` to which you can pass a classname and it will return the actual class, to be used on classes of which you're not sure whether it is an alias or not.
* Module routes are prepended to the routes array when Fuel detects the fist URI segment as a module, therefor parsing them before an `(:any)` route in the app config.
* Config is now environment aware and allows partial/full overwriting of the base config from subdirectories in the config dir named after the environment.
* Added a new `Theme` class.  It allows you to easily add Theme support to your applications.
* `Fuel_Exception` has been renamed to `FuelException`
* `Fuel::find_file()` and related methods are now deprecated.  Use the `Finder` class instead (e.g. `Finder::search()`).
* Migrations are now supported in Modules and Packages
* Routing has 3 new shortcuts:
	* `:almun` matches all utf-8 alphabetical and numeric characters
	* `:num` matches all numeric characters.
	* `:alpha` matches all utf-8 alphabetical characters
* Put the `Autoloader` class into `Fuel\Core` to allow extending it, it must now be required in the app bootstrap file which is also the location where you must require your own extension.

### Security related

* Added Fuel's own response object class `Fuel\Core\Response` to default whitelist in `app/config/config.php` of objects that aren't encoded on output by the View when passed.
* The `security.auto_encode_view_data` config option in `app/config/config.php` has been renamed to `security.auto_filter_output`.
* `stdClass` was part of the default whitelisted classes from output encoding, this was a bug and it has been removed.

### Specific classes

* __Arr__: Added methods `Arr::get()`, `Arr::set()` and `Arr::prepend()`.
* __Arr__: `Arr::element()` and `Arr::elements()` have been deprecated.  Use the new `Arr::get()` instead.
* __Database__: Using transactions will no longer prevent exceptions, exceptions are thrown and should be handled by the dev. The `Database_Transaction` class has been deprecated as it has little use because of this change.
* __File__: `File::read_dir()` (and related methods on Area and Directory handler) now return dirnames with directory separator suffix
* __Fieldset_Field__: Parsing of validation rules has been moved from `Fieldset_Field::add_rule()` to `Validaton::_find_fule()`, from the outside the method still works the same but notices for inactive rules are now only shown when running the validation.
* __Form__: Added inline error reporting, which must first be switched on in config and will replace an `{error_msg}` tag
* __Form__: New default form template which puts it inside a table.
* __Fuel__: Added `Fuel::value()` which checks if the given value is a Closure, and returns the result of the Closure if it is, otherwise, simply the value.
* __Image__: No longer throws `Fuel_Exception` for any type of exception but instead `RuntimeException`, `InvalidArguementException` and `OutOfBoundsException` where appropriate.
* __Input__: `Input::post(null)` doesn't work to get full post array anymore, just `Input::post()` without params - same for all other Input methods
* __Input__: `Input::get_post()` has been deprecated and replaced by `Input::param()`.  It now also includes PUT and DELETE variables.
* __Input / Uri__: `Uri::detect()` moved to `Input::uri()` as it is part of the input and thus should be part of the input class
* __Request__: You can now also do external requests through the Request class, for now only a curl driver: `Request::forge('http//url', 'curl')` or `Request::forge('http//url', array('driver' => 'curl', 'method' => 'post', 'params' => array())`.
* __Validation__: `Validation::errors()` is depricated and replaced by singular form `Validation::error()` to be more in line with other class methods
* __Validation__: New 3rd parameter added to `Validation::run()` that allows adding callables for the duration of the run.
* __View__: The view class has been refactored and works much better now.  Output filtering is vastly improved.
* __View__: `View::capture()` has been split into two protected instance methods: `process_file()` and `get_data()`.  You will need to update your View class extensions.
* __View__: `View::$auto_encode` has been removed.  It has been replaced but auto_filter, which is per-view instance.
* __ViewModel__: Refactored the class internals to work more transparently with the `View`.
* __ViewModel__: Deprecated `$this->_template` and renamed it to `$this->_view`.
* __ViewModel__: Updated to work with the refactored `View` class.  Added `$this->bind()`.
* __ViewModel__: Deprecated `$this->set_template()` and renamed it to `$this->set_view()`.
* __Html__: Removed (not deprecated) the following methods: `Html::h()`, `Html::br()`, `Html::hr()`, `Html::nbs()`, `Html::title()`, `Html::header()`.  You should simply write the HTML yourself.
* __Config__: Added Config file drivers for PHP, INI, JSON and Yaml.  They are detected by file extension (e.g. `Config::load('foo.yml')` will load and parse the Yaml).

### Packages

* __Auth__: Renamed default table name from `simpleusers` to `users`.
* __Auth__: Added config options for DB connection and table columns used for fetching the user.
* __Auth__: Removed default config for groups & roles in `simpleauth.php` config file, only commented out examples left.
* __Orm__: Lots of tweaks to `Observer_Validation` related to changes to `Validation` & `Fieldset_Field` classes. Also changed it to only save properties that are actually changed.
* __Orm__: The `ValidationFailed` thrown when the `Observer_Validation` fails now includes a reference to the Fieldset instance that failed: `$valfailed->get_fieldset();`
* __Orm__: Added support for changing the type of join used when fetching relations, example: `Model_Example::query()->related('something', array('join_type' => 'inner'))->get();`
* __Orm__: Observers are no longer singleton but one instance per model with per model settings, check docs for more info.
* __Parser__: Added Parser package to the default install.
* __Parser__: Mustache is now part of the Parser package by default.  Version 0.7.1.
* __Email__: The Email package is added.

## v1.0

### Core

[Full Changelog](https://github.com/fuel/core/compare/v1.0-rc3...v1.0)

### Auth

[Full Changelog](https://github.com/fuel/auth/compare/v1.0-rc3...v1.0)

### Oil

[Full Changelog](https://github.com/fuel/oil/compare/v1.0-rc3...v1.0)

### Orm

[Full Changelog](https://github.com/fuel/orm/compare/v1.0-rc3...v1.0)


## v1.0-RC3

### Core

[Full Changelog](https://github.com/fuel/core/compare/v1.0-rc2.1...v1.0-rc3)

### Auth

[Full Changelog](https://github.com/fuel/auth/compare/v1.0-rc2...v1.0-rc3)

### Oil

[Full Changelog](https://github.com/fuel/oil/compare/v1.0-rc2...v1.0-rc3)

### Orm

[Full Changelog](https://github.com/fuel/orm/compare/v1.0-rc2...v1.0-rc3)


## v1.0-RC2.1

### Core

* Fixed a security issue where the URI was not being properly sanitized.

## v1.0-RC2

### Core

* oil refine install now makes the config directory writable. (Dan Horrigan)
* Added auto-id to select fields (Kelly Banman)
* Fixed typo in ::analyze\_table (Frank de Jonge)
* replaced the regex that processes :segment in the Route class. closes #33. (Harro Verton)
* Closes #31: logic error caused the Crypt class to update the config when nothing is changed. (Harro Verton)
* Fixed up XML output so that singular versions of basenode names are used when a numeric value is provided as a key.XML doesn't like numeric keys and item, item, item is boring. Also moved formatting logic out of the REST library. (Phil Sturgeon)
* Added Format::to\_php(). (Phil Sturgeon)
* Updated Form config file to work with the Form class we've had for the past 3 months (oops). Fixes #93 (Jelmer Schreuder)
* Fixes #115: Form::button() now produces a &lt;button&gt; tag instead of &lt;input&gt; (Harro Verton)
* Fixed #116: Throw an error if File::update can't open the file for write (Harro Verton)
* Added a check to File::open\_file() to make sure $resource is a valid resource before we attempt to flock() (Harro Verton)
* Fixed badly named variable in profiler. (Phil Sturgeon)
* Show full file paths in the Install task. No security concern if you're already in the terminal. (Phil Sturgeon)
* Fixed bug in \Date::create\_from\_string() where the date produced would always be exactly one month behind the actual date. (Ben Corlett)
* updated the Crypt class to make the generation of the random keys more secure (Harro Verton)
* fixed error in Fuel::find\_file(), causing a PHP notice on repeated finds (Harro Verton)
* The DBUtil class now respects the table prefix if set (Fixes #103). (Dan Horrigan)
* If an empty string is passed to Format::factory('', 'xml') it will no longer error, just return an empty array. (Phil Sturgeon)
* Added PHPSecLib to vendor to provide encryption features if no crypto is available in PHP. (Harro Verton)
* Rewritten the crypto class to use AES256 encryption, and a HMAC-SHA256 tamper validation hash. (Harro Verton)
* Added Redis to the bootstrap. (Jelmer Schreuder)
* Made Inflector::camelize() return camelcased result again but the Inflector::classify() won't use it anymore and still respect underscores. (Jelmer Schreuder)
* Allow setting labels as array including attributes instead of just tring in form->add (Jeffery Utter)
* Fix Date class. strptime returns years since 1900 not 1901. Dates were a year in the future. (Jeffery Utter)
* Options wasn't being passed when adding a radio.. thus it wasn't making all the separate fields. (Jeffery Utter)
* fixes bug #96: advanced regex must use non greedy match to properly match segments (Harro Verton)
* fixes bug #99: PHP notice due to not-initialized property (Harro Verton)
* Using memory\_get\_peak\_usage() instead of memory\_get\_usage() for more reliable memory reporting. (Jelmer Schreuder)
* Form generation: Fixed issue with "type" attribute set for textareas and selects. Also prevented empty for="" attributes by ignoring null values. (Jelmer Schreuder)
* Moved page link creation into separate method for more flexibility (Kelly Banman)
* fixed broken database profiling (Harro Verton)
* Input::real\_ip() now returns "0.0.0.0" if IP detection fails (Harro Verton)
* Bugfix: hidden inputs created with the Fieldset class caused unending loops. (Jelmer Schreuder)
* Fixed a bug that caused the image library to refuse all image types. (Alexander Hill)
* Corrected typos in the image class. (Alexander Hill)
* Fuel::find\_file() now caches files found per request URI, instead of a global cache. (Harro Verton)
* Fixed a bug in the response constructor. Response body was not setting. (Dan Horrigan)
* Bugfix: Fieldset::build() didn't match Form::build() for which it should be an alias. (Jelmer Schreuder)
* Changed Controller\_Rest formatting methods from private to protected so they can be extended (Tom Arnfeld)
* Improved the Fieldset::repopulate() method to also take a Model or array instead of using the POST values. Will accept any array, ArrayAccess instance, Orm\Model or object with public properties. (Jelmer Schreuder)

### Auth

* Fixed an issue with the casing of the Simple-driver classnames. (Jelmer Schreuder)
* Fixed small bug in Auth check method. (Jelmer Schreuder)
* Bugfix: ACL rights merging went wrong because the base was a string instead of an array. (Jelmer Schreuder)

### Oil

* Updated scaffolding to work better with the new ORM package. Fix #81.
* Suppress the error message for PHPUnit in oil, if it can't load the file from include it should just error as usual. (Phil Sturgeon)
* Fixed PHPUnit, said it wasn't installed when it was. (Phil Sturgeon)
* Fix #85: Scaffolding still referred to ActiveRecord instead of Orm. (Phil Sturgeon)

### Orm

* Added to\_array() method to export current object as an array. Improved ArrayAccess and Iterable implementation to work with relations. (Jelmer Schreuder)
* Finished the unfinished \_\_clone() method. (Jelmer Schreuder)
* Fixes #84 - now an exception is thrown when an invalid Model classname is given to a relation. (Jelmer Schreuder)
* Implemented \_\_isset() and \_\_unset() magic methods for Orm\Model (Jelmer Schreuder)
* Moved Query object creation into its own method to allow the more accurate Model\_Example::query()->where()->get(). (Jelmer Schreuder)
* order\_by() didn't return $this with array input. (Jelmer Schreuder)
* Fixed issue with constructing new models without adding properties. (Jelmer Schreuder)
