<a name="module_handbrake-js"></a>
##handbrake-js
Handbrake for node.js.

**Example**  
```js
var hbjs = require("handbrake-js");
```

* [handbrake-js](#module_handbrake-js)
  * [class: ~Handbrake](#module_handbrake-js..Handbrake)
    * _instance_
      * [.output](#module_handbrake-js..Handbrake#output) → <code>string</code>
      * [.options](#module_handbrake-js..Handbrake#options) → <code>object</code>
    * _events_
      * ["start"](#module_handbrake-js..Handbrake#event_start)
      * ["begin"](#module_handbrake-js..Handbrake#event_begin)
      * ["progress" (progress)](#module_handbrake-js..Handbrake#event_progress)
      * ["output" (output)](#module_handbrake-js..Handbrake#event_output)
      * ["error" (error)](#module_handbrake-js..Handbrake#event_error)
      * ["end"](#module_handbrake-js..Handbrake#event_end)
      * ["complete"](#module_handbrake-js..Handbrake#event_complete)
  * [.spawn(options)](#module_handbrake-js.spawn) ⇒ <code>[Handbrake](#module_handbrake-js..Handbrake)</code>
  * [.exec(options, [onComplete])](#module_handbrake-js.exec)
  * [.cliOptions](#module_handbrake-js.cliOptions) → <code>array</code>

<a name="module_handbrake-js..Handbrake"></a>
###class: hbjs~Handbrake
A thin wrapper on the handbrakeCLI child_process handle. An instance of this class is returned by `hbjs.spawn()`.

**Extends:** <code>[EventEmitter](http://nodejs.org/api/events.html)</code>  
**Scope**: inner class of <code>[handbrake-js](#module_handbrake-js)</code>  
**Emits**: <code>[start](#module_handbrake-js..Handbrake#event_start)</code>, <code>[begin](#module_handbrake-js..Handbrake#event_begin)</code>, <code>[progress](#module_handbrake-js..Handbrake#event_progress)</code>, <code>[output](#module_handbrake-js..Handbrake#event_output)</code>, <code>[error](#module_handbrake-js..Handbrake#event_error)</code>, <code>[end](#module_handbrake-js..Handbrake#event_end)</code>, <code>[complete](#module_handbrake-js..Handbrake#event_complete)</code>

* [class: ~Handbrake](#module_handbrake-js..Handbrake)
  * _instance_
    * [.output](#module_handbrake-js..Handbrake#output) → <code>string</code>
    * [.options](#module_handbrake-js..Handbrake#options) → <code>object</code>
  * _events_
    * ["start"](#module_handbrake-js..Handbrake#event_start)
    * ["begin"](#module_handbrake-js..Handbrake#event_begin)
    * ["progress" (progress)](#module_handbrake-js..Handbrake#event_progress)
    * ["output" (output)](#module_handbrake-js..Handbrake#event_output)
    * ["error" (error)](#module_handbrake-js..Handbrake#event_error)
    * ["end"](#module_handbrake-js..Handbrake#event_end)
    * ["complete"](#module_handbrake-js..Handbrake#event_complete)

<a name="module_handbrake-js..Handbrake#output"></a>
####handbrake.output → <code>string</code>
A `String` containing all handbrakeCLI output

<a name="module_handbrake-js..Handbrake#options"></a>
####handbrake.options → <code>object</code>
the options HandbrakeCLI was spawned with

<a name="module_handbrake-js..Handbrake#event_start"></a>
####event: "start"
Fired as HandbrakeCLI is launched. Nothing has happened yet.

<a name="module_handbrake-js..Handbrake#event_begin"></a>
####event: "begin"
Fired when encoding begins. If you're expecting an encode and this never fired, something went wrong.

<a name="module_handbrake-js..Handbrake#event_progress"></a>
####event: "progress" (progress)
Fired at regular intervals passing a `progress` object.

| Param | Type | Description |
| ----- | ---- | ----------- |
| progress | <code>object</code> | details of encode progress |
| progress.taskNumber | <code>number</code> | current task index |
| progress.taskCount | <code>number</code> | total tasks in the queue |
| progress.percentComplete | <code>number</code> |  |
| progress.fps | <code>number</code> | Frames per second |
| progress.avgFps | <code>number</code> | Average frames per second |
| progress.eta | <code>string</code> | Estimated time until completion |
| progress.task | <code>string</code> | Task description, either "Encoding" or "Muxing" |

<a name="module_handbrake-js..Handbrake#event_output"></a>
####event: "output" (output)
| Param | Type | Description |
| ----- | ---- | ----------- |
| output | <code>string</code> | An aggregate of `stdout` and `stderr` output from the underlying HandbrakeCLI process. |

<a name="module_handbrake-js..Handbrake#event_error"></a>
####event: "error" (error)
| Param | Type | Description |
| ----- | ---- | ----------- |
| error | <code>Error</code> | All operational exceptions are delivered via this event. |
| error.name | <code>string</code> | One of `HandbrakeCLINotFound`, `HandbrakeCLIError`, `NoTitleFound`, `HandbrakeCLICrash` or `ValidationError` |
| error.message | <code>string</code> |  |
| error.errno | <code>string</code> |  |

<a name="module_handbrake-js..Handbrake#event_end"></a>
####event: "end"
Fired on successful completion of an encoding task. Always follows a `begin` event, with some `progress` in between.

<a name="module_handbrake-js..Handbrake#event_complete"></a>
####event: "complete"
Fired when HandbrakeCLI exited cleanly. This does not necessarily mean your encode completed as planned..

<a name="module_handbrake-js.spawn"></a>
###hbjs.spawn(options) ⇒ <code>[Handbrake](#module_handbrake-js..Handbrake)</code>
Spawns a HandbrakeCLI process with the supplied [options](https://trac.handbrake.fr/wiki/CLIGuide#options), returning an instance of `Handbrake` on which you can listen for events.

| Param | Type | Description |
| ----- | ---- | ----------- |
| options | <code>Object</code> | [Options](https://trac.handbrake.fr/wiki/CLIGuide#options) to pass directly to HandbrakeCLI |

**Example**  
```js
var hbjs = require("handbrake-js");

hbjs.spawn(options)
    .on("error", console.error)
    .on("output", console.log);
```
<a name="module_handbrake-js.exec"></a>
###hbjs.exec(options, [onComplete])
Runs HandbrakeCLI with the supplied [options](https://trac.handbrake.fr/wiki/CLIGuide#options) calling the supplied callback on completion. The exec method is best suited for short duration tasks where you can wait until completion for the output.

| Param | Type | Description |
| ----- | ---- | ----------- |
| options | <code>Object</code> | [Options](https://trac.handbrake.fr/wiki/CLIGuide#options) to pass directly to HandbrakeCLI |
| \[onComplete\] | <code>function</code> | If passed, `onComplete(err, stdout, stderr)` will be called on completion, `stdout` and `stderr` being strings containing the HandbrakeCLI output. |

**Example**  
```js
var hbjs = require("handbrake-js");

hbjs.exec({ preset-list: true }, function(err, stdout, stderr){
    if (err) throw err;
    console.log(stdout);
});
```
<a name="module_handbrake-js.cliOptions"></a>
###hbjs.cliOptions → <code>array</code>
[Command-line-args](https://github.com/75lb/command-line-args) option definitions, useful when building a CLI.
