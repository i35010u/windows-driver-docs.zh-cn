---
title: NdisXxx 函数调用的差异
description: NdisXxx 函数调用的差异
ms.assetid: 967ad913-24ca-4f05-b10b-1daa88845ed3
keywords:
- NdisCmXxx 函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a4a3f7138c93e35f97a337b46d8dea309af57f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381380"
---
# <a name="differences-in-calls-to-ndisxxx-functions"></a>NdisXxx 函数调用的差异





呼叫管理器调用了一组不同的调用与 MCM 驱动程序管理器函数。 呼叫管理器调用**NdisCm * Xxx*** 函数和 MCM 驱动程序调用**NdisMCm * Xxx*** 函数。

MCM 驱动程序不会调用**NdisCo * Xxx*** 面向连接的客户端和调用管理器调用的函数。 改为 MCM 驱动程序调用以下相当**NdisMCm * Xxx*** 函数：

-   [**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc) instead of [**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscocreatevc)

-   [**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc) instead of [**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscodeletevc)

-   [**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequest) instead of [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)

-   [**NdisMCmOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequestcomplete) instead of [**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)

MCM 驱动程序不需要相当于调用[ **NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)，因为呼叫管理器和微型端口驱动程序之间的发送接口是 MCM 驱动程序的内部和因此不透明的 NDIS。

 

 





