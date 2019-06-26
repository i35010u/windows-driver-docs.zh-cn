---
title: 启动适配器
description: 启动适配器
ms.assetid: ff2c8914-2fc2-4182-b47e-685571508b33
keywords:
- 微型端口适配器 WDK 网络启动
- 适配器 WDK 网络启动
- 暂停的状态 WDK 网络
- 运行状态 WDK 网络
- MiniportRestart
- 起始微型端口适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05722fcc939cafc03e88a902446bbdf9e340cf0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377555"
---
# <a name="starting-an-adapter"></a>启动适配器





NDIS 调用微型端口驱动程序[ **MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)函数启动的重新启动请求的适配器处于已暂停状态。 该驱动程序可以继续，该值指示接收数据 NDIS 调用后立即*MiniportRestart*和之前的微型端口驱动程序完成的重新启动操作，同步或异步。

当它调用微型端口驱动程序[ **MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)函数，NDIS 将传递一个指向[ **NDIS\_重启\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_restart_attributes)结构中的微型端口驱动程序**RestartAttributes**的成员[ **NDIS\_微型端口\_重启\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_restart_parameters)结构。

若要以异步方式完成重新启动操作*MiniportRestart*返回 NDIS\_状态\_PENDING 和驱动程序必须调用[ **NdisMRestartComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismrestartcomplete)函数后，才完成操作。

微型端口驱动程序应该已准备好接受发送请求，则在完成重新启动操作。 NDIS 并不会启动任何其他插操作，例如停止、 初始化或暂停请求，直到重新启动操作已完成。

该驱动程序已准备好处理发送和接收操作后，适配器将处于运行状态。

 

 





