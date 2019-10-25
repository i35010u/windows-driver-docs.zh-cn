---
title: OID_WWAN_DEVICE_RESET
description: OID_WWAN_DEVICE_RESET
ms.assetid: CF15A1FD-9E48-458C-80DF-F63636F73962
keywords:
- MB 设备重置，移动宽带设备重置，移动宽带微型端口驱动程序设备重置
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a8c69a8db7259445e4b7c926be833f8f3984a2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843860"
---
# <a name="oid_wwan_device_reset"></a>OID_WWAN_DEVICE_RESET

移动宽带主机将 OID_WWAN_DEVICE_RESET 发送到调制解调器端口，以重置调制解调器设备。

查询请求不适用。

对于 Set 请求，OID_WWAN_DEVICE_RESET 使用[NDIS_WWAN_SET_DEVICE_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)结构。 调制解调器小型端口驱动程序必须异步响应设置请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送包含 NDIS 的[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)通知[_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)结构，表示调制解调器设备的重置状态。 此响应不包含有效负载，但始终是调制解调器（如*WWAN_STATUS_SUCCESS*或*WWAN_STATUS_BUSY*）中的状态代码。

未经请求的事件不适用。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[NDIS_WWAN_SET_DEVICE_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)

[MB 调制解调器重置操作](mb-modem-reset-operations.md)

