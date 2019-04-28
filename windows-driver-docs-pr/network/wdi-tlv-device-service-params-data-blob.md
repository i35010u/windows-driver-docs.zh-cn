---
title: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB
description: WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 是 TLV，其中包含有关设备服务从 IHV 驱动程序收到的信息。
ms.assetid: D07CDC24-849F-447A-8447-FD2D37178C42
ms.date: 06/15/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 76bec883c708bb9976d907c119e0cc790e5b4e0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331849"
---
# <a name="wditlvdeviceserviceparamsdatablob"></a>WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB

WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB 是 TLV，其中包含有关设备服务从 IHV 驱动程序收到的信息。 在中使用此 TLV [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md)状态指示。

## <a name="tlv-type"></a>TLV 类型

0x141

## <a name="length"></a>长度

大小，以字节为单位的`(UINT8 * (the number of elements in the list))`。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| TLV\<List\<UINT8\>\> | [可选]从 IHV 驱动程序收到的信息。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1809 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
