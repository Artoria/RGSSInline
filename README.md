RGSSInline
==========

An RubyInline-like framework in RGSSS (Ruby Game Scripting System Series of RPG Makers' )

Only depends on, (no other things required, *even a binary form compiler like gcc*):
* https://github.com/Artoria/RMSFX, which has a dependency of:
* https://github.com/jjyg/Metasm, which contains an RGSSS-compliance C compiler in pure Ruby




Sample Code
============
```ruby
class A
  inline do |builder|
    builder.c "
      long factorial(int max){
        int i=max, result=1;
        while (i >= 2) { result *= i--; }
        return result;
      }
      
      char *test(){
        return \"Hello\";
      }
      
      char *test_reverse(char *st){
        char *ed = st;
        int n = 0, i;
        while(*ed) ++ ed, ++n;
        
        for(i = 0; i < n - i - 1; ++i){
          char p = st[i]; st[i] = st[n - i - 1]; st[n - i - 1] = p;
        }
        return st;
      }
       
      
      
      void test_msgbox(char *msgbox){
         int __stdcall MessageBoxA(int, char *, int, int);
         MessageBoxA(0, msgbox, 0, 16);
      }
    "
    
    builder.c_raw "
       int add(int argc, int *argv, int self){
         return argv[0] + argv[1] - 1;
       }
    
    "
  end
end

A.new.test_msgbox("Hello")
```
