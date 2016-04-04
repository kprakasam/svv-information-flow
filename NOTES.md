1. Source 
    
    1.1 Require VProxy implementation.<br/>
    1.2 Define a function that taints or perform custom operaton resulting in an VProxy instance.<br/>
    1.3. Require the above function and code rest of the functionality.
    
2. Compilation
 
    1.1 Includes macros in 'macros/index.js' that overridies JavaScript operators with unary or binary functions of VProxy into the supplied source file.<br/>
    1.2  Compiles resultant input file resulting in all unary and binary operations being replaced by unary or binary function calls of VProxy.
    
3. Runtime
    
    2.1 VProxy's unary and binary operations apply JavaScript operations if the operands are not an instance of VProxy.<br/>
    2.2 If the operands are instance of VProxy, value is unwraped and unary or left or right function of handler of the given VProxy type (ex: tainting VProxy) is invoked.<br/>
    2.3 Handler now perform the actual operation. (If any of these operation are one of the overrriden operations this will inturn delegate to VProxy to unwrap or to perform VProxy implemented operation on  the right hand side operand. 

4. Interanals of VProxy

    1.3 Key being the underlying proxy and the value being a composite madeup of handler, original value, and classifier key.
    1.4 Unary/binary function calls verify is a operand is a VProxy and extract original value and calls left or right function of the proxy handler.
    1.5 Handler in turn performs invoked unray or binary function which will do the defalu op on the values.
    
2. Changes
    2.1 Don't include VProxy definition in the compile step
    2.2 So the source file being compiled doesn't have this appended to it and keeping it clear.
    
3. Implementing Taint
    3.1 Implement a function to taint any value.
    3.2 This function will return a VProxy with a specific classification key
    3.3 Also implement Unary and binary operations for the tainted values
    3.4 Compile it with vjs so the unary and binary ops delegate to unary and binary operators contained in VProxy.