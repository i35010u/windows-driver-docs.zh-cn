---
title: PnP 管理器重新分发系统资源
description: PnP 管理器重新分发系统资源
ms.assetid: c8e6277b-b1e5-449f-b5a0-f5a46b46e56e
keywords:
- 电源管理方案 WDK UMDF，即插即用管理器将重新分发的系统资源
- 重新分发的系统资源方案，WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f61e2dc439300eb9186831a39fb0692a70988fc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350639"
---
# <a name="the-pnp-manager-redistributes-system-resources"></a>PnP 管理器重新分发系统资源


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果用户将设备添加到系统，以及设备需要即插即用的管理员已分配给另一台设备的系统资源，即插即用管理器将尝试重新分配资源。

在此过程中，即插即用管理器停止设备并获取它们超出其工作 (D0) 状态。 它然后提供了新的资源列表到设备，以便它们可以重新启动，请使用新的资源。

在重新分发的资源，即插即用管理器不会更改设备的资源分配如果其中一个设备的基于 UMDF 驱动程序提供[ **IPnpCallback::OnQueryStop** ](https://msdn.microsoft.com/library/windows/hardware/ff556811)回调函数和回调函数已禁止重新分配。

<a href="" id="power-down-sequence"></a>**电源关闭序列**  
对于每个基于 UMDF 的函数和筛选器驱动程序支持设备正在停止，框架将执行以下操作，在序列中，一个驱动程序时，开始驱动程序堆栈中最高的驱动程序：

1.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoSuspend** ](https://msdn.microsoft.com/library/windows/hardware/ff556790)回调函数。

2.  该框架将停止所有设备的电源管理的 I/O 队列。

3.  框架将调用的驱动程序[ **IPnpCallback::OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803)回调函数 （如果存在）。

4.  框架将调用的驱动程序[ **IPnpCallbackHardware::OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556768)传递的即插即用的管理员分配给设备的硬件资源的列表的回调函数 （如果存在）。

若要查看图显示了这些步骤，请参阅图有序地删除[用户断开设备](a-user-unplugs-a-device.md)。

<a href="" id="power-up-sequence-------"></a>**强化序列**   
对于每个基于 UMDF 的函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，使用驱动程序的最低驱动程序堆栈中启动一个时，驱动程序：

1.  框架将调用的驱动程序[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)回调函数 （如果存在），同时传入的即插即用的管理员分配给设备的硬件资源的列表。

2.  框架将调用的驱动程序[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)回调函数 （如果存在）。

3.  该框架将重新启动的所有设备的电源管理的 I/O 队列。

4.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff556785)回调函数。

若要查看图显示了这些步骤，请参阅[设备中的用户插入](a-user-plugs-in-a-device.md)。

 

 





