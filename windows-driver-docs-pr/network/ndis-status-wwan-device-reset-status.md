---
title: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
description: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
ms.assetid: 3745E3A8-6807-4BAF-8074-90C661EAD15E
keywords:
- NDIS_STATUS_WWAN_DEVICE_RESET_STATUS，调制解调器重置状态通知，移动宽带调制解调器重置状态通知，MB 调制解调器重置状态通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd39c586735ba50542471ba896b0eba62f2c7788
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842631"
---
# <a name="ndis_status_wwan_device_reset_status"></a>NDIS_STATUS_WWAN_DEVICE_RESET_STATUS

NDIS_STATUS_WWAN_DEVICE_RESET_STATUS 通知通过调制解调器微型驱动程序发送，通知 MB 主机调制解调器设备的重置状态。 此通知将作为异步响应发送到[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)设置请求。

此通知使用[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)结构。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ndis。h |

## <a name="see-also"></a>另请参阅

[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[MB 调制解调器重置操作](mb-modem-reset-operations.md)

