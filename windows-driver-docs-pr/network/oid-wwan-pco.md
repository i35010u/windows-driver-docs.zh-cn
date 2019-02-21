---
title: OID_WWAN_PCO
description: OID_WWAN_PCO 报告的状态和调制解调器都已收到来自运营商网络 PCO 值的有效负载。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_PCO、 PCO OID
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5b6d0a71570cb0afa66b2c1181d1a3c6b24edfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525433"
---
# <a name="oidwwanpco"></a>OID_WWAN_PCO

OID_WWAN_PCO 报告的状态和调制解调器都已收到来自移动运营商网络协议配置 Optiont (PCO) 值的有效负载。 返回从调制解调器的 PCO 值对应于 PDN OID 请求结构中指定的端口号。

对于查询请求，调制解调器首先响应 NDIS_STATUS_INDICATION_REQUIRED 接收此 OID 时。 [NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)通知将返回包含[NDIS_WWAN_PCO_STATUS](https://msdn.microsoft.com/library/windows/hardware/C71187C5-74B6-450A-8461-BB9FDF60DB8D)结构查询请求完成时。 **NDIS_WWAN_PCO_STATUS**，又包含 PCO 状态和一个[WWAN_PCO_VALUE](https://msdn.microsoft.com/library/windows/hardware/45A499CE-2C9A-4070-BEF8-880E7673FA8E)结构，它表示 PCO 值。

不适用集发出的请求。

## <a name="remarks"></a>备注

选择使用 Microsoft 收件箱微型端口类驱动程序中，若要从主机接收查询请求的调制解调器，调制解调器必须播发，它支持的新**MBIM_CID_PCO** CID (索引 = 9) 中**MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**服务响应时**MBIM_CID_DEVICE_SERVICES**查询。 有关详细信息*MBIM_CID_PCO*，请参阅[MB 协议配置选项 (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)。

对于选择的调制解调器不使用 Microsoft 收件箱微型端口类驱动程序，以便接收来自 WWANSVC 查询请求，它支持对调制解调器的微型端口驱动程序必须播发*WWAN_OPTIONAL_SERVICE_CAPS_PCO*选项时响应向[OID OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)查询请求。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>另请参阅

[**NDIS_STATUS_WWAN_PCO_STATUS**](ndis-status-wwan-pco-status.md)

[**NDIS_WWAN_PCO_STATUS**](https://msdn.microsoft.com/library/windows/hardware/C71187C5-74B6-450A-8461-BB9FDF60DB8D)

[**WWAN_PCO_VALUE**](https://msdn.microsoft.com/library/windows/hardware/45A499CE-2C9A-4070-BEF8-880E7673FA8E) 

[**OID OID_WWAN_DEVICE_CAPS_EX**](oid-wwan-device-caps-ex.md)

[MB 协议配置选项 (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)
