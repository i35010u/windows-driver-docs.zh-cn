---
title: 取消发送操作
description: 取消发送操作
ms.assetid: 5bd7a815-4e4d-4259-b322-f4f8d07f2e1a
keywords:
- 网络数据 WDK，发送
- 数据 WDK 连接网络、 发送
- 数据包 WDK 连接网络、 发送
- 发送数据 WDK 网络
- NDIS_SET_NET_BUFFER_LIST_CANCEL_ID
- 取消发送操作 WDK 网络
- 取消 Id WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fa24eceedc606034b880484bd119faa56494981
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369066"
---
# <a name="canceling-a-send-operation"></a>取消发送操作





下图说明了取消发送操作。

![说明取消发送操作的关系图](images/netbuffercancelsend.png)

驱动程序调用[ **NDIS\_设置\_NET\_缓冲区\_列表\_取消\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff567299)宏为每个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，它将传递到较低级别的驱动程序以进行传输。 NDIS\_设置\_NET\_缓冲区\_列表\_取消\_ID 函数会将标记包含取消标识符的指定的数据包。

在将取消 Id 分配到数据包前, 一个驱动程序应调用[ **NdisGeneratePartialCancelId** ](https://msdn.microsoft.com/library/windows/hardware/ff562623)获取它将分配每个取消 ID 的高序位字节。 这可确保该驱动程序不复制取消由其他驱动程序分配在系统中的 Id。 通常情况下，驱动程序调用**NdisGeneratePartialCancelId**一次从**DriverEntry**例程; 但是，驱动程序可以通过调用获取多个部分取消标识符**NdisGeneratePartialCancelId**不止一次。

若要取消挂起的标记的.NET 中的数据传输\_缓冲区\_列表结构驱动程序将传递到取消 ID [ **NdisCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561623)函数。 驱动程序可以获取 NET\_缓冲区\_通过调用列表结构取消 ID [ **NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff565683)宏。

如果驱动程序将标记所有[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)具有相同的取消标识符的结构，它可以取消所有挂起的传输的单个调用**NdisCancelSendNetBufferLists**。 如果驱动程序将标记所有 NET\_缓冲区\_内的 NET 子组的列表结构\_缓冲区\_具有唯一标识符的列表结构，它可以取消所有挂起的传输中通过调用一次该子组向**NdisCancelSendNetBufferLists**。

NDIS 调用[ *MiniportCancelSend* ](https://msdn.microsoft.com/library/windows/hardware/ff559342)函数在绑定上相应的较低级驱动程序。 正在中止挂起的传输后，将调用基础微型端口驱动程序[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数，返回 NET\_缓冲区\_列表结构和完成状态的 NDIS\_状态\_发送\_已中止。 NDIS，反过来，调用相应的驱动程序[ **ProtocolSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570268)函数。

在其*ProtocolSendNetBufferListsComplete*函数，协议驱动程序可以调用 NDIS\_设置\_NET\_缓冲区\_列表\_取消\_与 ID*CancelId*设置为**NULL**。 这可以防止 NET\_缓冲区\_列表会无意中使用同样的过时取消 id。

 

 





