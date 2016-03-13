node-libclang
=============
node.js module for libclang and parsing c-style source from javascript

AST Traversal
-------------
```javascript
var libclang = require('libclang');

var index = new libclang.Index();
var tu = libclang.TranslationUnit.fromSource(index, 'myLibrary.h', ['-I/path/to/my/project']);

tu.cursor.visitChildren(function (parent) {
  switch (this.kind) {
    case libclang.Type.CXCursor_FunctionDecl:
      console.log(this.spelling);
      break;
  }
  return libclang.CXChildVisit_Continue;
});

index.dispose();
tu.dispose();
````

Generate FFI Bindings
---------------------
This has been moved to its own library `npm install -g ffi-generate`

See also https://github.com/tjfontaine/node-ffi-generate

Notes
-----
Not all of libclang is wrapped yet, but there's enough for
[ffi-generate](https://github.com/tjfontaine/node-ffi-generate) to regenerate
the dynamic clang bindings.

The native wrapper isn't completely fleshed out or free of errors. Enough is
wrapped to allow for C modules to be successfully generated by `lib/generateffi.js`.
