# Redis Object Cache Drop-in for WordPress

_[This is a fork of WP Redis](https://github.com/pantheon-systems/wp-redis)_

A simple drop-in that makes WordPress cache objects in Redis. This reason for the fork is to ensure compatibility with [Batcache](https://wordpress.org/plugins/batcache/).

## Installation

This assumes you have a PHP environment with the [required PhpRedis extension](https://github.com/phpredis/phpredis) and a working Redis server.

1. Install `object-cache.php` to `wp-content/object-cache.php` with a symlink or by copying the file.
2. Optionally edit wp-config.php to add your cache credentials, e.g.:

	```php
	$redis_server = array(
		'host' => '127.0.0.1',
		'port' => 6379,
		'auth' => '12345',
	);
	```

3. Engage thrusters: you are now backing WP's Object Cache with Redis.
4. (Optional) To use the same Redis server with multiple, discreet WordPress installs, you can use the `WP_CACHE_KEY_SALT` constant to define a unique salt for each install.
5. (Optional) To use true cache groups, with the ability to delete all keys for a given group, define the `WP_REDIS_USE_CACHE_GROUPS` constant to true. However, when enabled, the expiration value is not respected because expiration on group keys isn't a feature supported by Redis.
6. (Optional) On an existing site previously using WordPress' transient cache, use WP-CLI to delete all (`%_transient_%`) transients from the options table: `wp transient delete-all`. WP Redis assumes responsibility for the transient cache.