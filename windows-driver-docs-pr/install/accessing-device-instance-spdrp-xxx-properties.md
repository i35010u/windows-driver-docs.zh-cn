---
title: 访问设备实例 SPDRP_Xxx 属性
description: 访问设备实例 SPDRP_Xxx 属性
ms.assetid: 15ee51f8-1904-43ee-8bc2-311688c860e0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f502ed9ae1bd56d222bd9a36cbe33826598203f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373897"
---
# <a name="accessing-device-instance-spdrpxxx-properties"></a>访问设备实例 SPDRP_Xxx 属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持的设备实例属性中定义的 SPDRP_Xxx 标识符对应*Setupapi.h*. 这些属性描述设备实例的配置的特征。 统一的设备属性模型使用[属性键](property-keys.md)来表示这些属性。 Windows Server 2003、 Windows XP 和 Windows 2000 还支持这些设备驱动程序属性。 但是，这些早期版本的 Windows 不支持统一的设备属性模型属性键。 相反，这些早期的 Windows 版本使用 SPDRP_*Xxx*实例属性的标识符，以表示和访问设备。

为了保持与这些早期版本的 Windows、 Windows Vista 和更高版本的兼容性还支持使用 SPDRP_Xxx 标识符访问设备实例属性。 但是，应使用相应的属性键来访问在 Windows Vista 和更高版本的 Windows 上的这些属性。

具有相应 SPDRP_Xxx 标识符的系统定义的设备实例属性的列表，请参阅[设备属性，具有相应 SPDRP_Xxx 标识符](https://msdn.microsoft.com/library/windows/hardware/ff541469)。 用于访问在 Windows Vista 和更高版本的 Windows 中的属性的属性键列出设备实例属性。 所提供的密钥与每个属性包括相应 SPDRP_ 的信息*Xxx*可用于访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的属性的标识符。

有关如何使用属性键来访问在 Windows Vista 和更高版本的 Windows 设备实例属性的信息，请参阅[访问设备实例属性 （Windows Vista 和更高版本）](accessing-device-instance-properties--windows-vista-and-later-.md)。

### <a name="accessing-a-device-property"></a>访问设备属性

为访问设备实例属性对应于 SPDRP_*Xxx*标识符在 Windows Server 2003、 Windows XP 和 Windows 2000 中，使用以下安装程序 Api 函数：

-   [**SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)

    此函数可检索的设备属性指定的 SPDRP_*Xxx*标识符。

-   [**SetupDiSetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552169)

    此函数设置的设备属性指定的 SPDRP_*Xxx*标识符。

### <a name="retrieving-a-device-property"></a>检索设备属性

若要检索 Windows Server 2003、 Windows XP 和 Microsoft Windows 2000 上的设备属性，请按照下列步骤：

1.  调用**SetupDiGetDeviceRegistryProperty**检索大小 （字节） 的属性值。 提供以下参数值：

    -   设置*DeviceInfoSet*到设备的信息集，其中包含要为其检索请求的属性值的设备实例的句柄。
    -   设置*DeviceInfoData*指向的[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)结构，它表示要为其检索请求的属性值的设备实例。
    -   设置*属性*到 SPDRP_*Xxx*标识符。 有关这些标识符和相应的设备属性的说明的列表，请参阅的说明*属性*附带的参数[ **SetupDiSetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552169).
    -   设置*PropertyRegDataType*到指向 DWORD 类型的变量的指针。
    -   设置*PropertyBuffer*到**NULL**。
    -   设置*PropertyBufferSize*为零。
    -   设置*RequiredSize*为指向一个 DWORD 类型的变量来接收，大小，以字节为单位的属性值。

    以响应对的调用[ **SetupDiSetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552169)， **SetupDiGetDeviceRegistryProperty**设置\* *RequiredSize*大小，以字节为单位，检索属性值，所需的缓冲区的记录的错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  调用**SetupDiGetDeviceRegistryProperty**试并提供在第一个调用中，除以下更改外提供了相同的参数值：

    -   设置*PropertyBuffer*到指向接收请求的属性值的字节类型的缓冲区的指针。
    -   设置*PropertyBufferSize*到的大小，以字节为单位的*PropertyBuffer*缓冲区。 首次调用**SetupDiGetDeviceRegistryProperty**检索 PropertyBuffer 缓冲区中的所需的大小\* *RequiredSize*。

    如果第二个调用**SetupDiGetDeviceRegistryProperty**成功， **SetupDiGetDeviceRegistryProperty**设置\* *PropertyRegDataType*到注册表数据类型的属性值，设置*PropertyBuffer*属性值设置到缓冲区\* *RequiredSize*的大小，以字节为单位，属性值的表格是检索，并返回 **，则返回 TRUE**。 如果函数调用失败， **SetupDiGetDeviceRegistryProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

### <a name="setting-a-device-property"></a>设置设备属性

若要在 Windows Server 2003、 Windows XP 和 Windows 2000 上设置的设备属性，调用[ **SetupDiSetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552169)并提供以下参数值：

-   设置*DeviceInfoSet*到设备的信息集，其中包含要为其设置属性值的设备实例的句柄。

-   设置*DeviceInfoData*指向的[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)结构，它表示要为其设置属性值的设备实例。

-   设置*属性*到 SPDRP_*Xxx*标识符。

-   设置*PropertyBuffer*到指向包含的属性值的字节类型的缓冲区的指针。

-   设置*PropertyBufferSize*大小，以字节为单位，属性值的中提供的*PropertyBuffer*缓冲区。

如果此调用**SetupDiSetDeviceRegistryProperty**成功， **SetupDiSetDeviceRegistryProperty**设置的设备实例属性，并返回**TRUE**。 如果函数调用失败， **SetupDiSetDeviceRegistryProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

 

 





