---
title: NDIS_STATUS_WWAN_LTE_ATTACH_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知来通知关于完成的上一个 OID_WWAN_LTE_ATTACH_STATUS 查询请求的移动宽带 (MB) 服务。
ms.assetid: 8A40437E-7AAC-4829-A032-0B8C933A7AC0
ms.date: 08/23/2018
keywords: -NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e3dcd88fa09cd7d99c5baf53f9bc5fa4366035b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346071"
---
# <a name="ndisstatuswwanlteattachstatus"></a>NDIS_STATUS_WWAN_LTE_ATTACH_STATUS

微型端口驱动程序使用 NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知来告知在前一次完成移动宽带 (MB) 服务[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)查询请求。

如果上下文为 LTE 附加已激活，这可能是如插入 SIM 时发送未经请求的事件。 在这种情况下，微型端口驱动程序应与主机 OS 发送此通知。

此状态通知使用[ **NDIS_WWAN_LTE_ATTACH_STATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10 版本 1703 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB LTE 附加操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)

[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)
