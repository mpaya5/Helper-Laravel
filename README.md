# Helper-Laravel
How to create a Helper in Laravel, step by step

>Sorry but the code that I write is in Spanish

### Step 1: 
- Create a Helper in the Directory `App/Helper`
```
<?php
namespace App\Helpers;
  
use Illuminate\Support\Facades\DB;
  
class FormatTime {
 
    public static function LongTimeFilter($date) {
        if ($date == null) {
            return "Sin fecha";
        }
 
        $start_date = $date;
        $since_start = $start_date->diff(new \DateTime(date("Y-m-d") . " " . date("H:i:s")));
 
        if ($since_start->y == 0) {
            if ($since_start->m == 0) {
                if ($since_start->d == 0) {
                    if ($since_start->h == 0) {
                        if ($since_start->i == 0) {
                            if ($since_start->s == 0) {
                                $result = $since_start->s . ' segundos';
                            } else {
                                if ($since_start->s == 1) {
                                    $result = $since_start->s . ' segundo';
                                } else {
                                    $result = $since_start->s . ' segundos';
                                }
                            }
                        } else {
                            if ($since_start->i == 1) {
                                $result = $since_start->i . ' minuto';
                            } else {
                                $result = $since_start->i . ' minutos';
                            }
                        }
                    } else {
                        if ($since_start->h == 1) {
                            $result = $since_start->h . ' hora';
                        } else {
                            $result = $since_start->h . ' horas';
                        }
                    }
                } else {
                    if ($since_start->d == 1) {
                        $result = $since_start->d . ' día';
                    } else {
                        $result = $since_start->d . ' días';
                    }
                }
            } else {
                if ($since_start->m == 1) {
                    $result = $since_start->m . ' mes';
                } else {
                    $result = $since_start->m . ' meses';
                }
            }
        } else {
            if ($since_start->y == 1) {
                $result = $since_start->y . ' año';
            } else {
                $result = $since_start->y . ' años';
            }
        }
 
        return "Hace " . $result;
    }
}
```

### Step 2
- Create the provider using the command:
`php artisan make:provider FormatTimeServiceProvider`

### Step 3
- Include the register method in the provider:
```
public function register()
{
    require_once app_path() . '/Helpers/FormatTime.php';
}
```

### Step 4
- Enter the directory config / app.php and add the provider to the array of providers:
`App\Providers\FormatTimeServiceProvider::class,`
- And add an alias for our helper:
`'FormatTime' => App\Helpers\FormatTime::class,`
- We can now use our helper in any part of our code, for example in a view we would do something like this:
`{{ \FormatTime::LongTimeFilter($entrada->created_at) }}`

And with this we have already learned to create helpers in Laravel 5 in a simple way
