---
title: OID_WWAN_DEVICE_RESET
description: OID_WWAN_DEVICE_RESET
ms.assetid: CF15A1FD-9E48-458C-80DF-F63636F73962
keywords:
- MB 设备重置，移动宽带设备重置，移动宽带微型端口驱动程序设备重置
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: e06accfa568ec45084e3e543b63ef3766068f19e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218349"
---
# <a name="oid_wwan_device_reset"></a>OID_WWAN_DEVICE_RESET

移动宽带主机将 OID_WWAN_DEVICE_RESET 发送到调制解调器端口，以重置调制解调器设备。

查询请求不适用。

对于 Set 请求，OID_WWAN_DEVICE_RESET 使用 [NDIS_WWAN_SET_DEVICE_RESET](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset) 结构。 调制解调器小型端口驱动程序必须异步响应设置请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送 [NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md) 通知，其中包含表示调制解调器设备重置状态的 [NDIS_WWAN_DEVICE_RESET_STATUS](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status) 结构。 此响应不包含有效负载，但始终是调制解调器的状态代码，如 *WWAN_STATUS_SUCCESS* 或 *WWAN_STATUS_BUSY*。

未经请求的事件不适用。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1709 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[NDIS_WWAN_SET_DEVICE_RESET](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)

[MB 调制解调器重置操作](mb-modem-reset-operations.md)