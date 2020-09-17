---
title: 访问设备实例 SPDRP_Xxx 属性
description: 访问设备实例 SPDRP_Xxx 属性
ms.assetid: 15ee51f8-1904-43ee-8bc2-311688c860e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c546500071414c38716211abfb72404e6b2d024
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715786"
---
# <a name="accessing-device-instance-spdrp_xxx-properties"></a>访问设备实例 SPDRP_Xxx 属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 支持与 *setupapi.log*中定义的 SPDRP_Xxx 标识符对应的设备实例属性。 这些属性描述设备实例的配置。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。 Windows Server 2003、Windows XP 和 Windows 2000 还支持这些设备驱动程序属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，这些早期版本的 Windows 版本使用 SPDRP_*Xxx* 标识符来表示和访问设备实例属性。

为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持使用 SPDRP_Xxx 标识符来访问设备实例属性。 但是，在 Windows Vista 和更高版本的 Windows 上，应使用相应的属性键来访问这些属性。

有关具有相应 SPDRP_Xxx 标识符的系统定义的设备实例属性的列表，请参阅 [具有相应 SPDRP_Xxx 标识符的设备属性](/previous-versions/ff541469(v=vs.85))。 设备实例属性由用于访问 Windows Vista 和更高版本 Windows 中的属性的属性键列出。 随每个属性键一起提供的信息包括相应 SPDRP_*Xxx* 标识符，可用于在 windows Server 2003、windows XP 和 windows 2000 上访问该属性。

有关如何使用属性键访问 Windows Vista 和更高版本的 Windows 中的设备实例属性的信息，请参阅 [ (Windows vista 和更高版本) 访问设备实例属性 ](accessing-device-instance-properties--windows-vista-and-later-.md)。

### <a name="accessing-a-device-property"></a>访问设备属性

若要访问与 Windows Server 2003、Windows XP 和 Windows 2000 上的 SPDRP_*Xxx* 标识符对应的设备实例属性，请使用以下 setupapi.log 函数：

-   [**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)

    此函数检索由 SPDRP_*Xxx* 标识符指定的设备属性。

-   [**SetupDiSetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)

    此函数设置由 SPDRP_*Xxx* 标识符指定的设备属性。

### <a name="retrieving-a-device-property"></a>检索设备属性

若要在 Windows Server 2003、Windows XP 和 Microsoft Windows 2000 上检索设备属性，请执行以下步骤：

1.  调用 **SetupDiGetDeviceRegistryProperty** 可检索属性值的大小（以字节为单位）。 提供以下参数值：

    -   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其检索请求的属性值的设备实例。
    -   将 *DeviceInfoData* 设置为指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构表示要为其检索请求的属性值的设备实例。
    -   将 *属性* 设置为 SPDRP_*Xxx* 标识符。 有关这些标识符的列表和相应的设备属性的说明，请参阅[**SetupDiSetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)附带的*属性*参数说明。
    -   将 *PropertyRegDataType* 设置为指向 DWORD 类型化变量的指针。
    -   将 *PropertyBuffer* 设置为 **NULL**。
    -   将 *PropertyBufferSize* 设置为零。
    -   将 *RequiredSize* 设置为一个指针，该指针指向接收的 DWORD 类型化变量，该变量表示属性值的大小（以字节为单位）。

    在响应对[**SetupDiSetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)的调用时， **SetupDiGetDeviceRegistryProperty**将 \* *RequiredSize*设置为检索属性值所需的缓冲区大小（以字节为单位），记录错误代码 ERROR_INSUFFICIENT_BUFFER 并返回**FALSE**。 对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetDeviceRegistryProperty** ，并提供在第一次调用中提供的相同参数值，但以下更改除外：

    -   将 *PropertyBuffer* 设置为指向字节类型缓冲区的指针，该缓冲区接收请求的属性值。
    -   将 *PropertyBufferSize* 设置为 *PropertyBuffer* 缓冲区的大小（以字节为单位）。 第一次调用**SetupDiGetDeviceRegistryProperty**时，检索到 RequiredSize 中的 PropertyBuffer 缓冲区的所需大小 \* *RequiredSize*。

    如果对**SetupDiGetDeviceRegistryProperty**的第二次调用成功，则**SetupDiGetDeviceRegistryProperty**将 \* *PropertyRegDataType*设置为属性值的注册表数据类型，将*PropertyBuffer*缓冲区设置为属性值，将 \* *RequiredSize*设置为检索到的属性值的大小（以字节为单位），并返回**TRUE**。 如果函数调用失败， **SetupDiGetDeviceRegistryProperty** 将返回 **FALSE** ，并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回记录的错误代码。

### <a name="setting-a-device-property"></a>设置设备属性

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上设置设备属性，请调用 [**SetupDiSetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya) 并提供以下参数值：

-   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其设置属性值的设备实例。

-   将 *DeviceInfoData* 设置为指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构表示要为其设置属性值的设备实例。

-   将 *属性* 设置为 SPDRP_*Xxx* 标识符。

-   将 *PropertyBuffer* 设置为指向包含属性值的字节类型缓冲区的指针。

-   将 *PropertyBufferSize* 设置为 *PropertyBuffer* 缓冲区中提供的属性值的大小（以字节为单位）。

如果对 **SetupDiSetDeviceRegistryProperty** 的此调用成功，则 **SetupDiSetDeviceRegistryProperty** 将设置设备实例属性并返回 **TRUE**。 如果函数调用失败， **SetupDiSetDeviceRegistryProperty** 将返回 **FALSE** ，并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回记录的错误代码。

 

