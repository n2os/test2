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


결과확인
<pre>
root@N1:~# valgrind --leak-check=yes ./app_test
==1776== Memcheck, a memory error detector
==1776== Copyright (C) 2002-2015, and GNU GPL'd, by Julian Seward et al.
==1776== Using Valgrind-3.12.0.SVN and LibVEX; rerun with -h for copyright info
==1776== Command: ./app_test
==1776==
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa==1776==
==1776== HEAP SUMMARY:
==1776==     in use at exit: 110 bytes in 11 blocks
==1776==   total heap usage: 23 allocs, 12 frees, 1,244 bytes allocated
==1776==
==1776== 110 bytes in 11 blocks are definitely lost in loss record 1 of 1
==1776==    at 0x4C2CB3F: malloc (in /usr/lib/valgrind/vgpreload_memcheck-amd64-linux.so)
==1776==    by 0x108781: memory_leak (test.c:12)
==1776==    by 0x10881F: main (test.c:42)
==1776==
==1776== LEAK SUMMARY:
==1776==    definitely lost: 110 bytes in 11 blocks
==1776==    indirectly lost: 0 bytes in 0 blocks
==1776==      possibly lost: 0 bytes in 0 blocks
==1776==    still reachable: 0 bytes in 0 blocks
==1776==         suppressed: 0 bytes in 0 blocks
==1776==
==1776== For counts of detected and suppressed errors, rerun with: -v
==1776== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
</pre>
