<h1>ft_printf 💻🖨️</h1> <h2 align='right'>Final Grade 100/125 ✅ </h2>

This project includes a custom implementation of a printf-like function in C, named ft_printf. </br>
The ft_printf function is a function that processes a formatted string and a variable number of arguments, converting and outputting the arguments based on the specified format.

<h3>The prototype of ft_printf() is:</h3>

```c
int ft_printf(const char *, ...);
```

<h2 align="center"> Description </h2>

<h3>Conversion Logic:</h3>

- %c: Converts and outputs a single character.
- %s: Converts and outputs a string.
- %p: Converts and outputs a pointer address in hexadecimal format.
- %d / %i: Converts and outputs a signed decimal integer.
- %u: Converts and outputs an unsigned decimal integer.
- %x: Converts and outputs a number in hexadecimal format with lowercase letters.
- %X: Converts and outputs a number in hexadecimal format with uppercase letters.
- %%: Outputs a literal percent sign.

The conversion and output for each format specifier is handled by a helper function ft_convert, which uses a variable argument list to retrieve the corresponding argument and pass it to the appropriate output function.

```c
int	ft_convert(char c, va_list arg)
{
	if (c == 'c')
		return (ft_putchar(va_arg(arg, int)));
	else if (c == 's')
		return (ft_putstr(va_arg(arg, char *)));
	else if (c == 'p')
		return (ft_pointer(va_arg(arg, unsigned long)));
	else if (c == 'd' || c == 'i')
		return (ft_putnbr(va_arg(arg, int)));
	else if (c == 'u')
		return (ft_putunbr(va_arg(arg, unsigned int)));
	else if (c == 'x')
		return (ft_hexlower(va_arg(arg, int)));
	else if (c == 'X')
		return (ft_hexupper(va_arg(arg, int)));
	else if (c == '%')
		return (ft_putchar('%'));
	return (0);
}
```

<h3>Detailed Function Descriptions</h3>

- ft_printf: Parses the format string and uses ft_convert to handle each conversion specifier.
- ft_convert: Determines the type of conversion based on the format specifier and calls the appropriate function to handle the conversion and output.
- ft_putchar
  - Purpose: Outputs a single character.
  - Implementation: Uses the write system call to write the character c to the standard output (file descriptor 1).
  - Return Value: Always returns 1, indicating that one character was written.
- ft_putstr
  - Purpose: Outputs a string.
  - Implementation: Iterates through each character of the string str, using ft_putchar to output each character. If str is NULL, it outputs the string "(null)".
  - Return Value: Returns the number of characters written.
- ft_hexlower
  - Purpose: Outputs an unsigned integer in hexadecimal format with lowercase letters.
  - Implementation: Recursively divides the number nb by 16, using the remainder to determine the corresponding hexadecimal character from the string "0123456789abcdef".
  - Return Value: Returns the number of characters written.
- ft_hexupper
  - Purpose: Outputs an unsigned integer in hexadecimal format with uppercase letters.
  - Implementation: Similar to ft_hexlower, but uses the string "0123456789ABCDEF" to determine the hexadecimal characters.
  - Return Value: Returns the number of characters written.
- ft_hexptr
  - Purpose: Outputs an unsigned long integer in hexadecimal format with lowercase letters.
  - Implementation: Similar to ft_hexlower, but works with an unsigned long type.
  - Return Value: Returns the number of characters written.
- ft_pointer
  - Purpose: Outputs a pointer address in hexadecimal format.
  - Implementation: Outputs the prefix "0x" followed by the address in hexadecimal format using ft_hexptr.
  - Return Value: Returns the total number of characters written, including the "0x" prefix.
- ft_putunbr
  - Purpose: Outputs an unsigned decimal integer.
  - Implementation: Recursively divides the number nb by 10 to break it into individual digits, outputting each digit using ft_putchar.
  - Return Value: Returns the number of characters written.
- ft_putnbr
  - Purpose: Outputs a signed decimal integer.
  - Implementation: Handles the special case of the minimum integer value -2147483648 separately. For negative numbers, outputs the '-' sign and converts the number to positive. Recursively divides the number nb by 10 to 
    break it into individual digits, outputting each digit using ft_putchar.
  - Return Value: Returns the number of characters written.


<h3>Example Usage</h3>

```c
#include "ft_printf.h"

int main(void)
{
    ft_printf("Character: %c\n", 'A');
    ft_printf("String: %s\n", "Hello, World!");
    ft_printf("Pointer: %p\n", (void *)0x7ffee3bff6b8);
    ft_printf("Integer: %d\n", 42);
    ft_printf("Unsigned: %u\n", 42);
    ft_printf("Hex (lowercase): %x\n", 255);
    ft_printf("Hex (uppercase): %X\n", 255);
    ft_printf("Percent sign: %%\n");
    return 0;
}

```
