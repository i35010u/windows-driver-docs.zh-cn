---
title: MB 调制解调器重置操作
description: MB 调制解调器重置操作
ms.assetid: E33073B5-53D5-4F6F-85EC-5B46FDE9EA4D
keywords:
- MB 调制解调器重置，移动宽带调制解调器重置，移动宽带的微型端口驱动程序调制解调器重置
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6172d1949ae8b52a8c353f26503d14ad01435a80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547610"
---
# <a name="mb-modem-reset-operations"></a>MB 调制解调器重置操作

本部分将定义 MBIM CID 命令和数据结构，以及 NDIS OID 命令和数据结构，用于重置移动宽带 (MB) 设备中的调制解调器。 Windows 10 版本 1709年及更高版本中提供了这些命令和数据结构。

## <a name="mbimcidmsdevicereset"></a>MBIM_CID_MS_DEVICE_RESET

主机将 MBIM_CID_MS_DEVICE_RESET 发送到 MBIM 函数，以将调制解调器设备重置。

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft Basic IP 连接扩展 | UUID_BASIC_CONNECT_EXTENSIONS | 3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf |

| CID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- |
| MBIM_CID_MS_DEVICE_RESET | 10 | Y | N | N |

### <a name="parameters"></a>参数

|   | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 空 | 不适用 | 不适用 |
| 响应 | 空 | 不适用 | 不适用 |

### <a name="query"></a>查询

不适用。

### <a name="set"></a>设置

InformationBuffer 应为 NULL 并且*InformationBufferLength*应该为零。

### <a name="response"></a>响应

InformationBuffer 应为 NULL 并且*InformationBufferLength*应该为零。

### <a name="notification"></a>通知

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码都适用。 重置完成后，作为对设置操作的异步响应返回状态。

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 操作成功。 |
| MBIM_STATUS_BUSY | 设备正在使用。 |
| MBIM_STATUS_FAILURE | 操作失败。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 设备不支持此操作。 |

## <a name="oidwwandevicereset"></a>OID_WWAN_DEVICE_RESET

MBIM_CID_MS_DEVICE_RESET NDIS 等效项是[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)。
