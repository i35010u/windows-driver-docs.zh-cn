---
title: CoNDIS 微型端口驱动程序状态指示
description: CoNDIS 微型端口驱动程序状态指示
ms.assetid: 1f1174ba-8b0a-4d43-96c9-2d92f50a22c4
keywords:
- 微型端口驱动程序 WDK 网络的 CoNDIS
- NDIS 微型端口驱动程序 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a815ef4b31ca0d59fc23c9383a00dc4fe5310a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390734"
---
# <a name="condis-miniport-driver-status-indications"></a>CoNDIS 微型端口驱动程序状态指示





微型端口驱动程序调用[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)函数报告的微型端口适配器状态中的更改。 微型端口驱动程序传递**NdisMCoIndicateStatusEx**指向的指针[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构，其中包含状态信息。

状态指示包括的信息来标识的类型的状态和状态更改的原因。

微型端口驱动程序应设置**SourceHandle**成员的 NDIS\_状态\_指示结构到 NDIS 传递给的句柄*MiniportAdapterHandle*参数[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。 如果使用 OID 请求相关联的状态指示，则可以设置微型端口驱动程序**DestinationHandle**和**RequestId**的 NDIS 成员\_状态\_指示以便该 NDIS 可以提供特定的协议绑定到的状态指示。 有关 OID 的请求的详细信息，请参阅[CoNDIS 微型端口驱动程序 OID 请求](condis-miniport-driver-oid-requests.md)。

 

 





