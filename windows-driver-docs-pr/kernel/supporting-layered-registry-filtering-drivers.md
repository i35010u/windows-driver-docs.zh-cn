---
title: 支持分层注册表筛选驱动程序
description: 支持分层注册表筛选驱动程序
keywords:
- 筛选注册表调用 WDK 内核，分层
- 注册表筛选驱动程序 WDK 内核，分层
- 分层注册表筛选驱动程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93292cbb74306df1b4fad591424701205c749ecc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817161"
---
# <a name="supporting-layered-registry-filtering-drivers"></a>支持分层注册表筛选驱动程序


Windows Vista 和更高版本的操作系统版本支持分层的注册表筛选驱动程序堆栈。 堆栈中的每个驱动程序都可以通过注册 [*RegistryCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function) 例程参与筛选注册表操作。 为每个注册表筛选驱动程序分配一个 *海拔高度*，驱动程序只能为每个海拔注册一个 *RegistryCallback* 例程。 当驱动程序调用 [**CmRegisterCallbackEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)时，驱动程序将指定其高度。 有关高度的详细信息，请参阅 [微筛选器驱动程序的加载顺序组和高度](../ifs/load-order-groups-and-altitudes-for-minifilter-drivers.md)。

当某个线程进行注册表调用时，configuration manager 会按顺序从最高级别按顺序调用每个 *RegistryCallback* 例程，直到调用了所有驱动程序，或 *RegistryCallback* 例程返回 (*状态* 值为 " [NT \_ SUCCESS](using-ntstatus-values.md) " 的状态值) 等于 **FALSE**。 因此，如果较高级别的驱动程序阻止或修改注册表操作，则不会调用较低级别的驱动程序。  (如果驱动程序通过调用不同的注册表函数修改操作，则不会在筛选器堆栈顶部重新启动配置管理器。 ) 

在 windows Vista 之前编写的注册表筛选驱动程序在 Windows Vista 筛选器堆栈顶部附近插入（按照它们调用 [**CmRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)的顺序）。

 

