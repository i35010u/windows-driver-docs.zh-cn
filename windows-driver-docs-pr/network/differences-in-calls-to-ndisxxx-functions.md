---
title: NdisXxx 函数调用的差异
description: NdisXxx 函数调用的差异
ms.assetid: 967ad913-24ca-4f05-b10b-1daa88845ed3
keywords:
- NdisCmXxx 函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e784b67678f731cebefa22b5354238aaa53cf9a3
ms.sourcegitcommit: 8486945726d87cf983a7035360059d9f9ab765a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68808269"
---
# <a name="differences-in-calls-to-ndisxxx-functions"></a>NdisXxx 函数调用的差异





调用管理器调用一组不同于 MCM 驱动程序的调用管理器功能。 调用管理器调用**NdisCm_Xxx_** 函数, MCM 驱动程序调用**NdisMCm_Xxx_** 函数。

MCM 驱动程序不调用面向连接的客户端和调用管理器都调用的**NdisCo_Xxx_** 函数。 相反, MCM 驱动程序会调用以下类似的**NdisMCm_Xxx_** 函数:

-   [**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc)而不是[ **NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscocreatevc)

-   [**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc)而不是[ **NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscodeletevc)

-   [**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequest)而不是[ **NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)

-   [**NdisMCmOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequestcomplete)而不是[ **NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)

MCM 驱动程序不需要与[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)相当的呼叫, 因为呼叫管理器和微型端口驱动程序之间的发送接口是 MCM 驱动程序的内部, 因此不能与 NDIS 进行透明。

 

 





