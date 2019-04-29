---
title: 修改资源要求列表
description: 修改资源要求列表
ms.assetid: 75391dd2-5ae1-4562-97a0-4de21a08b61c
keywords:
- 列出了硬件资源 WDK KMDF，修改资源要求
- 资源要求列表 WDK KMDF，修改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 065df4ec43703467b19c8ce6fd714d103c18e002
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390132"
---
# <a name="modifying-a-resource-requirements-list"></a>修改资源要求列表


PnP 管理器可确保，所有新连接的设备驱动程序后已加载，它将设备的硬件要求列表发送到设备的驱动程序堆栈。

当列表下堆栈传输时，框架将调用每个函数和筛选器驱动程序的[ *EvtDeviceFilterRemoveResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540872)回调函数，传递形式的硬件要求列表输入的参数。 此回调函数可以从已指定总线驱动程序，但该功能驱动程序确定，则不需要使设备能够运行的硬件要求列表中删除硬件资源。

例如，PCI 总线驱动程序可能符合 PCI 规范中，复制内存空间中的 I/O 空间资源。 如果你的设备可以运行而无需使用 I/O 空间资源，设备的功能驱动程序可以从硬件要求列表中删除 I/O 空间资源。

从要求列表中删除项目，驱动程序可以执行以下操作：

-   调用以下方法来修改资源要求列表中的逻辑配置：
    -   [**WdfIoResourceRequirementsListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff548545)，以获取多个逻辑配置。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548553)，以获取访问逻辑配置。
    -   [**WdfIoResourceRequirementsListRemove** ](https://msdn.microsoft.com/library/windows/hardware/ff548570)并[ **WdfIoResourceRequirementsListRemoveByIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548575)，以删除逻辑配置。
-   调用以下方法来修改逻辑配置中的资源描述符：
    -   [**WdfIoResourceListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff548506)，以获取资源说明符的数目。
    -   [**WdfIoResourceListGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff548510)，以获取对资源描述符访问权限。
    -   [**WdfIoResourceListRemove** ](https://msdn.microsoft.com/library/windows/hardware/ff548523)并[ **WdfIoResourceListRemoveByDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff548528)，若要删除的资源描述符。

当列表传输到驱动程序堆栈时，框架将调用每个函数和筛选器驱动程序的[ *EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870)回调函数，传递的硬件要求作为输入参数的列表。 此回调函数可以添加额外的硬件资源功能驱动程序所需的用于使设备可操作。

若要将项添加到硬件要求列表，驱动程序可以执行以下操作：

-   调用以下方法来修改资源要求列表中的逻辑配置：
    -   [**WdfIoResourceRequirementsListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff548545)，以获取多个逻辑配置。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548553)，以获取访问逻辑配置。
    -   [**WdfIoResourceListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548502)，以创建新的逻辑配置。
    -   [**WdfIoResourceRequirementsListAppendIoResList** ](https://msdn.microsoft.com/library/windows/hardware/ff548537)或[ **WdfIoResourceRequirementsListInsertIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548560)，以添加新的逻辑配置。
-   调用以下方法来修改逻辑配置中的资源描述符：
    -   [**WdfIoResourceListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff548506)，以获取资源说明符的数目。
    -   [**WdfIoResourceListGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff548510)，以获取对资源描述符访问权限。
    -   [**WdfIoResourceListAppendDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff548498)或[ **WdfIoResourceListInsertDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff548513)，以添加资源描述符。

 

 





