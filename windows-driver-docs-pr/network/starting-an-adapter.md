---
title: 启动适配器
description: 启动适配器
keywords:
- 微型端口适配器 WDK 网络，开始
- 适配器 WDK 网络，开始
- 暂停状态 WDK 网络
- 运行状态 WDK 网络
- MiniportRestart
- 启动微型端口适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 881a3a8ccb3be330537f1752be771cc60583af91
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801265"
---
# <a name="starting-an-adapter"></a>启动适配器





NDIS 调用微型端口驱动程序的 [**MiniportRestart**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart) 函数来启动处于暂停状态的适配器的重新启动请求。 此驱动程序可以在 NDIS 调用 *MiniportRestart* 之后和在微型端口驱动程序完成重新启动操作之前（同步或异步）恢复指示已接收数据。

当它调用微型端口驱动程序的 [**MiniportRestart**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)函数时，ndis 会将指向 [**ndis \_ 重新启动 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)结构的指针传递到 [**Ndis \_ 微型端口 \_ restart \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_restart_parameters)结构的 **RestartAttributes** 成员中的微型端口驱动程序。

若要以异步方式完成重启操作， *MiniportRestart* 将返回 NDIS \_ 状态 \_ "挂起"，并且驱动程序必须在操作完成后调用 [**NdisMRestartComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismrestartcomplete) 函数。

小型端口驱动程序应准备好在完成重启操作后接受发送请求。 在重新启动操作完成之前，NDIS 不会启动任何其他即插即用操作，如暂停、初始化或暂停请求。

驱动程序准备好处理发送和接收操作后，适配器处于 "正在运行" 状态。

 

