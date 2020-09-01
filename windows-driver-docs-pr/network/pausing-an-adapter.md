---
title: 暂停适配器
description: 暂停适配器
ms.assetid: e24a9886-a1d7-4ca5-bed8-85db4a49ed9c
keywords:
- 微型端口适配器 WDK 网络，暂停
- 适配器 WDK 网络，暂停
- 暂停状态 WDK 网络
- 暂停状态 WDK 网络
- MiniportPause
- 暂停微型端口适配器
- 正在停止微型端口适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6b2cc4fb7dfaca2be5abf4e700d083c91bed939
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212807"
---
# <a name="pausing-an-adapter"></a>暂停适配器





NDIS 调用微型端口驱动程序的 [*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause) 函数来启动暂停操作。 直到暂停操作完成后，适配器才会保持暂停状态。

在暂停状态下，微型端口驱动程序必须完成未完成的接收操作。 驱动程序还必须完成所有未完成的发送操作，并且应拒绝任何新的发送请求。

若要完成接收操作，驱动程序将等待对 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 函数的所有调用返回，NDIS 必须将所有未完成的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构返回给微型端口驱动程序的 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists) 函数。

若要完成未完成的发送操作，微型端口驱动[**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)程序应为所有未完成的网络 \_ 缓冲区 \_ 列表结构调用 NdisMSendNetBufferListsComplete 函数。 驱动程序应拒绝对其 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 函数立即发出的所有新发送请求。

当微型端口驱动程序完成所有未完成的发送和接收操作之后，驱动程序必须以同步或异步方式完成暂停请求。 如果暂停操作异步完成，则驱动程序将调用 [**NdisMPauseComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismpausecomplete) 来完成暂停请求。 完成暂停请求后，微型端口驱动程序处于暂停状态。

当微型端口驱动程序处于暂停状态时，NDIS 不会启动其他即插即用操作，如暂停、初始化、电源更改或重启操作。 在微型端口驱动程序处于暂停状态之后，NDIS 可以启动这些即插即用操作。

 

