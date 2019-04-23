---
title: MB NITZ 支持
description: MB NITZ 支持
ms.assetid: 94FE0380-C5EA-49F7-A649-0524C27F1A35
keywords:
- MB NITZ 支持，移动宽带 NITZ 支持
ms.date: 03/13/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 09cfce70987bd3e19955449250dc88b793a1c7a2
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905337"
---
# <a name="mb-nitz-support"></a>MB NITZ 支持

## <a name="overview"></a>概述

从 Windows 10，版本 1903，Windows 支持网络标识和时区 (NITZ) 在 OS 级别的移动宽带 (MBB) 设备。 在以前版本的 Windows 中，只有网络时间可用在 OS 级别为网络时间协议 (NTP) 即使 NITZ 已在调制解调器级别支持的所有符合 3GPP 的调制解调器。 借助 NITZ 支持，Windows 就能够从调制解调器接收未经请求的 NITZ 通知并发布必需的事件通知使用者的 NITZ 时间戳。

对于 MBIM 函数，无需额外 NITZ 相关安装程序并预配不需要。 只要通过移动电话的持有者建立数据连接，调制解调器可以的随时从网络接收 NITZ 时间戳通知操作系统。 调制解调器可以接收来自基于移动运营商自己定义的频率和计划，3GPP 规范中的网络基础结构 NITZ 通知。 未经请求 NITZ 通知。 在收到 NITZ 通知，操作系统将发布 NITZ 数据是可用的通知。

## <a name="ndis-interface-extension"></a>NDIS 接口扩展

已定义的以下 OID，以支持 NITZ。

- [OID_WWAN_NITZ](oid-wwan-nitz.md)

## <a name="mbim-service-and-cid-values"></a>MBIM 服务和 CID 值

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft Basic IP 连接扩展 | UUID_VOICEEXTENSIONS | 8d8b9eba-37be-449b-8f1e-61cb034a702e |

下表指定 UUID 和每个 CID 命令代码，以及是否 CID 支持设置，请查询，或事件 （通知） 请求。 请参阅在本主题中详细了解其参数、 数据结构和通知的每个 CID 的各个部分。 

| CID | UUID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_NITZ | UUID_VOICEEXTENSIONS | 10 | N | Y | Y |

## <a name="mbimcidnitz"></a>MBIM_CID_NITZ

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | 不适用 | 不适用 |
| 响应 | 不适用 | MBIM_NITZ_INFO | MBIM_NITZ_INFO |

### <a name="query"></a>查询

查询当前的网络时间。 不使用 MBIM_COMMAND_MSG InformationBuffer。 以下 MBIM_NITZ_INFO 结构 MBIM_COMMAND_DONE InformationBuffer 中使用。

#### <a name="mbimnitzinfo"></a>MBIM_NITZ_INFO

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 年 | UINT32 | 一个整数，表示的年份。 例如， **2014年**。 |
| 4 | 4 | 月 | UINT32 | 月 (1..12)，其中年 1 月 = = 1。 |
| 8 | 4 | Day | UINT32 | 月 (1..31) 的某一天。 |
| 12 | 4 | Hour | UINT32 | 小时 (0..23)。 |
| 16 | 4 | Minute | UINT32 | 分钟 （） (0..59)。 |
| 20 | 4 | 第二个 | UINT32 | 第二个，(0..59)。 |
| 24 | 4 | TimeZoneOffsetMinutes | UINT32 | 时区偏移量，以分钟为单位，从 UTC。 此值包括夏时制的当前状态的任何调整。 时区信息不可用时，此值应设置为 0xFFFFFFFF。 |
| 28 | 4 | DaylightSavingTimeOffsetMinutes | UINT32 | 夏时制，以分钟为单位的偏移量。 夏时制不可用时，此值应设置为 0xFFFFFFFF。 |
| 32 | 4 | DataClasses | UINT32 | 此网络支持的数据类。 如果此信息不可用，则此字段应设置为 MBIMDataClassNone。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

在 MBIM_COMMAND_DONE InformationBuffer 包含 MBIM_NITZ_INFO 结构。

### <a name="unsolicited-events"></a>未经请求的事件

此未经请求的事件提供了新的网络时间和时区信息。

### <a name="status-codes"></a>状态代码

此 CID 仅使用 9.4.5 节中定义的泛型状态代码[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。
