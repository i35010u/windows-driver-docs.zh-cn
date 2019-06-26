---
title: OID_WWAN_DEVICE_RESET
description: OID_WWAN_DEVICE_RESET
ms.assetid: CF15A1FD-9E48-458C-80DF-F63636F73962
keywords:
- MB 设备重置，移动宽带设备重置，移动宽带的微型端口驱动程序设备重置
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03397a121a25efad0dcc420030bbc32e239f666b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362845"
---
# <a name="oidwwandevicereset"></a>OID_WWAN_DEVICE_RESET

移动宽带调制解调器微型端口适配器主机发送 OID_WWAN_DEVICE_RESET 重置调制解调器设备。

查询请求不适用。

对于组的请求，使用 OID_WWAN_DEVICE_RESET [NDIS_WWAN_SET_DEVICE_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)结构。 调制解调器微型端口驱动程序必须响应以异步方式设置请求更高版本在发送之前对原始请求最初返回 NDIS_STATUS_INDICATION_REQUIRED [NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)通知包含[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)结构，它表示的调制解调器设备重置状态。 此响应不包含有效负载，而是始终从调制解调器的状态代码如*WWAN_STATUS_SUCCESS*或*WWAN_STATUS_BUSY*。

未经请求的事件不适用。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[NDIS_WWAN_SET_DEVICE_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_reset)

[MB 调制解调器重置操作](mb-modem-reset-operations.md)

