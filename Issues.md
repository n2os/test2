테스트코드
<pre>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

void memory_leak( void)
{
    char    *p_leak;
    int      ndx;

    p_leak  = malloc(  10);

    for ( ndx = 0; ndx < 10; ndx++)
    {
        p_leak[ndx] = 'a';
    }
    for ( ndx = 0; ndx < 10; ndx++)
    {
        printf( "%c", p_leak[ndx]);
    }
}

void memory_normal( void)
{
    char * p_leak;
    p_leak  = malloc(10);
    free (p_leak);
}

int main( void)
{
  int i = 0;

  while (1)
  {
    if (i++ > 10)
      break;

    memory_leak();
    memory_normal();

    sleep(1);
  }
}
</pre>

컴파일
<pre>
gcc -g test.c -o app_test
</pre>

valgrind 실행
<pre>
valgrind --leak-check=yes ./app_test
</pre>
