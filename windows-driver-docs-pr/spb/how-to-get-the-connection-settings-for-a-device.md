---
title: 如何获取设备的连接设置
description: 如果您的存储控制器驱动程序注册 EvtSpbTargetConnect 回调函数，存储 framework 扩展 (SpbCx) 调用此函数时 （外围设备驱动程序） 的控制器客户端发送 IRP_MJ_CREATE 请求以打开与目标的逻辑连接总线上的设备。 EvtSpbTargetConnect 回调响应，存储控制器驱动程序应调用 SpbTargetGetConnectionParameters 方法以获取目标设备的连接设置。 存储控制器驱动程序将这些设置存储和更高版本使用它们来访问响应来自客户端的 I/O 请求中的设备。
ms.assetid: B614993A-0EA9-4B91-A336-80EEF9BE3E69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 337e1089e103bc67e2da9b8d4ba96e1746ae4814
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545352"
---
# <a name="how-to-get-the-connection-settings-for-a-device"></a>如何获取设备的连接设置


如果您的存储控制器驱动程序注册[ *EvtSpbTargetConnect* ](https://msdn.microsoft.com/library/windows/hardware/hh450818)回调函数[存储框架扩展](https://msdn.microsoft.com/library/windows/hardware/hh406203)(SpbCx) 调用此函数时客户端 （外围设备驱动程序） 的控制器发送[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729)请求以打开到总线上的目标设备的逻辑连接。 以响应*EvtSpbTargetConnect*回调，存储控制器驱动程序应调用[ **SpbTargetGetConnectionParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh450926)方法以获取连接目标设备的设置。 存储控制器驱动程序将这些设置存储和更高版本使用它们来访问响应来自客户端的 I/O 请求中的设备。

例如，I2C 总线上的目标设备的连接设置包括设备、 地址宽度 （7 或 10 位） 和总线时钟频率，若要在访问设备的过程中使用的总线地址。 I2C 控制器驱动程序使用这些设置来配置要访问设备通过 I2C 总线的控制器。

存储控制器驱动程序调用**SpbTargetGetConnectionParameters**若要获取指向的指针*串行总线连接描述符*描述类型 I2C 串行总线的目标设备的连接或SPI。 此描述符包含连接信息普遍适用于这两种串行总线类型，并且后跟特定于设备连接到串行总线的信息。 有关此描述符的格式的详细信息，请参阅[ACPI 5.0 规范](https://www.uefi.org/specifications)。

在下面的代码示例，I2C 控制器驱动程序定义**PNP\_I2C\_串行\_总线\_描述符**结构。 此结构表示*I2C 串行总线连接描述符*，这是 ACPI 5.0 规范使用来描述的串行总线连接描述符，后跟连接设置特定于 I2C 术语总线。 第一个成员**PNP\_I2C\_串行\_总线\_描述符**结构**SerialBusDescriptor**，是[ **PNP\_串行\_总线\_描述符**](https://msdn.microsoft.com/library/windows/hardware/jj938062)结构，它表示串行总线连接描述符。 **ConnectionSpeed**并**SlaveAddress**成员包含特定于 I2C 的连接设置。

```cpp
#include <reshub.h>
#include <pshpack1.h>  

//
// See the ACPI 5.0 spec, section 6.4.3.8.2.1 (I2C Serial Bus Connection Descriptor).  
//
typedef struct _PNP_I2C_SERIAL_BUS_DESCRIPTOR {  
    PNP_SERIAL_BUS_DESCRIPTOR SerialBusDescriptor;  
    ULONG ConnectionSpeed;  
    USHORT SlaveAddress;  
    // Followed by optional vendor-specific data.
    // Followed by name of serial bus controller.
} PNP_I2C_SERIAL_BUS_DESCRIPTOR, *PPNP_I2C_SERIAL_BUS_DESCRIPTOR;  
  
#include <poppack.h>
```

Reshub.h 标头文件定义**PNP\_串行\_总线\_描述符**结构。 Pshpack1.h 和 poppack.h 标头文件来控制由编译器使用的结构对齐模式。

I2C 串行总线连接描述符是在其中相邻字段对齐到最接近的字节边界，而无需干预的间隙的已打包的数据结构。 因此，此说明符中的 16 位整数值可能会启动奇数字节边界上。 在前面的代码示例中，pshpack1.h 包含以告知编译器要打包相邻结构成员和 poppack.h 告知编译器要恢复默认结构的对齐方式。

**ConnectionSpeed**的成员**PNP\_I2C\_串行\_总线\_描述符**结构指定的频率，以赫兹表示，其中的在目标设备的访问过程时钟 I2C 总线。 **SlaveAddress**成员是目标设备的总线地址。 有些 I2C 控制器驱动程序，请**SlaveAddress**成员可能跟可选的特定于供应商的数据，但此数据不使用此代码示例中的驱动程序，因此，不是结构定义的一部分。

以下代码示例中，在上一示例中的 I2C 控制器驱动程序实现`GetTargetSettings`调用的例程[ **SpbTargetGetConnectionParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh450926)若要获取的连接设置有关 I2C 总线上的目标设备。 *目标*到此例程的输入的参数是目标设备的句柄。 *设置*输出参数是指向驱动程序分配[**存储\_连接\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh406204)结构到例程将写入一组的连接参数。 这些参数包括一个指向请求的连接设置。

```cpp
#define I2C_SERIAL_BUS_TYPE 0x01
#define I2C_SERIAL_BUS_SPECIFIC_FLAG_10BIT_ADDRESS 0x0001

typedef enum _I2C_ADDRESS_MODE
{
    AddressMode7Bit,
    AddressMode10Bit
} I2C_ADDRESS_MODE, *PI2C_ADDRESS_MODE;
  
typedef struct _I2C_TARGET_SETTINGS
{
    ULONG  ClockFrequency;
    ULONG  Address;
    I2C_ADDRESS_MODE  AddressMode;
} I2C_TARGET_SETTINGS, *PI2C_TARGET_SETTINGS;

NTSTATUS
GetTargetSettings(_In_ SPBTARGET Target, _Out_ PI2C_TARGET_SETTINGS Settings)
{
    PRH_QUERY_CONNECTION_PROPERTIES_OUTPUT_BUFFER Connection = NULL;
    SPB_CONNECTION_PARAMETERS Params;

    SPB_CONNECTION_PARAMETERS_INIT(&Params);
    SpbTargetGetConnectionParameters(Target, &Params);
    Connection = (PRH_QUERY_CONNECTION_PROPERTIES_OUTPUT_BUFFER)Params.ConnectionParameters;
    if (Connection->PropertiesLength < sizeof(PNP_SERIAL_BUS_DESCRIPTOR))
    {
        return STATUS_INVALID_PARAMETER;
    }

    PPNP_SERIAL_BUS_DESCRIPTOR Descriptor;

    Descriptor = (PPNP_SERIAL_BUS_DESCRIPTOR)Connection->ConnectionProperties;
    if (Descriptor->Tag != SERIAL_BUS_DESCRIPTOR ||
        Descriptor->SerialBusType != I2C_SERIAL_BUS_TYPE)
    {
        return STATUS_INVALID_PARAMETER;
    }

    PPNP_I2C_SERIAL_BUS_DESCRIPTOR I2CDescriptor;
    USHORT I2CFlags;

    I2CDescriptor = (PPNP_I2C_SERIAL_BUS_DESCRIPTOR)Connection->ConnectionProperties;
    Settings->Address = (ULONG)I2CDescriptor->SlaveAddress;
    I2CFlags = I2CDescriptor->SerialBusDescriptor.TypeSpecificFlags;
    Settings->AddressMode = 
                ((I2CFlags & I2C_SERIAL_BUS_SPECIFIC_FLAG_10BIT_ADDRESS) == 0) ? AddressMode7Bit : AddressMode10Bit;

    Settings->ClockFrequency = I2CDescriptor->ConnectionSpeed;

    return STATUS_SUCCESS;
}
```

在前面的代码示例中， [ **SpbTargetGetConnectionParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh450926)写入驱动程序分配的连接参数`Params`结构。 **ConnectionParameters**的成员`Params`指向[ **RH\_查询\_连接\_属性\_输出\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/jj938063)结构 （reshub.h 中定义），其**ConnectionProperties**成员是序列的第一个字节总线连接描述符; 此描述符的剩余字节数在后面紧跟**ConnectionProperties**成员。 指向缓冲区**ConnectionParameters**的成员`Params`足够大，以包含**RH\_查询\_连接\_属性\_输出\_缓冲区**结构，以及遵循此结构描述符个字节。

驱动程序实现`GetTargetSettings`前面的代码示例中的例程执行从收到的连接参数上的以下参数检查**SpbTargetGetConnectionParameters**:

-   验证中包含的串行总线连接描述符的大小[ **RH\_查询\_连接\_属性\_输出\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/jj938063)结构是至少**sizeof**(**PNP\_串行\_总线\_描述符**)。
-   验证串行总线连接描述符的第一个字节设置为序列号\_总线\_描述符 （常数值 0x8e 越权），根据 ACPI 5.0 规范的要求。
-   验证，串行总线连接描述符中的串行总线类型设置为 I2C\_串行\_总线\_类型 （常量值 0x01），用于标识为 I2C 串行总线类型。

在前面的代码示例，末尾\*`Settings`结构包含目标设备的连接设置 （总线地址、 地址宽度和总线时钟频率）。 I2C 控制器驱动程序使用这些连接设置来配置要访问设备的控制器。

 

 




