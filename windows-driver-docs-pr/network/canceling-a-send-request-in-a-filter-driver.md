---
title: 正在取消筛选器驱动程序中的发送请求
description: 正在取消筛选器驱动程序中的发送请求
ms.assetid: afa9c8d3-b30b-4009-8428-d31719885154
keywords:
- 取消发送操作 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dfeda07f9ef8a4178781f2c8a9fb18fc3ac98e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523198"
---
# <a name="canceling-a-send-request-in-a-filter-driver"></a>正在取消筛选器驱动程序中的发送请求





筛选器驱动程序可以取消已发起的筛选器驱动程序或已通过过量驱动程序上发起的发送请求。

### <a name="canceling-filter-driver-send-requests"></a>正在取消筛选器驱动程序发送请求

下图说明了取消生成的筛选器驱动程序的发送请求。

![说明取消生成的筛选器驱动程序的发送请求的关系图](images/filtercancelsend.png)

筛选器驱动程序调用[ **NDIS\_设置\_NET\_缓冲区\_列表\_取消\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff567299)为每个宏[**NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)它创建的发送操作的结构。 NDIS\_设置\_NET\_缓冲区\_列表\_取消\_ID 函数会将标记与取消标识符指定的数据。

将取消 Id 分配给网络数据之前, 筛选器驱动程序必须调用[ **NdisGeneratePartialCancelId** ](https://msdn.microsoft.com/library/windows/hardware/ff562623)获取它将分配每个取消 ID 的高序位字节。 这可确保该驱动程序不复制取消由其他驱动程序分配在系统中的 Id。 通常情况下，驱动程序调用**NdisGeneratePartialCancelId**从一次[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。 但是，驱动程序可以通过调用获取多个部分取消标识符**NdisGeneratePartialCancelId**多次。

若要取消挂起的标记的.NET 中的数据传输\_缓冲区\_列表结构筛选器驱动程序将传递到取消 ID [ **NdisFCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561794)函数。 驱动程序可以获取 NET\_缓冲区\_通过调用列表结构取消 ID [ **NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff565683)宏。

如果筛选器驱动程序将标记所有 NET\_缓冲区\_具有相同的取消标识符列表结构，它可以取消所有挂起传输的调用一次**NdisFCancelSendNetBufferLists**。 如果筛选器驱动程序将标记所有 NET\_缓冲区\_内的 NET 子组的列表结构\_缓冲区\_具有唯一标识符的列表结构，它可以取消与此子组中所有挂起的传输单一调用**NdisFCancelSendNetBufferLists**。

NDIS 调用基础驱动程序的取消按钮发送函数。 在中止挂起的传输之后, 基础驱动程序调用发送完整函数 (例如[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)) 以返回 NET\_缓冲区\_且完成状态的 NDIS 列表结构\_状态\_发送\_已中止。 NDIS，反过来，调用筛选器驱动程序[ *FilterSendNetBufferListsComplete* ](https://msdn.microsoft.com/library/windows/hardware/ff549967)函数。

在中*FilterSendNetBufferListsComplete*，筛选器驱动程序可以调用 NDIS\_设置\_NET\_缓冲区\_列表\_取消\_ID 与*CancelId*设置为**NULL**。 这可以防止 NET\_缓冲区\_列表意外使用同样的过时取消 id。

### <a name="canceling-send-requests-originated-by-overlying-drivers"></a>取消由基础驱动程序产生的发送请求

下图说明了取消生成的基础驱动程序的发送请求。

![说明取消生成的基础驱动程序的发送请求的关系图](images/cancelfiltersend.png)

基础驱动程序调用取消按钮发送函数 ( [ **NdisFCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561794)或[ **NdisCancelSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561623)) 到取消未完成发送请求。 这些基础驱动程序必须在发送请求之前将取消 id 的发送数据。

NDIS 筛选器驱动程序将调用[ *FilterCancelSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549915)函数取消所有传输[ **NET\_缓冲区\_列表** ](https://msdn.microsoft.com/library/windows/hardware/ff568388)用指定的取消标识符标记的结构。

*FilterCancelSendNetBufferLists*执行以下操作：

1.  遍历筛选器驱动程序的列表中的排队 NET\_缓冲区\_指定的筛选器模块和调用列表结构[ **NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff565683)宏，以获取取消标识符为每个结构。 筛选器驱动程序进行比较的取消操作 ID 的 NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID 返回 NDIS 传递给取消 ID *FilterCancelSendNetBufferLists*。

2.  从 （断开的链接） 的发送队列中移除所有的 NET\_缓冲区\_取消标识符匹配指定的取消标识符的列表结构。

3.  调用[ **NdisFSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562618)函数的所有未链接 NET\_缓冲区\_列表结构，以返回结构。 筛选器驱动程序设置状态字段中的 NET\_缓冲区\_列表结构到 NDIS\_状态\_发送\_已中止。

4.  调用**NdisFCancelSendNetBufferLists**函数传递取消将请求发送到基础驱动程序。 筛选器驱动程序将其从基础驱动程序收到的取消标识符传递。 使用筛选器驱动程序产生的取消将发送操作，继续执行取消操作。

 

 





