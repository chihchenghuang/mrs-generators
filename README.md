# [Laravel MRS Generators](https://packagist.org/packages/chihchenghuang/laravel-mrs-generators)

> This package is a experimental project inspired by [yish/generators](https://packagist.org/packages/yish/generators) which extends the core file generators based on Laravel 5
> It can help you build classes with basic Model-Repository-Service pattern.

# Installation

Install by composer
```
    $ composer require chihchenghuang/laravel-mrs-generators
```

Registing Service Provider

``` php
<?php

//app.php

'providers' => [
        
        /*
         * Laravel MRS Generators Service Provider
         */
        \ChihCheng\MRSGenerators\GeneratorsServiceProvider::class,

    ],

```
or

``` php
<?php

//app/Providers/AppServiceProvider.php

    public function register()
    {
        if ($this->app->environment() == 'local')
        {
	        /*
	         * Laravel MRS Generators Service Provider
	         */
            $this->app->register( \ChihCheng\MRSGenerators\GeneratorsServiceProvider::class );

        }
    }

```

## Example

### Generate Repository:
>This command will generate a repository class.

```
    $ php artisan make:repository Repositories/TestRepository
```

### Generate Service:
>This command will generate a service class.

```
    $ php artisan make:repository Services/TestService
```

### Generate classes based on the corresponding Model-Repository-Service Pattern Set:
>This command will generate classes based on the corresponding Model-Repository-Service Pattern Set.
>It will create files like the example pattern below by using only one command:

```
    $ php artisan make:mrs-model Test
```
* app/Models/Test.php
``` php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Test extends Model
{
    //
}

```
* app/Repositories/TestRepository.php
``` php
<?php

namespace App\Repositories;

use App\Models\Test;

class TestRepository
{
    protected $test;

    public function __construct( Test $test )
    {
        $this->test = $test;
    }

}

```
* app/Services/TestService.php
``` php
<?php

namespace App\Services;

use App\Repositories\TestRepository;

class TestService
{
    protected $testRepository;

    public function __construct( TestRepository $testRepository )
    {
        $this->testRepository = $testRepository;
    }

}

```