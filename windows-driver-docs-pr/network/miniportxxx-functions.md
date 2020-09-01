---
title: MiniportXxx 函数
description: MiniportXxx 函数
ms.assetid: b992c3ff-deb1-49e2-a99f-310cc4cb81c3
keywords:
- MiniportXxx 函数 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 251996b814f325e60667fdf324b1f293ce72a7d4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215548"
---
# <a name="miniportxxx-functions"></a>MiniportXxx 函数





典型的微型端口驱动程序使用少量的函数通过 NDIS 与上层和硬件进行通信。 并非所有这些函数都是必需的。 若要详细了解哪些函数是可选的（哪些是必需的）以及原因，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

NDIS 微型端口驱动程序和上层驱动程序使用 NDIS 库 ( # A0) 通过调用 **ndis * Xxx*** 函数互相通信。

许多微型端口驱动程序函数都可以同步或异步操作。 异步函数具有 **Ndis*Xxx*完成** 的函数，必须在操作完成时调用该函数。 例如，如果某个协议驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 来查询微型端口驱动程序信息，微型端口驱动程序的 *MiniportOidRequest* 函数可以通过返回 NDIS 状态 "挂起" 来挂起重置操作 \_ \_ 。 最后，微型端口驱动程序必须调用 [**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete) ，以指示查询请求的最终状态。

 

