---
title: OID_GEN_CO_MEDIA_CONNECT_STATUS
description: 本主题介绍) OID_GEN_CO_MEDIA_CONNECT_STATUS 对象标识符 (OID。
keywords:
- OID_GEN_CO_MEDIA_CONNECT_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5055789109fe2b51bb83f4562572115064049152
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806161"
---
# <a name="oid_gen_co_media_connect_status"></a>OID_GEN_CO_MEDIA_CONNECT_STATUS

OID_GEN_CO_MEDIA_CONNECT_STATUS OID 请求微型端口驱动程序将网络上 NIC 的连接状态返回为以下系统定义的值之一：

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

当微型端口驱动程序感知到网络连接已丢失时，它应使用 NDIS_STATUS_MEDIA_DISCONNECT 调用 [NdisMCoIndicateStatus](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) 。 在恢复连接时，它应 NDIS_STATUS_MEDIA_CONNECT 调用 NdisMCoIndicateStatus。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
