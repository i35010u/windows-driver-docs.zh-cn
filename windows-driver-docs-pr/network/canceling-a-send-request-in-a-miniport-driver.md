---
title: 正在取消微型端口驱动程序中的发送请求
description: 正在取消微型端口驱动程序中的发送请求
ms.assetid: 9339e661-b91a-49e1-9924-66c85cc80ee8
keywords:
- NdisCancelSendNetBufferLists
- MiniportCancelSend
- 取消发送请求 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323ff3f63d506620382aa38dc574e50603d68597
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526463"
---
# <a name="canceling-a-send-request-in-a-miniport-driver"></a>正在取消微型端口驱动程序中的发送请求





下图说明了微型端口驱动程序取消发送操作。

![说明的微型端口驱动程序取消发送操作的关系图](images/miniportcancelsend.png)

协议、 筛选和中间驱动程序可以调用[ **NdisCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561623)取消未完成发送请求。 这些基础驱动程序必须在发送请求之前将取消 id 的发送数据。

NDIS 调用微型端口驱动程序[ *MiniportCancelSend* ](https://msdn.microsoft.com/library/windows/hardware/ff559342)函数取消所有传输[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)用指定的取消标识符标记的结构。

微型端口驱动程序*MiniportCancelSend*函数执行以下操作：

1.  遍历的未完成发送请求指定的适配器并调用其列表[ **NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff565683)获取的每个网络取消标识符\_缓冲区\_列表结构。 微型端口驱动程序进行比较的取消操作 ID 的 NDIS\_获取\_NET\_缓冲区\_列表\_取消\_ID 返回 NDIS 传递给取消 ID *MiniportCancelSend*。

2.  删除从所有 NET\_缓冲区\_列表结构取消标识符匹配的未完成其列表中的指定的取消标识符将请求发送。

3.  调用[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数的所有已取消 NET\_缓冲区\_列表结构，以返回结构。微型端口驱动程序设置状态字段中的 NET\_缓冲区\_列表结构到 NDIS\_状态\_发送\_已中止。

 

 





