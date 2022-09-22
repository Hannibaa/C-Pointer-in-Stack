// C-Primitive-Concepts
// How to accesse from only one pointer to whole stack variable 
// Just
// Next will see how to use pointer to read inside function, struct(structure data type) and class;
#include <stdio.h>
#include <stdlib.h>


int main()
{
    // Distribution of Address in stack , pointer in stack
    int a,b,c;
    char ch;
    char s[6]= "abcde";
    int* pa = &a;
    
    
    // Difference of byte in stack between variable
    c = (int)(&b) - (int)(&a);
    b = (int)(&c) - (int)(&a);
    a = (int)(&c) - (int)(&b);
    
    printf("Address(b)[%X] - Address(a)[%X] = [%d]\n", &b, &a, c);
    printf("Address(c)[%X] - Address(a)[%X] = [%d]\n", &c, &a, b);
    printf("Address(c)[%x] - Address(b)[%x] = [%d]\n", &c, &b, a);

	int inc = (int)(&a + 1) - (int)(&a);

	printf("Address(a+1)[%x]; Increment=[%d]\n", &a + 1, inc );
	printf("Position of b is [&a+%d]\n", c / inc);
	printf("Address(b) = [%X], Address(a+8) = [%X]\n",&b, &a+8);

	//we can read the value of b by address operation  of a;
         a = 3; b = 12;
	 printf(" a = [%d]\n b= [%d]\n", a, *(&a + 8));
	
	//*(&a + 8) = 11; //check this expression ?
	// using pointer to modify value of a;
	*pa = 7;
	printf("Modify value of (a) by pointer pa ; a = [%d], b = [%d]\n", a,b);

	// test if we can use this pointer to a to modify b value!!
	*(pa + 8) = 9;
	printf("Modify value of (b) by pointer pa ; a = [%d], b = [%d]\n",a , b);

	//we try by same pointer to modify value of c
	*(pa + 16) = 50;
	
	printf("Modify value of (c) by pointer pa ; c = [%d]\n", c);

	system("pause");
	system("cls");

	printf("\t\t------------ we check with character ---------------\n");

	//calculate offset between c and ch;
	printf("Address(ch)[%X] - Address(c)[%X] = [%d]\n",&ch,&c, (int)(&ch) - (int)(&c));

	// use pointer of a to modify char
        *(pa + 24) = (int)('h');
	printf("Modift value of ch by ; *(pa + 24) = (int)('h')\n");
	printf("Value of ch is [%c]\n", ch);
	

	//we calculate the offset between ch and s;
	printf("Address(s)[%X] - Address(ch)[%X] = [%d]\n",&s,&ch, (int)(s) - (int)(&ch));
        printf("Offset &s[0][%X] and &s[1][%X] is [%d]\n",&s[0],&s[1], (int)(&s[1]) - (int)(&s[0]));

	printf("String (s) is [%s]\n", s);
	printf("Address(s)[%X] Address(pa+32)[%X]\n", &s, pa + 32);

	// use pointer pa to write in string s
        (char)*(pa + 32) = 'A';
	(char)*(pa + 34) = 'B';
	printf("String (s) is [%s]\n", s);

	*((char*)(pa + 32)) = 'G';
	//*((char*)(pa + 33)) = 'H';             // this not work
	*((char*)(pa + 32) + 1) = 'H';           // this work; formated(casted) pointer at pa+32 to char* 
	printf("String (s) is [%s]\n", s);       // and start counting.

	// use pointer pa to write in string s without casting;
	*(pa + 32) = 'D';                     //this pointer take it as integer so 
	printf("String (s) is [%s]\n", s);    // check how it work to fill string s by integer pointer
	printf("All value of String s ;[%c][%c][%c][%c][%c][%c]\n", s[0], s[1], s[2], s[3], s[4],s[5]);
	system("pause");
	system("cls");

	printf(" ------------------------check with char pointer to read integer-----------\n");

	printf("Value of a = [%d]\n", a);
	a = (int)&a;
	printf("Value of a = [%X]\n", a);
        printf("Value of [ a ] = [%X][%X][%X][%X]\n",(unsigned) * ((char*)pa),
		                                          (unsigned) * ((char*)pa + 1),
		                                           (unsigned) * ((char*)pa + 2), 
		                                            (unsigned) * ((char*)pa + 3));
	// You can stor these value in string 's' 
	s[0] = *((char*)pa);      s[1] = *((char*)pa+1);
	s[2] = *((char*)pa+2);      s[3] = *((char*)pa+3);
	s[4] = '\0';
	printf("Value of integer a is string s = [%s]\n", s);

	getchar();
  return 0;
  
  }
