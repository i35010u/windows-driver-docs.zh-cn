---
title: 将中间驱动程序注册为协议
description: 将中间驱动程序注册为协议
ms.assetid: 79707f6b-0e31-46a8-a763-fa2669ce9635
keywords:
- 注册中间驱动程序
- 驱动程序 WDK 的中间连接网络、 注册
- NDIS 中间层驱动程序 WDK，注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bc62c5a54a00b0f7642379bbc502776b05dd5b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374787"
---
# <a name="registering-an-intermediate-driver-as-a-protocol"></a>将中间驱动程序注册为协议





中间的驱动程序注册其*ProtocolXxx*的上下文中使用 NDIS 函数及其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数通过调用[ **NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)。

注册中间驱动程序为一种协议与注册为协议驱动程序几乎完全相同。 有关详细信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。

使用面向连接的下边缘中间驱动程序必须将注册为面向连接的客户端。 面向连接的客户端使用的呼叫管理器或集成的微型端口呼叫管理器 (MCM) 的调用设置和关闭的服务。 面向连接的客户端还使用发送和接收的面向连接的微型端口驱动程序或 MCM 发送和接收数据的功能。 有关详细信息，请参阅[Connection-Oriented 的客户端执行的操作](connection-oriented-operations-performed-by-clients.md)。

中间的驱动程序可能需要其他*ProtocolXxx*都特定于实现的函数。 有关注册可选信息*ProtocolXxx*函数，请参阅[配置可选协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

 

 





