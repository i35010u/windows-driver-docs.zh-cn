---
title: 通过中间驱动程序传输网络数据
description: 通过中间驱动程序传输网络数据
keywords:
- 中级驱动程序 WDK 网络，传输数据
- NDIS 中间驱动程序 WDK，传输数据
- 传输网络数据
- 数据传输 WDK NDIS 中间
- 传输数据 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15c2a217443f8899705d8fc73f34c1069245836c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815855"
---
# <a name="transmitting-network-data-through-an-intermediate-driver"></a>通过中间驱动程序传输网络数据





如将 [中间驱动程序注册为微型端口驱动程序](registering-an-intermediate-driver-as-a-miniport-driver.md)中所述，中间驱动程序在向 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)注册时必须提供 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数。 如果驱动程序具有无连接的下边缘，则 *MiniportSendNetBufferLists* 函数可以通过调用 [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)转发传入的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 *MiniportSendNetBufferLists* 可以 \_ 通过 NdisSendNetBufferLists 发送它接收的网络缓冲区列表结构的列表， \_ 而不考虑基础微型端口驱动程序的功能。 **NdisSendNetBufferLists**

*MiniportSendNetBufferLists* 接收按 \_ \_ **NdisSendNetBufferLists** 的过量调用方确定的顺序排列的网络缓冲区列表结构的列表。 在大多数情况下，中间驱动程序应保持此顺序，因为它会将传入的网络 \_ 缓冲区 \_ 列表结构数组传递到基础微型端口驱动程序。 一个中间驱动程序，用于修改网络数据中的数据，然后将这些数据传递到基础驱动程序，以便对列表重新排序。

NDIS 始终保留将 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构指针作为链接列表传递到 **NdisSendNetBufferLists** 的顺序。 基础微型端口驱动程序还假设传递到其 *MiniportSendNetBufferLists* 函数的列表表示网络数据应按相同顺序进行传输。

 

