---
title: MB NITZ 支持
description: MB NITZ 支持
ms.assetid: 94FE0380-C5EA-49F7-A649-0524C27F1A35
keywords:
- MB NITZ 支持，Mobile 宽带 NITZ 支持
ms.date: 03/13/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9dd754e5dd15d2af8739d7c54957fdd5adbe8507
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557732"
---
# <a name="mb-nitz-support"></a>MB NITZ 支持

## <a name="overview"></a>概述

从 Windows 10 版本1903开始，Windows 支持移动宽带（MBB）设备的 OS 级别的网络标识和时区（NITZ）。 在以前版本的 Windows 中，操作系统级别的唯一可用网络时间是网络时间协议（NTP），尽管所有3GPP 兼容的调制解调器都支持通过调制解调器级别的 NITZ。 使用 NITZ 支持，Windows 可以从调制解调器接收未经请求的 NITZ 通知并发布必要的事件，以通知用户 NITZ 时间戳。

对于 MBIM 函数，不需要执行其他 NITZ 相关的设置和配置。 只要通过蜂窝持有者建立数据连接，调制解调器就可以在收到网络的 NITZ 时间戳时随时通知操作系统。 根据移动运营商在3GPP 规范中定义的步调和计划，调制解调器可以从网络基础结构接收 NITZ 通知。 NITZ 通知是主动的。 收到 NITZ 通知后，操作系统将发布 NITZ 数据可用的通知。

## <a name="ndis-interface-extension"></a>NDIS 接口扩展

为支持 NITZ，定义了以下 OID。

- [OID_WWAN_NITZ](oid-wwan-nitz.md)

## <a name="mbim-service-and-cid-values"></a>MBIM 服务和 CID 值

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft 基本 IP 连接扩展插件 | UUID_VOICEEXTENSIONS | 8d8b9eba-37be-449b-8f1e-61cb034a702e |

下表为每个 CID 指定了 UUID 和命令代码，以及 CID 是否支持设置、查询或事件（通知）请求。 有关其参数、数据结构和通知的详细信息，请参阅本主题中的每个 CID 的各个部分。 

| CID | UUID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_NITZ | UUID_VOICEEXTENSIONS | 10 | N | Y | 是 |

## <a name="mbim_cid_nitz"></a>MBIM_CID_NITZ

### <a name="parameters"></a>参数

| Operation | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | 不适用 | 不适用 |
| 响应 | 不适用 | MBIM_NITZ_INFO | MBIM_NITZ_INFO |

### <a name="query"></a>查询

查询当前网络时间。 不使用 MBIM_COMMAND_MSG 的 InformationBuffer。 以下 MBIM_NITZ_INFO 结构在 MBIM_COMMAND_DONE 的 InformationBuffer 中使用。

#### <a name="mbim_nitz_info"></a>MBIM_NITZ_INFO

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 年份 | UINT32 | 整数形式的年份。 例如， **2014**。 |
| 4 | 4 | 月 | UINT32 | 月份（1-12），其中一月 = = 1。 |
| 8 | 4 | 天 | UINT32 | 每月的某一天，（1. 31）。 |
| 12 | 4 | Hour | UINT32 | 小时，（0到23）。 |
| 16 | 4 | Minute | UINT32 | 分钟（0到59）。 |
| 20 | 4 | Second | UINT32 | 第二个，（0）。 |
| 24 | 4 | TimeZoneOffsetMinutes | UINT32 | UTC 的时区偏移量（分钟）。 此值包括夏令时的当前状态的任何调整。 当时区信息不可用时，此值应设置为0xFFFFFFFF。 |
| 28 | 4 | DaylightSavingTimeOffsetMinutes | UINT32 | 夏令时的偏移量，以分钟为单位。 当夏令时不可用时，此值应设置为0xFFFFFFFF。 |
| 32 | 4 | Dataclasses.dll | UINT32 | 此网络支持的数据类。 如果此信息不可用，则应将此字段设置为 MBIMDataClassNone。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 中的 InformationBuffer 包含 MBIM_NITZ_INFO 的结构。

### <a name="unsolicited-events"></a>未经请求的事件

此未经许可事件提供当前网络时间和时区信息。

### <a name="status-codes"></a>状态代码

此 CID 仅使用[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的9.4.5 部分中定义的通用状态代码。
