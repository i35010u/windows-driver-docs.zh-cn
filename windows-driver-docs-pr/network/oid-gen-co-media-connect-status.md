---
title: OID_GEN_CO_MEDIA_CONNECT_STATUS
description: 本主题介绍 OID_GEN_CO_MEDIA_CONNECT_STATUS 对象标识符 (OID)。
ms.assetid: d49ebdfb-1c41-40dc-86bf-01db50a73607
keywords:
- OID_GEN_CO_MEDIA_CONNECT_STATUS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c88cda4dc1b2dd3b438c6ff73b4ae18e05e8fc43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361175"
---
# <a name="oidgencomediaconnectstatus"></a>OID_GEN_CO_MEDIA_CONNECT_STATUS

OID_GEN_CO_MEDIA_CONNECT_STATUS OID 请求微型端口驱动程序，以在网络上的 NIC 的连接状态返回作为系统定义的以下值之一：

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

当微型端口驱动程序检测到的网络连接已丢失时，则应调用[NdisMCoIndicateStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex) NDIS_STATUS_MEDIA_DISCONNECT 使用。 当恢复连接时，它应调用与 NDIS_STATUS_MEDIA_CONNECT NdisMCoIndicateStatus。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

