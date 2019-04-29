---
title: NDIS_STATUS_WWAN_UICC_RESET_INFO
description: NDIS_STATUS_WWAN_UICC_RESET_INFO
ms.assetid: ADA3ADC9-82AD-423A-ABA4-902EAF5F5C74
keywords:
- NDIS_STATUS_WWAN_UICC_RESET_INFO，UICC 重置状态通知、 移动宽带 UICC 重置状态通知、 MB UICC 重置状态通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6deb8a53742bb47118eb823eefd43633a93e2b09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324893"
---
# <a name="ndisstatuswwanuiccresetinfo"></a>NDIS_STATUS_WWAN_UICC_RESET_INFO

调制解调器微型端口适配器发送 NDIS_STATUS_WWAN_UICC_RESET_INFO 状态通知来通知 MB 到主机的主机的当前的传递状态 UICC 智能卡。 Folloiwng 两个方案中发送此通知：

1. 之后[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)查询请求。
2. 完成 UICC 重置后遵循 OID_WWAN_UICC_RESET 设置请求，以通知 MB 主机 UICC 卡后重置的传递状态。

使用此通知[NDIS_WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/9CBAFC44-187A-41ED-9405-1208167AC75D)结构。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>请参阅

[OID_WWAN_UICC_RESET](oid-wwan-uicc-reset.md)

[NDIS_WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/9CBAFC44-187A-41ED-9405-1208167AC75D)

[MB 低级别 UICC 访问](mb-low-level-uicc-access.md)

