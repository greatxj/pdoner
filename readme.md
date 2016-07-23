# pdoner

## Running

````shell
$ phpize
$ ./configure --with-php-config=/path/php/bin/php-config
$ make && sudo make install
````

## global const

| name | explain
|--- |---
| PD_ONE_MINUTE | 60
| PD_ONE_HOUR | 3600
| PD_BY_DAY | 3600*12
| PD_ONE_DAY | 3600*24

## Function

| name | explain
|--- |---
| `int pd_random_id([int $salt = 0])` | a random id based unix timestamp.
| `string pd_implode_json(array $arr [, string $glue = ','])` | array [1=>123,2=>456] to string [123,456] <br> glue can also be other character.

## Class

respond defined, usage:
````php
$Rp = new Rp;  
echo Rp::get(Rp::FAIL) . "\n";  
Rp::set(6, '测试');  
var_dump(Rp::get());  
````

you can reference this:
````php
class Err 
{
    const SUCC = 0;
    const FAIL = 1;  
    const EXCEP = 2;
    const UNKNOW = 3;

    public static $msg = NULL;

    public function __construct() {
        self::$msg[self::SUCC] = '成功';
        self::$msg[self::FAIL] = '失败';
        self::$msg[self::EXCEP] = '异常';
        self::$msg[self::UNKNOW] = '未知';
    }   

    public static function get($code = "") 
    {   
		if (! self::$msg) {  
			trigger_error("please new Errs instance before use, for property will initialized in construct!\n", E_USER_WARNING);  
			return NULL;  
		}  

        return $code ? self::$msg[$code] : self::$msg;  
    }   

    public static function set($code, $value)
    {   
		if (! self::$msg) {  
			trigger_error("please new Errs instance before use, for property will initialized in construct!\n", E_USER_WARNING);  
			return false;  
		}

        if (isset(self::$msg[$code])) {  
			trigger_error("the code has exists in using " . __CLASS__ . "::" . __FUNCTION__ . "()!\n" , E_USER_WARNING);  
		} else if (self::$msg[$code] = $value) {  
			return true;  
		}  

        return false;  
    }   
}
````
