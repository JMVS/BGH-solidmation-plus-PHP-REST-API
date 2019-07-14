# BGH & Solidmation Plus PHP REST API
Solidmation / BGH Smart Control Kit PHP REST API for HVAC (air conditioner)

Based on https://github.com/JoanManuelH/BHG-solidmation-PHP-REST-API

## Usage

```php
define("BGH_USER", "XXXXX"); //Login email
define("BGH_PASS", "XXXXX"); //Login password

require 'bgh.class.php';

$bgh = new BGH();
/* Use this if you want to get your device list or use another endpointID instead of first */
$devices = $bgh->getDevices(); 
print("<pre>".print_r($devices,true)."</pre>");

/* Available modes & functions
mode (if not specified, cold is default):
"off" = Off
"cold" = Cold
"hot" = Hot
"dehum" = Dehumidifier
"vent" = Ventilation
"auto" = Auto

temperature (if not specified or out of range, 24 is default):
Integer range from 17 to 30.

fan (if not specified or out of range, 4 is default):
1 = Speed 1
2 = Speed 2
3 = Speed 3
4 = Auto

endpoint (if not specified, first device found is default):
Numeric value representing device.

subcommand (if not specified, 0 is default):
0 = nothing
81 = swing
113 = turbo
*/

$bgh->sendCommand(array(
	"temperature" => 17,   //Set temperature
	"fan" => 3,            //Set 1-3 (254 for auto)
	"subcommand" => 81     //Set subcommand function
	"endpoint" => 39282,   //Set endpoint
	"mode" => "cold"       //Set mode
));

/* Turn on and set it to 19° */
$bgh->sendCommand(array(
	"temperature" => 19
));

/* Turn fan on max */
$bgh->sendCommand(array(
	"fan" => 3
));

/* Turn off */
$bgh->sendCommand(array(
	"mode" => "off"
));
```

### Commands
#### returnToken _(null)_
Get BGH private token
#### getHomeId _(null)_
Get the ID of your home
#### getDevices _(null)_
Get a list of devices on your home, including ID, room temperature, air conditioner preset, and status
```php
print("<pre>".print_r($devices,true)."</pre>");
```

```php
Array
(
    [0] => Array
        (
            [endpointID] => 39282
            [turned] => 1
            [room] => 30.2
            [air] => 17
            [name] => Terraza
            [device] => BGH Smart Control Kit
            [homeID] => 27622
        )

)
```
#### sendCommand _(Array)_
Send command to air conditioner

## License

MIT License

2019
