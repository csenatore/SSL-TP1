# SSL-TP1
1. Al preprocesar :
extern int __vsprintf_chk (char * restrict, int, size_t,
      const char * restrict, va_list);







extern int __vsnprintf_chk (char * restrict, size_t, int, size_t,
       const char * restrict, va_list);
# 412 "/usr/include/stdio.h" 2 3 4
# 2 "hello2.c" 2

int main(void){
 int i=42;
 prontf("La respuesta es %d\n");
		
Se observa el código escrito y la definición de las funciones incluidas en la biblioteca stdio.h

2.Crea el hello2.i con el comando gcc hello2.c -E >hello2.i

Se pega lo mostrado anteriormente por consola en un archivo .i

3. Genero nuevo archivo hello3.c

4.  Int printf(const char *s, …)
	- declaración de funcionarios printf recibe por lo menos un puntero char
	- puede o no tener mas argumentos (por eso el …)
  
5. Al preprocesar en este caso, como declaramos la función y no hicimos include de biblioteca, se verán iguales el .c y el .i

6. Al intentar compilar de ven errores:

hello3.c:4:2: warning: implicit declaration of function 'prontf' is invalid in
      C99 [-Wimplicit-function-declaration]
 prontf("La respuesta es %d\n");
 ^
hello3.c:4:33: error: expected '}'
 prontf("La respuesta es %d\n");
                                ^
hello3.c:2:15: note: to match this '{'
int main(void){
              
Se ven errores porque:
  - Declaración de funcion prontf no declarada
  - La funcion prontf esperan un parametro que no estamos pasando
  - La funcion main no termina en llave
  - Hay un warning porque creamos una variable int que noestamos usando
  
7. Generar el .s

8. El .s tiene código en Assembler
	.section	__TEXT,__text,regular,pure_instructions
	.macosx_version_min 10, 13
	.globl	_main                   ## -- Begin function main
	.p2align	4, 0x90
_main:                                  ## @main
	.cfi_startproc
## BB#0:
	pushq	%rbp
Lcfi0:
	.cfi_def_cfa_offset 16
Lcfi1:
	.cfi_offset %rbp, -16
	movq	%rsp, %rbp
Lcfi2:
	.cfi_def_cfa_register %rbp
	subq	$16, %rsp
	leaq	L_.str(%rip), %rdi
	movl	$42, -4(%rbp)
	movl	-4(%rbp), %esi
	movb	$0, %al
	callq	_printf
	xorl	%esi, %esi
	movl	%eax, -8(%rbp)          ## 4-byte Spill
	movl	%esi, %eax
	addq	$16, %rsp
	popq	%rbp
	retq
	.cfi_endproc
                                        ## -- End function
	.section	__TEXT,__cstring,cstring_literals
L_.str:                                 ## @.str
	.asciz	"La respuesta es %d\n"


.subsections_via_symbols

9. Al compilar a código de maquina, el archivo generado (.o) no es legible, se ven cogidos y caracteres no alfanuméricos

10. Vincular con la biblio std y genera exe. Tira error al intentar ejecutar
-clang: error: argument to '-o' is missing (expected 1 value)

11.genero hello5.c

12.
hello5.c:7:2: warning: implicit declaration of function 'prontf' is invalid in
      C99 [-Wimplicit-function-declaration]
 prontf("La respuesta es %d\n");
 ^
1 warning generated.
Undefined symbols for architecture x86_64:
  "_prontf", referenced from:
      _main in hello5-dfb663.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocat
Error y warning: no estas declarando funcion 

13. Sigue tirando warning porque no le paso ningún parámetro al printf

14.  Genero hello7.c 

15. Al ejecutarlo devuelve “la respuesta es 42”, funciona porque estamos incluyendo librería donde se define la función printf y a la funcion printf le estamos pasando como paramento el valor int 42
