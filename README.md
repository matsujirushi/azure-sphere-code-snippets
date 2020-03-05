# Azure Sphere Code Snippets

## HLApp

Code snippets for high-level application.

### Digital In

Include:
```c
#include <applibs/gpio.h>
#include <unistd.h>
```

Code:
```c
// Initialize
int fd = GPIO_OpenAsInput(4);
if (fd < 0) /* Error handing */;

// Input
GPIO_Value_Type value;
if (GPIO_GetValue(fd, &value) != 0) /* Error handing */;
// value is GPIO_Value_High or GPIO_Value_Low

// Terminate
if (close(fd) != 0) /* Error handing */;
```

See also:
* [GPIO_OpenAsInput](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-gpio/function-gpio-openasinput)
* [GPIO_GetValue](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-gpio/function-gpio-getvalue)

### Digital Out

Include:
```c
#include <applibs/gpio.h>
#include <unistd.h>
```

Code:
```c
// Initialize
int fd = GPIO_OpenAsOutput(4, GPIO_OutputMode_PushPull, GPIO_Value_Low);
if (fd < 0) /* Error handing */;

// Output low
if (GPIO_SetValue(fd, GPIO_Value_Low) != 0) /* Error handing */;

// Terminate
if (close(fd) != 0) /* Error handing */;
```

See also:
* [GPIO_OpenAsOutput](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-gpio/function-gpio-openasoutput)
* [GPIO_SetValue](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-gpio/function-gpio-setvalue)

## RTApp

Code snippets for real-time capable application.

