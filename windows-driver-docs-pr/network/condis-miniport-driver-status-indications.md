---
title: CoNDIS 微型端口驱动程序状态指示
description: CoNDIS 微型端口驱动程序状态指示
ms.assetid: 1f1174ba-8b0a-4d43-96c9-2d92f50a22c4
keywords:
- 微型端口驱动程序 WDK 网络，CoNDIS
- NDIS 微型端口驱动程序 WDK，CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95bfba37c3f77585a3aaa934f084e2be5b74350b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835102"
---
# <a name="condis-miniport-driver-status-indications"></a>CoNDIS 微型端口驱动程序状态指示





微型端口驱动程序调用[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)函数来报告微型端口适配器的状态更改。 微型端口驱动程序将指向[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针（包含状态信息）传递给**NdisMCoIndicateStatusEx** 。

状态指示包含用于标识状态类型和状态更改原因的信息。

微型端口驱动程序应将 NDIS\_状态\_指示结构的**SourceHandle**成员设置为 ndis 传递到[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的*MiniportAdapterHandle*参数的句柄。 如果状态指示与 OID 请求关联，则微型端口驱动程序可以将 NDIS\_状态的**DestinationHandle**和**RequestId**成员设置\_指示，以便 ndis 可以向特定的协议绑定。 有关 OID 请求的详细信息，请参阅[CoNDIS 微型端口驱动程序 OID 请求](condis-miniport-driver-oid-requests.md)。

 

 





