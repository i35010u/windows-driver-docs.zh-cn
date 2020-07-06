---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID
description: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 是一种 TLV，其中包含 GUID 来标识此状态指示所属的设备服务。
ms.assetid: BBD64E6F-A2E2-4601-A231-4FCB4574EFC7
ms.date: 06/15/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c74ec4cb17a859c78c5b8742ccd696a92244a7c1
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968202"
---
# <a name="wdi_tlv_device_service_params_guid"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_GUID

WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 是一种 TLV，其中包含 GUID 来标识此状态指示所属的设备服务。 此 TLV 用于[NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状态指示。

## <a name="tlv-type"></a>TLV 类型

0x140

## <a name="length"></a>长度

GUID 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| GUID | 标识此状态指示所属的设备服务（由 IHV/OEM 定义）的 GUID。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1809

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp

