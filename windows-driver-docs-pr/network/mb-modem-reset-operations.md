---
title: MB 调制解调器重置操作
description: MB 调制解调器重置操作
ms.assetid: E33073B5-53D5-4F6F-85EC-5B46FDE9EA4D
keywords:
- MB 调制解调器重置，移动宽带调制解调器重置，移动宽带微型端口驱动程序调制解调器重置
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: d516123e8cfd70b1be0f82ce7f8dcd2e63922f69
ms.sourcegitcommit: 74a8dc9ef1da03857dec5cab8d304e2869ba54a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90759780"
---
# <a name="mb-modem-reset-operations"></a>MB 调制解调器重置操作

本部分定义 MBIM CID 命令和数据结构，以及用于重置移动 (宽带中的调制解调器) 设备的 NDIS OID 命令和数据结构。 在 Windows 10 版本1709及更高版本中提供这些命令和数据结构。

## <a name="mbim_cid_ms_device_reset"></a>MBIM_CID_MS_DEVICE_RESET

主机将 MBIM_CID_MS_DEVICE_RESET 发送到 MBIM 函数以重置调制解调器设备。

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft 基本 IP 连接扩展插件 | UUID_BASIC_CONNECT_EXTENSIONS | 3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf |

| CID | 命令代码 | Set | 查询 | 通知 |
| --- | --- | --- | --- | --- |
| MBIM_CID_MS_DEVICE_RESET | 10 | Y | N | N |

### <a name="parameters"></a>参数

|  类型 | Set | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 空 | 不适用 | 不适用 |
| 响应 | 空 | 不适用 | 不适用 |

### <a name="query"></a>查询

不适用。

### <a name="set"></a>Set

InformationBuffer 应为 NULL，而 *InformationBufferLength* 应为零。

### <a name="response"></a>响应

InformationBuffer 应为 NULL，而 *InformationBufferLength* 应为零。

### <a name="notification"></a>通知

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用。 重置完成后，状态将作为对集操作的异步响应返回。

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 操作成功。 |
| MBIM_STATUS_BUSY | 设备处于繁忙状态。 |
| MBIM_STATUS_FAILURE | 此操作失败。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 设备不支持此操作。 |

## <a name="oid_wwan_device_reset"></a>OID_WWAN_DEVICE_RESET

[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)MBIM_CID_MS_DEVICE_RESET 的 NDIS 等效项。
