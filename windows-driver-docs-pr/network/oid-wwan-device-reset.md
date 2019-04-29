---
title: OID_WWAN_DEVICE_RESET
description: OID_WWAN_DEVICE_RESET
ms.assetid: CF15A1FD-9E48-458C-80DF-F63636F73962
keywords:
- MB 设备重置，移动宽带设备重置，移动宽带的微型端口驱动程序设备重置
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009a309b889e3efbd06bf23dfa892eee7ca40e5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386677"
---
# <a name="oidwwandevicereset"></a>OID_WWAN_DEVICE_RESET

移动宽带调制解调器微型端口适配器主机发送 OID_WWAN_DEVICE_RESET 重置调制解调器设备。

查询请求不适用。

对于组的请求，使用 OID_WWAN_DEVICE_RESET [NDIS_WWAN_SET_DEVICE_RESET](https://msdn.microsoft.com/library/windows/hardware/73894308-CFE0-49EF-BB09-E104CEE9C746)结构。 调制解调器微型端口驱动程序必须响应以异步方式设置请求更高版本在发送之前对原始请求最初返回 NDIS_STATUS_INDICATION_REQUIRED [NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)通知包含[NDIS_WWAN_DEVICE_RESET_STATUS](https://msdn.microsoft.com/library/windows/hardware/D18E8633-BEAD-49A5-A730-10564AFF8A3E)结构，它表示的调制解调器设备重置状态。 此响应不包含有效负载，而是始终从调制解调器的状态代码如*WWAN_STATUS_SUCCESS*或*WWAN_STATUS_BUSY*。

未经请求的事件不适用。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[NDIS_STATUS_WWAN_DEVICE_RESET_STATUS](ndis-status-wwan-device-reset-status.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://msdn.microsoft.com/library/windows/hardware/D18E8633-BEAD-49A5-A730-10564AFF8A3E)

[NDIS_WWAN_SET_DEVICE_RESET](https://msdn.microsoft.com/library/windows/hardware/73894308-CFE0-49EF-BB09-E104CEE9C746)

[MB 调制解调器重置操作](mb-modem-reset-operations.md)

