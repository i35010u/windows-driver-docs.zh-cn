---
title: 通过中间驱动程序传输网络数据
description: 通过中间驱动程序传输网络数据
ms.assetid: 90759322-810b-47fd-896c-465c96be4cdd
keywords:
- 中级驱动程序 WDK 网络，传输数据
- NDIS 中间驱动程序 WDK，传输数据
- 传输网络数据
- 数据传输 WDK NDIS 中间
- 传输数据 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3f5fe24a256ed82473cd2cb40f71f7e3fe88d25
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841775"
---
# <a name="transmitting-network-data-through-an-intermediate-driver"></a>通过中间驱动程序传输网络数据





如将[中间驱动程序注册为微型端口驱动程序](registering-an-intermediate-driver-as-a-miniport-driver.md)中所述，中间驱动程序在向[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)注册时必须提供[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数。 如果驱动程序具有无连接的下边缘，则*MiniportSendNetBufferLists*函数可以通过调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)来转发传入的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 *MiniportSendNetBufferLists*可以通过**NdisSendNetBufferLists**发送网络\_\_缓冲区的列表，而不考虑基础微型端口驱动程序的功能。

*MiniportSendNetBufferLists*接收按**NdisSendNetBufferLists**的过量调用方确定的顺序排列的网络\_缓冲区\_列表结构的列表。 在大多数情况下，中间驱动程序应保持此顺序，因为它将传入的 NET\_缓冲区\_列表结构的传入数组传递到基础微型端口驱动程序。 一个中间驱动程序，用于修改网络数据中的数据，然后将这些数据传递到基础驱动程序，以便对列表重新排序。

NDIS 始终将[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构指针的排序保存为作为链接列表传递到**NdisSendNetBufferLists**。 基础微型端口驱动程序还假设传递到其*MiniportSendNetBufferLists*函数的列表表示网络数据应按相同顺序进行传输。

 

 





