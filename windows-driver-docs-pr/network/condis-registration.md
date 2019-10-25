---
title: CoNDIS 注册
description: CoNDIS 注册
ms.assetid: 6db5a4a2-f090-4688-99fa-9d22ca7077ed
keywords:
- CoNDIS WDK 网络，注册
- 注册 CoNDIS 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d9d118f8e499ac1dd66b8b669f91bbb905e681
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838188"
---
# <a name="condis-registration"></a>CoNDIS 注册





为了支持 CoNDIS，NDIS 驱动程序必须注册可选的 CoNDIS 函数入口点。 NDIS 驱动程序调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数来注册可选服务。

本部分包括下列主题：

[CoNDIS 微型端口驱动程序注册](condis-miniport-driver-registration.md)

[CoNDIS 客户端注册](condis-client-registration.md)

[CoNDIS 呼叫管理器注册](condis-call-manager-registration.md)

[CoNDIS MCM 注册](condis-mcm-registration.md)

 

 





