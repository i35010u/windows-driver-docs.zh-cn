---
title: 卸载微型端口驱动程序
description: 卸载微型端口驱动程序
keywords:
- 微型端口驱动程序 WDK 网络，卸载
- NDIS 微型端口驱动程序 WDK，卸载
- 卸载微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4a4d36fa9d39e660593f5924a6600609abd99c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839421"
---
# <a name="unloading-a-miniport-driver"></a>卸载微型端口驱动程序





与 NDIS 微型端口驱动程序关联的驱动程序对象指定一个 [**卸载**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程。 删除驱动程序服务的所有设备时，系统会调用 *Unload* 例程。 NDIS 为微型端口驱动程序提供 *卸载* 例程。 NDIS 从 *Unload* 例程调用微型端口驱动程序的 [*MiniportDriverUnload*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)函数。

微型端口驱动程序必须从 *MiniportDriverUnload* 调用 [**NdisMDeregisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) 。

微型端口驱动程序的 *MiniportDriverUnload* 函数还应释放任何特定于驱动程序的资源。 系统将在 *MiniportDriverUnload* 返回后完成驱动程序卸载操作。

*MiniportDriverUnload* 函数的功能特定于驱动程序。 作为一般规则， *MiniportDriverUnload* 应撤消驱动程序初始化过程中执行的操作。 有关驱动程序初始化的详细信息，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

 

