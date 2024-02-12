
레퍼런스 :
https://dspace.vutbr.cz/bitstream/handle/11012/189195/final-thesis.pdf?sequence=-1&isAllowed=y


```
// debugger bypass

    var ContextWrapper = Java.use("android.content.ContextWrapper");

    var Debug = Java.use("android.os.Debug");

    var FLAG_DEBUGGABLE = 1 << 1;

  

    ContextWrapper.getApplicationInfo.implementation = function () {

        var appInfo = this.getApplicationInfo.call(this);    

        appInfo.flags.value &= ~FLAG_DEBUGGABLE;    

        return appInfo;

    };

  

    Debug.isDebuggerConnected.implementation = function () {

        return false;

    }
```
