# Fast-Hyperf
[中文](./README-cn.md)

[![Latest Stable Version](http://poser.pugx.org/yogcloud/framework/v)](https://packagist.org/packages/yogcloud/framework) [![Total Downloads](http://poser.pugx.org/yogcloud/framework/downloads)](https://packagist.org/packages/yogcloud/framework) [![Latest Unstable Version](http://poser.pugx.org/yogcloud/framework/v/unstable)](https://packagist.org/packages/yogcloud/framework) [![License](http://poser.pugx.org/yogcloud/framework/license)](https://packagist.org/packages/yogcloud/framework) [![PHP Version Require](http://poser.pugx.org/yogcloud/framework/require/php)](https://packagist.org/packages/yogcloud/framework)

A component based on Hyperf Framework with rapid installation


```php
composer require yogcloud/framework
```


# Function
supply `Controller` `Request` `Model` `Service` `Interface` Complete set of build commands
```php
$ php bin/hyperf
 fs
  fs:controller        Generate controller, Generated by default in app/Controller
  fs:model             Generate Model, default generate app/Model, Automatic generated Service,Interface
  fs:request           Generate request, Generated by default in app/Request
  fs:service           Generate service, Generated by default in app/Service
  fs:serviceInterface  Generate service interface, Generated by default in app/Service
server
    server:restart       Restart hyperf servers.
    server:start         Start hyperf servers.
    server:stop          Stop hyperf servers.
```


One-click code generation for rapid development
```php
php bin/hyperf.php fs:model test

Model App\Model\Test was created.
success:[/demo/app/Rpc/TestServiceInterface.php]
success:[/demo/app/Service/TestService.php]
```

Generate Code

```php
    /**
     * Query single entry - by ID.
     * @param int $id ID
     * @param array|string[] $columns Query field
     * @return array
     */
    public function getOneById(int $id, array $columns = ['*']): array;

    /**
     * Query single - according to the where condition.
     * @param array $where
     * @param array|string[] $columns
     * @param array Optional ['orderByRaw'=> 'id asc', 'with' = []]
     * @return array
     */
    public function findByWhere(array $where, array $columns=['*'], array $options = []): array;

    /**
     * Query multiple - by ID.
     * @param array $ids ID
     * @param array|string[] $columns
     * @return array
     */
    public function getAllById(array $ids, array $columns = ['*']): array;

    /**
     * Query multiple items according to where criteria.
     * @param array $where
     * @param array $columns
     * @param array  ['orderByRaw'=> 'id asc', 'with' = [], 'selectRaw' => 'count(*) as count']
     * @return array
     */
    public function getManyByWhere(array $where, array $columns = ['*'], array $options = []): array;

    /**
     * Multiple pages.
     * @param array $where
     * @param array|string[] $columns
     * @param array $options  ['orderByRaw'=> 'id asc', 'perPage' => 15, 'page' => null, 'pageName' => 'page']
     * @return array
     */
    public function getPageList(array $where, array $columns = ['*'], array $options = []): array;

    /**
     * Add single.
     * @param array $data
     * @return int
     */
    public function createOne(array $data): int;

    /**
     * Add multiple.
     * @param array $data
     * @return bool
     */
    public function createAll(array $data): bool;

    /**
     * Modify single entry - according to ID.
     * @param int $id id
     * @param array $data
     * @return int
     */
    public function updateOneById(int $id, array $data): int;

    /**
     * Modify multiple - according to ID.
     * @param array $where
     * @param array $data
     * @return int
     */
    public function updateByWhere(array $where, array $data): int;

    /**
     * Delete - Single.
     * @param int $id
     * @return int
     */
    public function deleteOne(int $id): int;

    /**
     * Delete - multiple.
     * @param array $ids
     * @return int
     */
    public function deleteAll(array $ids): int;

    /**
     * Handle native SQL operations.
     * @param mixed $raw
     * @param array $where
     * @return array
     */
    public function rawWhere($raw, array $where = []): array;

    /**
     * Get a single value
     * @param string $column
     * @param array $where
     * @return string
     */
    public function valueWhere(string $column, array $where): string;
```

## Multi-application development
Generated outside the app

Because the design was originally designed for multi-plug-in and multi-function modules

for `Hyperf/Utils/CodeGen` need to read `composer-psr4` so
```json
"autoload": {
    "psr-4": {
        "App\\": "src/",
        "Demo\\Plugin\\Test": "plugin/demo/test/src/"
    }
}
```
update cache
```php
composer dump-autoload -o
```
generate
```php
php bin/hyperf fs:model test --path plugin/demo/test/src
```

The generated TestService can easily manipulate data and save most of the development time

> generate Service `--cache false` Cache can be disabled (enabled by default)

Cache will be generated after request, update/delete delete cache (default 9000TTL, will not occupy resources all the time)

## Tips
Looking forward to your discovery of other tips. Welcome to Pr

1. `Give a query column an alias`
```php
'selectRaw' => 'sum(`id`) as sum'
```
2. `Construct to where clause by closure`
```php
[function ($q) {
    $q->where('id', '=', 1)->orWhere('id', '=', 2);
}]
```


# TODO
- [ ] Generate Controller

# License
Apache License Version 2.0, http://www.apache.org/licenses/
