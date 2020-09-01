---
title: MB 网络阻止列表操作
description: MB 网络阻止列表操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 510c2025d5246e6fe2f42a6e3adc63d778eef5ba
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213933"
---
# <a name="mb-network-blacklist-operations"></a>MB 网络阻止列表操作

> [!IMPORTANT]
>
> ### <a name="bias-free-communication"></a>无偏差通信
>
> Microsoft 支持多样化的包容性环境。 本文包含对 word 黑名单的引用。 Microsoft 的[无偏差通信风格指南](/style-guide/bias-free-communication)将其视为排他性单词。 本文中使用的词是为了保持一致，因为它当前是软件中出现的单词。 如果软件更新后删除了该单词，则本文也将更新以保持一致。

在各种情况下，设备可能需要不注册到网络，例如插入特定 SIM 卡或设备不想注册到特定网络。 为了应对这些情况，Windows 10 1703 版正在添加调制解调器接口，以使操作系统能够为 SIM 卡和网络提供程序配置黑名单。

操作系统可以随时在调制解调器中配置 MCC/MNC 对，以指定不允许设备注册到的 SIM 或网络。  接口的灵活性足以允许两个不同的列表，一个用于 SIM 提供程序，另一个用于网络提供程序。  如果设备未尝试注册，因为特定 SIM 或网络提供程序被列入了黑名单，则调制解调器必须将注册状态报告为 "已拒绝"。

## <a name="mb-interface-update-for-network-blacklist-operations"></a>网络黑名单操作的 MB 接口更新

已创建一个新的 MBIM 命令，以使 OS 能够查询和设置在设备上存在匹配的 SIM 卡或网络提供程序时调制解调器不应尝试注册的 MCC 和 MNC 对。 对于此命令，已将新的 MSFT 专用 CID 定义为 MBIM_CID_MS_NETWORK_BLACKLIST。

服务名称 = **基本连接扩展**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 值 = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_MS_NETWORK_BLACKLIST | 2 | Windows 10 版本 1703 |

## <a name="mbim_cid_ms_network_blacklist"></a>MBIM_CID_MS_NETWORK_BLACKLIST

### <a name="description"></a>说明

企业、用户或移动运营商可以指定 SIM 卡和网络，它们不需要调制解调器进行注册。 此命令用于 OS，以便能够在调制解调器上查询和设置黑名单。 有两个黑名单：

1.  SIM 卡黑名单–其提供商是黑名单成员的 SIM 卡不应允许在任何网络上注册。
2.  网络提供者黑名单–无论设备上有哪些 SIM 卡，都不允许黑名单上的网络注册。

调制解调器必须为每个调制解调器维护黑名单，并跨 SIM 交换和电源周期保持。 无论 SIM 状态如何，都可以通过 Query 或 Set 访问这两个黑名单。

对于 Set 命令，它应覆盖带有 Set 命令的有效负载的调制解调器中的现有黑名单。

#### <a name="query"></a>查询

从已完成的查询返回 MBIM_MS_NETWORK_BLACKLIST_INFO，并在 InformationBuffer 中设置消息。 对于 Query，InformationBuffer 为 NULL。

#### <a name="set"></a>设置

对于 Set，InformationBuffer 包含 MBIM_MS_NETWORK_BLACKLIST_INFO。 在设置操作中，应为调制解调器提供一个 MNC/MCC 组合列表。 如果 SIM 卡的 IMSI 与指定的 MNC 和 MCC 值匹配，则调制解调器应从网络取消注册，并且在插入与 MNC/MCC 不匹配的新 SIM 卡之前，不应尝试重新注册。

#### <a name="unsolicited-event"></a>主动事件

如果任何黑名单状态已从 "开始" 改为 "未开始" （反之亦然），则应为未经请求的事件。例如，如果插入的 SIM 与 SIM 提供程序黑名单匹配，则为。

### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_NETWORK_BLACKLIST_INFO | 不适用 | 不适用 |
| 响应 | MBIM_MS_NETWORK_BLACKLIST_INFO | MBIM_MS_NETWORK_BLACKLIST_INFO | MBIM_MS_NETWORK_BLACKLIST_INFO |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询

InformationBuffer 应为 NULL，而 InformationBufferLength 应为零。

#### <a name="set"></a>设置

以下 MBIM_MS_NETWORK_BLACKLIST_INFO 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | BlacklistState | MBIM_MS_NETWORK_BLACKLIST_STATE | 指示是否满足任何黑名单条件，导致调制解调器未向网络注册。 有关详细信息，请参阅 MBIM_MS_NETWORK_BLACKLIST_STATE 表。 |
| 4 | 4 | Elementcount 多于 (EC)  | UINT32 | DataBuffer 中后面的 MBIM_MS_NETWORK_BLACKLIST_PROVIDER 结构的计数。 |
| 8 | 8 * EC | BlacklistProviderRefList | OL_PAIR_LIST | 该对的第一个元素为4字节偏移量，从该 MBIM_MS_NETWORK_BLACKLIST_INFO 结构的开始 (偏移量 0) 计算到 MBIM_MS_NETWORK_BLACKLIST_PROVIDER 结构。 有关详细信息，请参阅 MBIM_MS_NETWORK_BLACKLIST_PROVIDER 表。  对的第二个元素是指向相应 MBIM_MS_NETWORK_BLACKLIST_PROVIDER 结构的指针的大小为4字节。 |
| 8 + (8 * EC)  |  | DataBuffer | DATABUFFER | MBIM_MS_NETWORK_BLACKLIST_PROVIDER 结构的数组。 |

前面的表中使用了以下数据结构。

MBIM_MS_NETWORK_BLACKLIST_STATE 描述两个不同黑名单的可能状态。

| 类型 | Mask | 说明 |
| --- | --- | --- |
| MbimMsNetworkBlacklistStateNotActuated | 0h | 不满足这两个黑名单条件。 |
| MbimMsNetworkBlacklistSIMProviderActuated | 1小时 | 插入的 SIM 被列入黑名单，因为其提供程序 ID 与 SIM 提供程序 ID 的黑名单匹配。 |
| MbimMsNetworkBlacklistNetworkProviderActuated | 下半年 | 可用网络被列入黑名单，因为其提供程序 Id 全部位于网络提供程序 ID 黑名单中。 |

MBIM_MS_NETWORK_BLACKLIST_PROVIDER 指定黑名单的提供者。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MCC | UINT32 | 如3GPP 所指定，MCC 是 IMSI 的一部分，它指定了提供商的国家/地区。 |
| 4 | 4 | MNC | UINT32 | 由3GPP 指定，MNC 是 IMSI 的一部分并指定提供程序的网络。 |
| 8 | 4 | NetworkBlacklistType | MBIM_MS_NETWORK_BLACKLIST_TYPE | 指定对 MCC/MNC 对使用哪种类型的黑名单。 有关详细信息，请参阅 MBIM_MS_NETWORK_BLACKLIST_TYPE 表。 |

MBIM_MS_NETWORK_BLACKLIST_TYPE 由前面的数据结构使用。 它指定将使用这两个黑名单中的哪一个。

| 类型 | 值 | 说明 |
| --- | --- | ---- |
| MbimMsNetworkBlacklistTypeSIM | 0 | MCC/MNC 对用于 SIM 提供程序黑名单。 |
| MbimMsNetworkBlacklistTypeNetwork | 1 | MCC/MNC 对用于网络提供者黑名单。 |

#### <a name="response"></a>响应

有关详细信息，请参阅 MBIM_MS_NETWORK_BLACKLIST_INFO 表。

### <a name="status-codes"></a>状态代码

对于查询和设置操作：

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | 操作失败，因为设备无法检索预配的上下文。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持此操作。 |

仅适用于集操作：

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_WRITE_FAILURE | 操作失败，因为更新请求不成功。 |