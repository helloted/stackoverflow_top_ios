# Objective-C里类型大小
[Types in objective-c on iPhone](https://stackoverflow.com/questions/2107544/types-in-objective-c-on-iphone)

___



> 1

```
  NSLog(@"Primitive sizes:");
  NSLog(@"The size of a char is: %d.", sizeof(char));
  NSLog(@"The size of short is: %d.", sizeof(short));
  NSLog(@"The size of int is: %d.", sizeof(int));
  NSLog(@"The size of long is: %d.", sizeof(long));
  NSLog(@"The size of long long is: %d.", sizeof(long long));
  NSLog(@"The size of a unsigned char is: %d.", sizeof(unsigned char));
  NSLog(@"The size of unsigned short is: %d.", sizeof(unsigned short));
  NSLog(@"The size of unsigned int is: %d.", sizeof(unsigned int));
  NSLog(@"The size of unsigned long is: %d.", sizeof(unsigned long));
  NSLog(@"The size of unsigned long long is: %d.", sizeof(unsigned long long));
  NSLog(@"The size of a float is: %d.", sizeof(float));
  NSLog(@"The size of a double is %d.", sizeof(double));

  NSLog(@"Ranges:");
  NSLog(@"CHAR_MIN:   %c",   CHAR_MIN);
  NSLog(@"CHAR_MAX:   %c",   CHAR_MAX);
  NSLog(@"SHRT_MIN:   %hi",  SHRT_MIN);    // signed short int
  NSLog(@"SHRT_MAX:   %hi",  SHRT_MAX);
  NSLog(@"INT_MIN:    %i",   INT_MIN);
  NSLog(@"INT_MAX:    %i",   INT_MAX);
  NSLog(@"LONG_MIN:   %li",  LONG_MIN);    // signed long int
  NSLog(@"LONG_MAX:   %li",  LONG_MAX);
  NSLog(@"ULONG_MAX:  %lu",  ULONG_MAX);   // unsigned long int
  NSLog(@"LLONG_MIN:  %lli", LLONG_MIN);   // signed long long int
  NSLog(@"LLONG_MAX:  %lli", LLONG_MAX);
  NSLog(@"ULLONG_MAX: %llu", ULLONG_MAX);  // unsigned long long int
```

#### 32位机

```
Primitive sizes:
The size of a char is: 1.                
The size of short is: 2.                 
The size of int is: 4.                   
The size of long is: 4.                  
The size of long long is: 8.             
The size of a unsigned char is: 1.       
The size of unsigned short is: 2.        
The size of unsigned int is: 4.          
The size of unsigned long is: 4.         
The size of unsigned long long is: 8.    
The size of a float is: 4.               
The size of a double is 8.               
Ranges:                                  
CHAR_MIN:   -128                         
CHAR_MAX:   127                          
SHRT_MIN:   -32768                       
SHRT_MAX:   32767                        
INT_MIN:    -2147483648                  
INT_MAX:    2147483647                   
LONG_MIN:   -2147483648                  
LONG_MAX:   2147483647                   
ULONG_MAX:  4294967295                   
LLONG_MIN:  -9223372036854775808         
LLONG_MAX:  9223372036854775807          
ULLONG_MAX: 18446744073709551615 
```

#### 64位机

```
The size of a char is: 1.
The size of short is: 2.
The size of int is: 4.
The size of long is: 8.
The size of long long is: 8.
The size of a unsigned char is: 1.
The size of unsigned short is: 2.
The size of unsigned int is: 4.
The size of unsigned long is: 8.
The size of unsigned long long is: 8.
The size of a float is: 4.
The size of a double is 8.
Ranges:
CHAR_MIN:   -128
CHAR_MAX:   127
SHRT_MIN:   -32768
SHRT_MAX:   32767
INT_MIN:    -2147483648
INT_MAX:    2147483647
LONG_MIN:   -9223372036854775808
LONG_MAX:   9223372036854775807
ULONG_MAX:  18446744073709551615
LLONG_MIN:  -9223372036854775808
LLONG_MAX:  9223372036854775807
ULLONG_MAX: 18446744073709551615
```