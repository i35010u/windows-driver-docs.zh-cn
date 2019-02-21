---
title: OID_WWAN_UICC_RESET
description: OID_WWAN_UICC_RESET
ms.assetid: D6654B8D-8700-437B-A944-BB273C7D31A1
keywords:
- MB UICC 重置时，移动宽带 UICC 重置，移动宽带 UICC 重置的微型端口驱动程序
ms.date: 08/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: 133267fea9d3a6f0280132d134f014729c97a6ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525428"
---
# <a name="oidwwanuiccreset"></a>OID_WWAN_UICC_RESET

OID_WWAN_UICC_RESET 是发送到调制解调器微型端口适配器来重置 UICC 智能卡和指定 UICC 的传递状态之后重置，, 或查询该适配器的传递状态的移动宽带主机。

调制解调器微型端口驱动程序必须查询请求进行异步处理，最初在更高版本发送之前对原始请求返回 NDIS_STATUS_INDICATION_REQUIRED [NDIS_STATUS_WWAN_UICC_RESET_INFO](ndis-status-wwan-uicc-reset-info.md)通知包含[NDIS_WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/9CBAFC44-187A-41ED-9405-1208167AC75D)结构，其中又包含[WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/1D53135F-3826-4546-A0AD-34697D186E8A)结构，它表示适配器的传递状态。

对于组的请求，使用 OID_WWAN_UICC_RESET [NDIS_WWAN_SET_UICC_RESET](https://msdn.microsoft.com/library/windows/hardware/98113BC2-317C-4FBD-B3A6-A14B3783D225)结构，其中又包含[WWAN_SET_UICC_RESET](https://msdn.microsoft.com/library/windows/hardware/33711459-70C8-43D2-974D-B90EC0DD8ED6)结构，它表示传递操作主机指定的微型端口适配器后它会重置 UICC。 重置完成后，使用做出响应的微型端口适配器**NDIS_STATUS_WWAN_UICC_RESET_INFO**通知，又包含[NDIS_WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/9CBAFC44-187A-41ED-9405-1208167AC75D)结构，以指示其传递状态。

未经请求的事件不适用。

有关传递操作和传递状态的详细信息，请参阅[MB 低级别 UICC 访问](mb-low-level-uicc-access.md)。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>另请参阅

[NDIS_WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/9CBAFC44-187A-41ED-9405-1208167AC75D)

[WWAN_UICC_RESET_INFO](https://msdn.microsoft.com/library/windows/hardware/1D53135F-3826-4546-A0AD-34697D186E8A)

[NDIS_WWAN_SET_UICC_RESET](https://msdn.microsoft.com/library/windows/hardware/98113BC2-317C-4FBD-B3A6-A14B3783D225)

[WWAN_SET_UICC_RESET](https://msdn.microsoft.com/library/windows/hardware/33711459-70C8-43D2-974D-B90EC0DD8ED6)

[NDIS_STATUS_WWAN_UICC_RESET_INFO](ndis-status-wwan-uicc-reset-info.md)

[MB 低级别 UICC 访问](mb-low-level-uicc-access.md)

