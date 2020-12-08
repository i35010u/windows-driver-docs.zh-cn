---
title: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
description: NDIS_STATUS_WWAN_DEVICE_RESET_STATUS
keywords:
- NDIS_STATUS_WWAN_DEVICE_RESET_STATUS、调制解调器重置状态通知、移动宽带调制解调器重置状态通知、MB 调制解调器重置状态通知
ms.date: 08/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4f0bbbbe6f3993ab9c54765e6809e7b31f63387
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822187"
---
# <a name="ndis_status_wwan_device_reset_status"></a>NDIS_STATUS_WWAN_DEVICE_RESET_STATUS

NDIS_STATUS_WWAN_DEVICE_RESET_STATUS 通知通过调制解调器微型驱动程序发送，通知 MB 主机调制解调器设备的重置状态。 此通知将作为异步响应发送到 [OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md) 集请求。

此通知使用 [NDIS_WWAN_DEVICE_RESET_STATUS](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1709 **头**： Ndis。h

## <a name="see-also"></a>请参阅

[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)

[NDIS_WWAN_DEVICE_RESET_STATUS](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_reset_status)

[MB 调制解调器重置操作](mb-modem-reset-operations.md)
