---
title: 卸载微型端口驱动程序
description: 卸载微型端口驱动程序
ms.assetid: c5199a0f-31c3-42e4-8758-cbe480dff682
keywords:
- 微型端口驱动程序 WDK 连接网络、 卸载
- NDIS 微型端口驱动程序 WDK，卸载
- 正在卸载的微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf5d0bccf3bc2a06c749da8fd66852dddbc3841
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382094"
---
# <a name="unloading-a-miniport-driver"></a>卸载微型端口驱动程序





与的 NDIS 微型端口驱动程序相关联的驱动程序对象指定[ **Unload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程。 系统调用*Unload*例程时，已删除的驱动程序服务的所有设备。 提供了 NDIS *Unload*例程的微型端口驱动程序。 NDIS 调用微型端口驱动程序[ *MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)函数从*卸载*例程。

微型端口驱动程序必须调用[ **NdisMDeregisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterminiportdriver)从*MiniportDriverUnload*。

微型端口驱动程序*MiniportDriverUnload*函数还应释放任何特定于驱动程序的资源。 系统将会完成驱动程序卸载操作后的*MiniportDriverUnload*返回。

功能*MiniportDriverUnload*函数是特定于驱动程序。 作为一般规则*MiniportDriverUnload*应撤消在驱动程序初始化期间执行的操作。 有关驱动程序初始化的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

 

 





