## 1.Write a program that shows how static and auto variables behave differently.
```
#include <stdio.h>
void demo(){
        int x=1;
        static int y=1;
        printf("%d",x);
        printf("%d",y);
        x++;
        y++;
}
int main(){
  demo();
  demo();
}
output
First function call
11
Second function call
12
```
## 2
