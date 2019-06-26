---
title: NDIS_STATUS_WWAN_UICC_RESET_INFO
description: NDIS_STATUS_WWAN_UICC_RESET_INFO
ms.assetid: ADA3ADC9-82AD-423A-ABA4-902EAF5F5C74
keywords:
- NDIS_STATUS_WWAN_UICC_RESET_INFO，UICC 重置状态通知、 移动宽带 UICC 重置状态通知、 MB UICC 重置状态通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e378f155cd928e09462f2c498599ee6ccc9a6ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384391"
---
# <a name="ndisstatuswwanuiccresetinfo"></a>NDIS_STATUS_WWAN_UICC_RESET_INFO

调制解调器微型端口适配器发送 NDIS_STATUS_WWAN_UICC_RESET_INFO 状态通知来通知 MB 到主机的主机的当前的传递状态 UICC 智能卡。 Folloiwng 两个方案中发送此通知：

1. 之后[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)查询请求。
2. 完成 UICC 重置后遵循 OID_WWAN_UICC_RESET 设置请求，以通知 MB 主机 UICC 卡后重置的传递状态。

使用此通知[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)结构。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>请参阅

[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)

[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)

[MB 低级别 UICC 访问](mb-low-level-uicc-access.md)

