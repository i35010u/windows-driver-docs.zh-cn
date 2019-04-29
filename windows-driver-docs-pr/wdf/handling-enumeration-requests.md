---
title: 处理枚举请求
description: 处理枚举请求
ms.assetid: 3719ffa7-2daf-4716-a183-531837be99aa
keywords:
- 枚举 WDK KMDF
- 即插即用 WDK KMDF，总线枚举
- 插 WDK KMDF，总线枚举
- 总线枚举 WDK KMDF
- 列出子设备 WDK KMDF
- 子设备 WDK KMDF
- 动态枚举 WDK KMDF
- 静态枚举 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7acccaf5603ad4dbcc22a3f2d4aaaa530b05fb9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391885"
---
# <a name="handling-enumeration-requests"></a>处理枚举请求


PnP 管理器可以请求总线驱动程序即可在任何时候枚举及其子级。 (如果已熟悉 WDM 接口，将枚举项请求[ **IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)具有关系的请求类型**BusRelations**。)基于框架的驱动程序不会看到这些请求。 相反，该框架处理的请求通过使用存储在设备的子列表中的信息。 该驱动程序负责使子列表保持最新以便 PnP 管理器请求枚举时，框架可以提供正确的信息。

支持动态枚举的基于框架的总线驱动程序可以接收 reenumerate 特定子设备的请求。 之后，驱动程序检测到设备故障，可能会由子设备功能驱动程序发送此类请求。 (该框架通过实现支持这种类型的请求[ **REENUMERATE\_自助\_接口\_标准**](https://msdn.microsoft.com/library/windows/hardware/ff560839)接口，这是一种标准[驱动程序定义的接口](using-driver-defined-interfaces.md)中定义*wdm.h 中*。)

支持动态枚举的基于框架的总线驱动程序可以提供[ *EvtChildListDeviceReenumerated* ](https://msdn.microsoft.com/library/windows/hardware/ff540830)回调函数，该框架将调用时收到重新枚举函数从子设备的驱动程序请求。 如果此回调函数返回 **，则返回 TRUE**或不存在，框架将标记为不再存在子设备，并通知即插即用 manager 总线驱动程序的子列表已更改。 结果，即插即用管理器将请求重新枚举，框架将调用的驱动程序[ *EvtChildListCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540828)回调函数，创建一个新的 PDO 子设备。

 

 





