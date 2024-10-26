
# self.machine.modes.attract

`class mpf.modes.attract.code.attract.Attract(*args, **kwargs)`

Bases: mpf.core.mode.Mode

Default mode running in a machine when a game is not in progress.

The attract mode’s main job is to watch for the start button to be pressed, to post the requests to start games, and to move the machine flow to the next mode if the request to start game comes back as approved.

## Accessing the attract mode via code

You can access the attract mode from anywhere via `self.machine.modes.attract`.

## Methods & Attributes

The attract mode has the following methods & attributes available. Note that methods & attributes inherited from the base Mode class are not included here.

`active`

Return True if this mode is active.

`add_mode_event_handler(event: str, handler: Callable, priority: int = 0, **kwargs) → mpf.core.events.EventHandlerKey`

Register an event handler which is automatically removed when this mode stops.

This method is similar to the Event Manager’s add_handler() method, except this method automatically unregisters the handlers when the mode ends.

Parameters:

* **event** – String name of the event you’re adding a handler for. Since events are text strings, they don’t have to be pre-defined.
* **handler** – The method that will be called when the event is fired.
* **priority** – An arbitrary integer value that defines what order the handlers will be called in. The default is 1, so if you have a handler that you want to be called first, add it here with a priority of 2. (Or 3 or 10 or 100000.) The numbers don’t matter. They’re called from highest to lowest. (i.e. priority 100 is called before priority 1.)
* ****kwargs** – Any any additional keyword/argument pairs entered here will be attached to the handler and called whenever that handler is called. Note these are in addition to kwargs that could be passed as part of the event post. If there’s a conflict, the event-level ones will win.

Returns a EventHandlerKey to the handler which you can use to later remove the handler via remove_handler_by_key. Though you don’t need to remove the handler since the whole point of this method is they’re automatically removed when the mode stops.

Note that if you do add a handler via this method and then remove it manually, that’s ok too.

`configure_logging(logger: str, console_level: str = 'basic', file_level: str = 'basic', url_base=None)`

Configure logging.

Parameters:

* **logger** – The string name of the logger to use.
* **console_level** – The level of logging for the console. Valid options are “none”, “basic”, or “full”.
* **file_level** – The level of logging for the console. Valid options are “none”, “basic”, or “full”.
* **url_base** – Base URL for docs links in exceptions.

`create_mode_devices() → None`

Create new devices that are specified in a mode config that haven’t been created in the machine-wide.

`debug_log(msg: str, *args, context=None, error_no=None, **kwargs) → None`

Log a message at the debug level.

Note that whether this message shows up in the console or log file is controlled by the settings used with configure_logging().

`error_log(msg: str, *args, context=None, error_no=None, **kwargs) → None`

Log a message at the error level.

These messages will always be shown in the console and the log file.

`format_log_line(msg, context, error_no) → str`

Return a formatted log line with log link and context.

`ignorable_runtime_exception(msg: str) → None`

Handle ignorable runtime exception.

During development or tests raise an exception for easier debugging. Log an error during production.

`info_log(msg: str, *args, context=None, error_no=None, **kwargs) → None`

Log a message at the info level.

Whether this message shows up in the console or log file is controlled by the settings used with configure_logging().

`initialise_mode() → None`

Initialise this mode.

`is_game_mode`

Return true if this is a game mode.

`load_mode_devices() → None`

Load config of mode devices.

`mode_will_start(**kwargs) → None`

User-overrideable method which will be called whenever this mode starts (i.e. before it becomes active).

`raise_config_error(msg, error_no, *, context=None) → NoReturn`

Raise a ConfigFileError exception.

`result_of_start_request(ev_result=True)`

Handle the result of the start request.

Called after the request_to_start_game event is posted.

If result is True, this method posts the event game_start. If False, nothing happens, as the game start request was denied by some handler.

Parameters:	ev_result – Bool result of the boolean event request_to_start_game. If any registered event handler did not want the game to start, this will be False. Otherwise it’s True.

`start(mode_priority=None, callback=None, **kwargs) → None`

Start this mode.

Parameters:

* **mode_priority** – Integer value of what you want this mode to run at. If you don’t specify one, it will use the “Mode: priority” setting from this mode’s configuration file.
* **callback** – Callback to call when this mode has been started.
* ****kwargs** – Catch-all since this mode might start from events with who-knows-what keyword arguments.

Warning: You can safely call this method, but do not override it in your mode code. If you want to write your own mode code by subclassing Mode, put whatever code you want to run when this mode starts in the mode_start method which will be called automatically.

`start_button_pressed()`

Handle start button press.

Called when the a switch tagged with start is activated.

Note that in MPF, the game start process is initiated when the start button is released, so when the button is first pressed, MPF just records the time stamp. This allows the total time the start button was pressed to be note, so that, for example, different types of games can be started based on long-presses of the start button.

`start_button_released(**kwargs)`

Handle start button release.

Called when the a switch tagged with start is deactivated.

Since this is the Attract mode, this method posts a boolean event called request_to_start_game. If that event comes back True, this method calls result_of_start_request().

`stop(callback: Any = None, **kwargs) → bool`

Stop this mode.

Parameters:

* **callback** – Method which will be called once this mode has stopped. Will only be called when the mode is running (includes currently stopping)
* ****kwargs** – Catch-all since this mode might start from events with who-knows-what keyword arguments.

Warning: You can safely call this method, but do not override it in your mode code. If you want to write your own mode code by subclassing Mode, put whatever code you want to run when this mode stops in the mode_stop method which will be called automatically.

Returns true if the mode is running. Otherwise false.

`warning_log(msg: str, *args, context=None, error_no=None, **kwargs) → None`

Log a message at the warning level.

These messages will always be shown in the console and the log file.
