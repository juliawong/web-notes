# I/O

* `cin` and `cout`
* `scanf` and `printf` are faster if taking more input and outputting more

# Preprocessor directives

* Resolved before compilation
* `#define identifier replacement`
* `#define getmax(a,b) a>b?a:b`
* Replace argument with string literal version
  * `#define str(x) #x`
  * `cout << str(test);` becomes `cout << "test"'`
* Concatenate arguments
  * `#define glue(a,b) a ## b`
  * `glue(c,out) << "test";` becomes `cout << "test"`
* Conditionals `#ifdef`, `#ifndef`, `#if`, `#endif`, `#else` and `#elif`
