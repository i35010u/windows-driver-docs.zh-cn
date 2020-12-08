---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID
description: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 是一种 TLV，其中包含 GUID 来标识此状态指示所属的设备服务。
ms.date: 06/15/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 564cbd722fc3dde48e9e512e64539947d2b59082
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790371"
---
# <a name="wdi_tlv_device_service_params_guid"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_GUID

WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 是一种 TLV，其中包含 GUID 来标识此状态指示所属的设备服务。 此 TLV 用于 [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md) 状态指示。

## <a name="tlv-type"></a>TLV 类型

0x140

## <a name="length"></a>长度

GUID 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| GUID | 标识此状态指示所属的设备服务 (由 IHV/OEM) 定义的 GUID。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1809

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp

