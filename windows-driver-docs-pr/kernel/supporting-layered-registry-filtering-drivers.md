---
title: 支持分层注册表筛选驱动程序
description: 支持分层注册表筛选驱动程序
ms.assetid: 5adeecdb-c26e-4502-87b4-bfb02a4aaba8
keywords:
- 筛选注册表调用 WDK 内核，分层
- 筛选驱动程序 WDK 内核，分层的注册表
- 分层注册表筛选驱动程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd9c451a34d73a2225a2a40a5711bfa31a82a377
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385109"
---
# <a name="supporting-layered-registry-filtering-drivers"></a>支持分层注册表筛选驱动程序


Windows Vista 和更高版本的操作系统版本支持筛选驱动程序的注册表的分层的的堆栈。 堆栈中的每个驱动程序可参与通过注册筛选注册表操作[ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)例程。 筛选驱动程序的每个注册表分配*海拔高度*，并且驱动程序可以注册一个*RegistryCallback*例程的每个海拔高度。 当您的驱动程序调用[ **CmRegisterCallbackEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallbackex)，驱动程序指定其海拔高度。 有关海拔的地区的详细信息，请参阅[加载顺序组和海拔微筛选器驱动程序的地区](https://docs.microsoft.com/windows-hardware/drivers/ifs/load-order-groups-and-altitudes-for-minifilter-drivers)。

当某个线程进行调用的注册表时，配置管理器中调用每个*RegistryCallback*例程，按从最高到最低，海拔高度的顺序被调用的所有驱动程序之前或*RegistryCallback*例程将为其返回状态值[NT\_成功](using-ntstatus-values.md)(*状态*) 等于**FALSE**。 因此，如果更高级别的驱动程序阻止，或修改注册表操作的较低级驱动程序不会调用。 （如果驱动程序通过调用不同的注册表函数修改操作，配置管理器不重新启动筛选器堆栈的顶部。）

它们调用的顺序中的 Windows Vista 筛选器堆栈的顶部附近，插入注册表筛选驱动程序在 Windows Vista 之前编写，因此不具有海拔高度赋值[ **CmRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallback).

 

 




