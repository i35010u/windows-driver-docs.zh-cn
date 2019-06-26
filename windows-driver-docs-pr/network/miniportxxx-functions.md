---
title: MiniportXxx 函数
description: MiniportXxx 函数
ms.assetid: b992c3ff-deb1-49e2-a99f-310cc4cb81c3
keywords:
- MiniportXxx 函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1ece15239edda28c6f381e5b973f9226a3ddbb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382214"
---
# <a name="miniportxxx-functions"></a>MiniportXxx 函数





典型的微型端口驱动程序使用少量的函数来通过 NDIS 与较高的层和硬件进行通信。 并非所有这些函数都需要。 有关哪些函数是可选的详细信息，这是必需的并且，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

NDIS 微型端口驱动程序和上层驱动程序使用 NDIS 库 (Ndis.sys) 来相互通信通过调用到**Ndis * Xxx*** 函数。

很多微型端口驱动程序函数可以运行同步或异步。 异步函数具有**Ndis*Xxx*完成**必须完成操作调用的函数。 例如，如果协议驱动程序调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)查询微型端口驱动程序信息，微型端口驱动程序的*MiniportOidRequest*函数可以挂起重置操作，通过返回 NDIS\_状态\_PENDING。 最终，微型端口驱动程序必须调用[ **NdisMOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)以指示查询请求的最终状态。

 

 





