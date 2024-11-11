# JavaScript

## Basismodul

Das JavaScript ist modular aufgebaut und basiert auf einem Basismodul, welches beim Aufruf der Seite initialisiert wird. Es erschafft ein globales Objekt mit dem Namen `goobiWorkflowJS`. Diesem Objekt werden, durch weitere Module, Methoden angehängt und können so in dessen Scope aufgerufen werden.

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

## Zusatzmodul

Dem Zusatzmodul wird das globale Objekt `goobiWorkflow` übergeben und ermöglicht es so, das Objekt mit zusätzlichen Methoden zu erweitern. In einem Modul können Methoden oder Variablen definiert werden, die nur im Modul (private) oder im globalen Objekt (public) aufgerufen werden können.

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