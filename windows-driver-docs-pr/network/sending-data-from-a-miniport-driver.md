---
title: 从微型端口驱动程序发送数据
description: 从微型端口驱动程序发送数据
ms.assetid: f82475ff-8d32-4448-9b19-b6fa97a93d32
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec41f368d101e216234767a4a18aa6924feccced
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555178"
---
# <a name="sending-data-from-a-miniport-driver"></a>从微型端口驱动程序发送数据





下图说明了微型端口驱动程序发送操作。

![说明微型端口驱动程序的关系图发送操作](images/miniportsend.png)

NDIS 调用微型端口驱动程序[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)函数将链接列表所述的网络数据传输[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

微型端口驱动程序调用[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数以返回 NET 的链接的列表\_缓冲区\_列表结构到基础驱动程序，并返回发送请求的最终状态。

 

 





