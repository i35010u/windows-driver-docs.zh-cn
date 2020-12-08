---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE
description: WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE 是一种 TLV，其中包含特定于设备服务的操作码。
ms.date: 06/15/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d14abd3a5bb138f767c4c294086a0bd6946384a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803483"
---
# <a name="wdi_tlv_device_service_params_opcode"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE

WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE 是一种 TLV，其中包含特定于设备服务的操作码。 此 TLV 用于 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md) 状态指示。

## <a name="tlv-type"></a>TLV 类型

0x13F

## <a name="length"></a>长度

UINT8 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| TLV\<UINT8\> | 特定于设备服务的操作码。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1809

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp

