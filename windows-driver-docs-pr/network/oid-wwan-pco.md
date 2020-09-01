---
title: OID_WWAN_PCO
description: OID_WWAN_PCO 报告调制解调器从操作员网络接收到的 PCO 值的状态和负载。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_PCO，PCO OID
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9947a40412e7c35caf8c80ce67975b72eeee365
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209293"
---
# <a name="oid_wwan_pco"></a>OID_WWAN_PCO

OID_WWAN_PCO 将报告从移动运营商网络接收到的协议配置 Optiont (PCO) 值的状态和有效负载。 从调制解调器返回的 PCO 值对应于端口号在 OID 请求结构中指定的 PDN。

对于查询请求，该调制解调器在收到此 OID 时首先会响应 NDIS_STATUS_INDICATION_REQUIRED。 查询请求完成时，将返回包含[NDIS_WWAN_PCO_STATUS](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)结构的[NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)通知。 **NDIS_WWAN_PCO_STATUS**又包含了 PCO 状态和表示 PCO 值的 [WWAN_PCO_VALUE](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value) 结构。

设置请求不适用。

## <a name="remarks"></a>备注

对于选择使用 Microsoft 收件箱微型类驱动程序的调制解调器，若要接收来自主机的查询请求，则调制解调器必须在响应**MBIM_CID_DEVICE_SERVICES**查询时播发它支持新的**MBIM_CID_PCO** CID (index = 9) **MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**服务中。 有关 *MBIM_CID_PCO*的详细信息，请参阅 [ (PCO) 操作的 MB 协议配置选项](mb-protocol-configuration-options-pco-operations.md)。

对于选择不使用 Microsoft 收件箱微型类驱动程序的调制解调器，若要接收来自 WWANSVC 的查询请求，则调制解调器的微型端口驱动程序必须在响应[OID OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)查询请求时播发该驱动程序支持*WWAN_OPTIONAL_SERVICE_CAPS_PCO*选项。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1709 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[**NDIS_STATUS_WWAN_PCO_STATUS**](ndis-status-wwan-pco-status.md)

[**NDIS_WWAN_PCO_STATUS**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)

[**WWAN_PCO_VALUE**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_pco_value) 

[**OID OID_WWAN_DEVICE_CAPS_EX**](oid-wwan-device-caps-ex.md)

[MB 协议配置选项 (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)