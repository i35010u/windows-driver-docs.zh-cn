---
title: 创建资源要求列表
description: 创建资源要求列表
ms.assetid: 1254aa21-c64b-4c62-93dc-6758cef382f9
keywords:
- 硬件资源 WDK KMDF，创建资源的要求列表
- 资源要求列表 WDK KMDF
- 资源要求列表 WDK KMDF，创建
- 资源要求列表对象 WDK KMDF
- framework 资源要求列表对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cc4c23ae0b003a09823d64b5d342afadc29f8e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358489"
---
# <a name="creating-a-resource-requirements-list"></a>创建资源要求列表


当总线驱动程序检测到的子设备时，该驱动程序负责创建设备的资源要求列表。 在列表中的每个项是[逻辑配置](https://msdn.microsoft.com/library/windows/hardware/ff547012#ddk-logical-configurations-kg)设备。

该驱动程序在总线枚举过程中报告设备后，框架将调用的驱动程序[ *EvtDeviceResourceRequirementsQuery* ](https://msdn.microsoft.com/library/windows/hardware/ff540894)回调函数。 此回调函数接收表示空的资源要求列表的资源要求列表对象的句柄。

然后，驱动程序必须执行以下操作来将信息添加到资源的要求列表：

-   创建空的逻辑配置。

    对于每个驱动程序将指定的逻辑配置，该驱动程序必须调用[ **WdfIoResourceListCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548502)创建空的逻辑配置。

-   将资源描述符添加到逻辑配置。

    若要将资源描述符添加到逻辑配置，该驱动程序必须执行以下操作，每种类型的设备需要的硬件资源：

    1.  填写驱动程序分配[ **IO\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff550598)结构，它指定的特定资源的有效值的范围。
    2.  调用[ **WdfIoResourceListAppendDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff548498)或[ **WdfIoResourceListInsertDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff548513)若要添加的 IO内容\_资源\_描述符结构到逻辑配置。

    如果设备使用多个资源类型的实例，必须了解在其中添加资源的顺序的所有驱动程序堆栈中访问资源。 例如，如果设备需要两个范围的 I/O 端口地址，请访问资源描述符的所有驱动程序必须了解的两个范围添加到逻辑配置中的顺序。

-   将逻辑配置添加到资源要求列表。

    若要将逻辑配置添加到设备的资源要求列表，驱动程序调用[ **WdfIoResourceRequirementsListAppendIoResList** ](https://msdn.microsoft.com/library/windows/hardware/ff548537)或[ **WdfIoResourceRequirementsListInsertIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548560)。

    如果将资源分配到设备，即插即用管理器将尝试匹配列表中的第一个逻辑配置的要求。 如果该配置所需的资源不可用，即插即用管理器与匹配资源都可用列表中的下一个配置。

    如果您的驱动程序支持非 PnP 设备，您的驱动程序通常还必须调用[ **WdfIoResourceRequirementsListSetSlotNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff548579)并[ **WdfIoResourceRequirementsListSetInterfaceType**](https://msdn.microsoft.com/library/windows/hardware/ff548577)。

驱动程序的后[ *EvtDeviceResourceRequirementsQuery* ](https://msdn.microsoft.com/library/windows/hardware/ff540894)回调函数返回，该框架将传递资源要求列表到 PnP 管理器。

 

 





