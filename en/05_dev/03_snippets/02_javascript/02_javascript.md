# JavaScript

## Basic module

The JavaScript is modular and based on a base module that is initialised when the page is called. It creates a global object with the name `goobiWorkflowJS`. Methods are attached to this object through further modules and can thus be called in its scope.

{% code title="goobiWorkflowJS.js" %}
```javascript
var goobiWorkflowJS = ( function() {
    'use strict';

    // global object
    var goobiWorkflow = {};

    // private variables
    var _debug = false;
    var _defaults = {};

    goobiWorkflow.init = function( config ) {
        if ( _debug ) {
            console.log( 'Initializing: goobiWorkflow.init' );
            console.log( '--> config = ', config );
        }

        $.extend( true, _defaults, config );
    }

    return goobiWorkflow;

} )( jQuery );
```
{% endcode %}

## Add-on module

The global object `goobiWorkflow` is passed to the add-on module, thus allowing the object to be extended with additional methods. In a module, methods or variables can be defined that can only be called in the module `(private) or in the global object`(public).

{% code title="goobiWorkflowJS.module.js" %}
```javascript
var goobiWorkflowJS = ( function( goobiWorkflow ) {
    'use strict';

    // private variables
    var _debug = false;
    var _defaults = {};

    goobiWorkflow.module = {
        /**
         * @description Method to initialize the module.
         * @method init
         */
        init: function( config ) {
            if ( _debug ) {
                console.log( 'Initializing: goobiWorkflow.module.init' );
                console.log( '--> config = ', config );
            }

            $.extend( true, _defaults, config );
        },
        /**
         * @description Method to ...
         * @method myPublicMethod
         */
        myPublicMethod: function() {
            if ( _debug ) {
                console.log( 'EXECUTE: goobiWorkflow.module.myPublicMethod' );
            }

            // magic happens here...
        },
        /**
         * @description Public variable
         */
        myPublicVariable: 'can be String, Boolean, Array or Object',
    };

    /**
     * @description Method to ...
     * @method _myPrivateMethod
     */
    function _myPrivateMethod() {
        if ( _debug ) {
            console.log( 'EXECUTE: _myPrivateMethod' );
        }

        // magic happens here...
    }

    return goobiWorkflow;

} )( goobiWorkflowJS || {}, jQuery );
```
{% endcode %}