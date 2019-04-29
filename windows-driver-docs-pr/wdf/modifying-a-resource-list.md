---
title: 修改资源列表
description: 修改资源列表
ms.assetid: 571b2990-5627-434e-b8fc-d2564188f544
keywords:
- 启动配置资源列出了 WDK KMDF，修改
- 硬件资源 WDK KMDF，列出了资源
- 资源列出了 WDK KMDF，修改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36fd23b5121d5fb895ca3092dd4f79b7c4a19722
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390164"
---
# <a name="modifying-a-resource-list"></a>修改资源列表


如果驱动程序提供了[ *EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870)回调函数，它还必须提供[ *EvtDeviceRemoveAddedResources*](https://msdn.microsoft.com/library/windows/hardware/ff540892)回调函数。 *EvtDeviceRemoveAddedResources*回调函数中删除资源的*EvtDeviceFilterAddResourceRequirements*添加，以便总线驱动程序不会尝试使用的回调函数它们。

若要修改设备的资源列表中的资源描述符，驱动程序应调用以下方法：

-   [**WdfCmResourceListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff545687)，以获取资源说明符的数目。

-   [**WdfCmResourceListGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff545688)，以获取对资源描述符访问权限。

-   [**WdfCmResourceListRemove** ](https://msdn.microsoft.com/library/windows/hardware/ff545704)并[ **WdfCmResourceListRemoveByDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff545717)，若要删除的资源描述符。

如果该驱动程序中删除资源，它必须将其删除从这两个[原始和已翻译的资源列表](raw-and-translated-resources.md)。

 

 





