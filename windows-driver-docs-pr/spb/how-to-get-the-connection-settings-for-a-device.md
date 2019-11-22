---
title: 如何获取设备的连接设置
description: 如果 SPB 控制器驱动程序注册了一个 EvtSpbTargetConnect 回调函数，则在控制器的客户端（外围设备驱动程序）发送 IRP_MJ_CREATE 请求以打开与目标的逻辑连接时，SPB framework extension （SpbCx）将调用此函数。总线上的设备。 为了响应 EvtSpbTargetConnect 回调，SPB 控制器驱动程序应调用 SpbTargetGetConnectionParameters 方法来获取目标设备的连接设置。 SPB 控制器驱动程序将存储这些设置，并在以后使用它们来访问设备，以响应客户端发出的 i/o 请求。
ms.assetid: B614993A-0EA9-4B91-A336-80EEF9BE3E69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cc63d5fa2d9db71420b1f2f4d9043f7429fa78d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843608"
---
# <a name="how-to-get-the-connection-settings-for-a-device"></a>如何获取设备的连接设置


如果 SPB 控制器驱动程序注册了一个[*EvtSpbTargetConnect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect)回调函数，则在控制器的客户端（外围设备驱动程序）发送[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求以打开到总线上的目标设备的逻辑连接时， [spb framework extension](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension) （SpbCx）将调用此函数。 为了响应*EvtSpbTargetConnect*回调，SPB 控制器驱动程序应调用[**SpbTargetGetConnectionParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters)方法来获取目标设备的连接设置。 SPB 控制器驱动程序将存储这些设置，并在以后使用它们来访问设备，以响应客户端发出的 i/o 请求。

例如，I2C 总线上的目标设备的连接设置包括设备的总线地址、地址宽度（7或10位）以及访问设备时要使用的总线时钟频率。 I2C 控制器驱动程序使用这些设置来配置控制器以通过 I2C 总线访问设备。

SPB 控制器驱动程序调用**SpbTargetGetConnectionParameters** ，以获取指向*串行总线连接描述符*的指针，该接口描述目标设备与 I2C 或 SPI 类型的串行总线的连接。 此描述符包含两种串行总线类型通用的连接信息，后跟特定于设备连接到的串行总线的信息。 有关此描述符的格式的详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)。

在下面的代码示例中，I2C 控制器驱动程序定义**PNP\_I2C\_串行\_总线\_描述符**结构。 此结构表示*i2c 串行总线连接描述符*，它是 ACPI 5.0 规范用于描述后跟特定于 I2C 总线的连接设置的串行总线连接描述符的术语。 **Pnp\_I2C\_串行\_总线\_描述符**结构**SerialBusDescriptor**的第一个成员是表示串行总线的[**pnp\_串行\_总线\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/reshub/ns-reshub-_pnp_serial_bus_descriptor)结构连接描述符。 **ConnectionSpeed**和**SLAVEADDRESS**成员包含 I2C 特定的连接设置。

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

Reshub 头文件定义**PNP\_串行\_总线\_描述符**结构。 Pshpack1 和 poppack 标头文件控制编译器使用的结构对齐模式。

I2C 串行总线连接描述符是一种打包的数据结构，其中相邻的字段与最接近的字节边界对齐，而不会出现间隔。 因此，此描述符中的16位整数值可能在奇数字节边界上启动。 在上面的代码示例中，包含 pshpack1 来告知编译器将相邻结构成员打包，而 poppack 会告诉编译器恢复默认的结构对齐方式。

**PNP\_I2C\_串行\_总线\_描述符**结构的**ConnectionSpeed**成员指定了在访问目标设备的过程中，时钟速率为赫兹的频率（以赫兹为单位）。 **SlaveAddress**成员是目标设备的总线地址。 对于某些 I2C 控制器驱动程序， **SlaveAddress**成员可能后跟可选的特定于供应商的数据，但此代码示例中的驱动程序不使用此数据，因此它不是结构定义的一部分。

在下面的代码示例中，上一示例中的 I2C 控制器驱动程序实现了一个 `GetTargetSettings` 例程，该例程调用[**SpbTargetGetConnectionParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters)来获取 I2C 总线上目标设备的连接设置。 此例程的*目标*输入参数是目标设备的句柄。 *Settings* output 参数是指向驱动程序分配的[**SPB\_连接\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/ns-spbcx-_spb_connection_parameters)结构的指针，该例程将一组连接参数写入到此结构中。 这些参数包括指向所请求的连接设置的指针。

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

在上面的代码示例中， [**SpbTargetGetConnectionParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters)将连接参数写入驱动程序分配的 `Params` 结构。 `Params` 的**ConnectionParameters**成员指向[**RH\_QUERY\_连接\_属性\_输出\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/reshub/ns-reshub-_rh_query_connection_properties_output_buffer)结构（在 reshub 中定义），其**ConnectionProperties**成员是串行总线连接描述符的第一个字节;此描述符的剩余字节会立即沿用**ConnectionProperties**成员。 `Params` 的**ConnectionParameters**成员指向的缓冲区足够大，可包含**RH\_QUERY\_连接\_属性\_输出\_缓冲**结构以及描述符字节遵循此结构。

前面的代码示例中的驱动程序实现 `GetTargetSettings` 例程对从**SpbTargetGetConnectionParameters**接收的连接参数执行以下参数检查：

-   验证 RH\_QUERY 中包含的串行总线连接描述符的大小[ **\_连接\_属性\_输出\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/reshub/ns-reshub-_rh_query_connection_properties_output_buffer)结构至少为**sizeof**（**PNP\_串行\_BUS\_描述符**）。
-   根据 ACPI 5.0 规范的要求，验证串行总线连接描述符的第一个字节是否设置为串行\_总线\_描述符（常数值0x8e）。
-   验证串行总线连接描述符中的串行总线类型是否设置为 I2C\_串行\_总线\_类型（常量值0x01），该类型将串行总线类型标识为 I2C。

前面的代码示例结束时，\*`Settings` 结构包含目标设备的连接设置（总线地址、地址宽度和总线时钟频率）。 I2C 控制器驱动程序使用这些连接设置来配置控制器以访问设备。

 

 




