---
title: OID_GEN_CO_MEDIA_CONNECT_STATUS
description: 本主题介绍 OID_GEN_CO_MEDIA_CONNECT_STATUS 对象标识符（OID）。
ms.assetid: d49ebdfb-1c41-40dc-86bf-01db50a73607
keywords:
- OID_GEN_CO_MEDIA_CONNECT_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7966d9d618780c619145f316df34d45c9d9b034
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916902"
---
# <a name="oid_gen_co_media_connect_status"></a>OID_GEN_CO_MEDIA_CONNECT_STATUS

OID_GEN_CO_MEDIA_CONNECT_STATUS OID 请求微型端口驱动程序将网络上 NIC 的连接状态返回为以下系统定义的值之一：

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

当微型端口驱动程序感知到网络连接已丢失时，它应使用 NDIS_STATUS_MEDIA_DISCONNECT 调用[NdisMCoIndicateStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) 。 在恢复连接时，它应 NDIS_STATUS_MEDIA_CONNECT 调用 NdisMCoIndicateStatus。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

