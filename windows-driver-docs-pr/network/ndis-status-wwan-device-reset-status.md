---
title: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
description: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
ms.assetid: 3745E3A8-6807-4BAF-8074-90C661EAD15E
keywords:
- NDIS_STATUS_WWAN_DEVICE_RESET_STATUS，调制解调器重置状态通知、 移动宽带调制解调器重置状态通知、 MB 调制解调器重置状态通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1755716139d831c4a2015db127e99eb22ddd5e0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523115"
---
# <a name="ndisstatuswwandeviceresetstatus"></a>NDIS_STATUS_WWAN_DEVICE_RESET_STATUS

调制解调器微型端口驱动程序发送 NDIS_STATUS_WWAN_DEVICE_RESET_STATUS 通知来通知 MB 宿主的调制解调器设备重置状态。 此通知将发送到的异步响应作为[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)集请求。

使用此通知[NDIS_WWAN_DEVICE_RESET_STATUS](https://msdn.microsoft.com/library/windows/hardware/D18E8633-BEAD-49A5-A730-10564AFF8A3E)结构。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ndis.h |

## <a name="see-also"></a>另请参阅

[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](https://msdn.microsoft.com/library/windows/hardware/D18E8633-BEAD-49A5-A730-10564AFF8A3E)

[MB 调制解调器重置操作](mb-modem-reset-operations.md)

