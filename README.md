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

### I2C

Include:
```c
#include <applibs/i2c.h>
#include <unistd.h>
```

Code:
```c
// Initialize
int fd = I2CMaster_Open(1);
if (fd < 0) /* Error handing */;
if (I2CMaster_SetBusSpeed(fd, I2C_BUS_SPEED_STANDARD) != 0) /* Error handing */;
if (I2CMaster_SetTimeout(fd, 100) != 0) /* Error handing */;

// Write
const uint8_t writeData[] = { 0x2d, 0x08 };
if (I2CMaster_Write(fd, 0x53, writeData, sizeof(writeData)) != sizeof(writeData)) /* Error handing */;

// Read
uint8_t readData[6];
ssize_t readSize = I2CMaster_Read(fd, 0x53, readData, sizeof(readData));
if (readSize < 0) /* Error handing */;

// Write and read
const uint8_t write2Data[] = { 0x32 };
uint8_t read2Data[6];
ssize_t read2Size = I2CMaster_WriteThenRead(fd, 0x53, write2Data, sizeof(write2Data), read2Data, sizeof(read2Data));
if (read2Size < 0) /* Error handing */;

// Terminate
if (close(fd) != 0) /* Error handing */;
```

See also:
* [I2CMaster_Open](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-i2c/function-i2cmaster-open)
* [I2CMaster_SetBusSpeed](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-i2c/function-i2cmaster-setbusspeed)
* [I2CMaster_SetTimeout](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-i2c/function-i2cmaster-settimeout)
* [I2CMaster_Write](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-i2c/function-i2cmaster-write)
* [I2CMaster_Read](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-i2c/function-i2cmaster-read)
* [I2CMaster_WriteThenRead](https://docs.microsoft.com/en-us/azure-sphere/reference/applibs-reference/applibs-i2c/function-i2cmaster-writethenread)

## RTApp

Code snippets for real-time capable application.

