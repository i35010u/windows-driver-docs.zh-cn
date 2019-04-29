---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID
description: WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 是 TLV 包含标识此状态指示所属的设备服务的 GUID。
ms.assetid: BBD64E6F-A2E2-4601-A231-4FCB4574EFC7
ms.date: 06/15/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0a07ccc43724f11b6d29c2c7bb29f8bc313f2f0f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365371"
---
# <a name="wditlvdeviceserviceparamsguid"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_GUID

WDI_TLV_DEVICE_SERVICE_PARAMS_GUID 是 TLV 包含标识此状态指示所属的设备服务的 GUID。 在中使用此 TLV [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状态指示。

## <a name="tlv-type"></a>TLV 类型

0x140

## <a name="length"></a>长度

以字节为单位，GUID 的大小。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| GUID | 标识此状态指示所属 （如 IHV/OEM 所定义） 的设备服务的 GUID。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1809 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
