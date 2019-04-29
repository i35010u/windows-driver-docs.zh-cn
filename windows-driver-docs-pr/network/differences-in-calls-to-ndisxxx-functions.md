---
title: NdisXxx 函数调用的差异
description: NdisXxx 函数调用的差异
ms.assetid: 967ad913-24ca-4f05-b10b-1daa88845ed3
keywords:
- NdisCmXxx 函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60f11be0dba00b38df3876e4cd53ea46dce6924
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379581"
---
# <a name="differences-in-calls-to-ndisxxx-functions"></a>NdisXxx 函数调用的差异





呼叫管理器调用了一组不同的调用与 MCM 驱动程序管理器函数。 呼叫管理器调用**NdisCm * Xxx*** 函数和 MCM 驱动程序调用**NdisMCm * Xxx*** 函数。

MCM 驱动程序不会调用**NdisCo * Xxx*** 面向连接的客户端和调用管理器调用的函数。 改为 MCM 驱动程序调用以下相当**NdisMCm * Xxx*** 函数：

-   [**NdisMCmCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562812) instead of [**NdisCoCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561696)

-   [**NdisMCmDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff562819) instead of [**NdisCoDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff561698)

-   [**NdisMCmOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563548) instead of [**NdisCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561711)

-   [**NdisMCmOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563551) instead of [**NdisCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561716)

MCM 驱动程序不需要相当于调用[ **NdisCoSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561728)，因为呼叫管理器和微型端口驱动程序之间的发送接口是 MCM 驱动程序的内部和因此不透明的 NDIS。

 

 





