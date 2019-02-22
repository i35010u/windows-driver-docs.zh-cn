---
title: 启动配置为创建的资源列表
description: 启动配置为创建的资源列表
ms.assetid: 8b78cbac-b547-45a1-a49c-f5543bf5ffed
keywords:
- 硬件资源 WDK KMDF 启动配置资源列表
- 启动配置资源列出了 WDK KMDF
- 启动配置资源列出了 WDK KMDF，创建
- 资源列出了 WDK KMDF
- 资源列出了 WDK KMDF，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08a519d3b3c0cfffc8b84694ab1e43228a4440e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533993"
---
# <a name="creating-a-resource-list-for-a-boot-configuration"></a>启动配置为创建的资源列表


总线驱动程序枚举设备后，框架将调用的驱动程序[ *EvtDeviceResourcesQuery* ](https://msdn.microsoft.com/library/windows/hardware/ff540895)回调函数。 此回调函数接收资源列表中对象，它表示空资源列表的句柄。 然后，该驱动程序必须执行以下操作将信息添加到列表中，每种类型的设备的启动配置要求的硬件资源：

1.  在驱动程序提供填充[ **CM\_分部\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)结构，它指定特定资源的有效值。

2.  调用[ **WdfCmResourceListAppendDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff545683)或[ **WdfCmResourceListInsertDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff545698)若要添加的 CM内容\_分部\_资源\_描述符结构到资源的列表。

驱动程序的后*EvtDeviceResourcesQuery*回调函数返回，框架将传递资源列表到 PnP 管理器。

设备安装程序可以指定其他资源的列表。 有关更多资源列表的详细信息，请参阅[硬件资源](https://msdn.microsoft.com/library/windows/hardware/ff547012)。

 

 





