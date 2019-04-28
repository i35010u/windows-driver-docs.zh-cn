---
title: MB 网络黑名单操作
description: MB 网络黑名单操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8b839edae59e50126b399cb0018573180281ba5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343292"
---
# <a name="mb-network-blacklist-operations"></a>MB 网络黑名单操作

设备可能需要注册到下各种方案，例如当插入特定的 SIM 卡，或如果设备不想注册到特定网络的网络。 若要解决这些情况下，Windows 10 版本 1703年添加调制解调器接口，以使 OS 配置 SIM 卡和网络提供商的阻止列表。

在任何时候，操作系统可以在调制解调器，若要指定 SIM 或向其设备不允许注册的网络中配置的 MCC/mnc 对。  该接口的灵活程度足以允许两个不同的列表，一个用于 SIM 提供程序，另一个网络提供商。  如果设备未尝试注册，因为特定 SIM 或网络提供商已列入黑名单，调制解调器必须报告注册状态为被拒绝。

## <a name="mb-interface-update-for-network-blacklist-operations"></a>有关网络方块列表操作 MB 界面更新

已创建新的 MBIM 命令以启用 OS 来查询和设置的 MCC 和 mnc 对与调制解调器不应尝试注册时匹配 SIM 卡或网络提供程序是设备上存在。 此命令，新的 MSFT 专有 CID 已定义为 MBIM_CID_MS_NETWORK_BLACKLIST。

服务名称 = **Basic 连接扩展**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID Value = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | 命令代码 | 最低 OS 版本 |
| --- | --- | --- |
| MBIM_CID_MS_NETWORK_BLACKLIST | 2 | Windows 10 版本 1703 |

## <a name="mbimcidmsnetworkblacklist"></a>MBIM_CID_MS_NETWORK_BLACKLIST

### <a name="description"></a>描述

企业、 用户或移动运营商可能指定 SIM 卡和网络的管理员不想要注册的调制解调器。 此命令用于为操作系统能够查询和设置的调制解调器上的阻止列表。 有两个阻止列表：

1.  SIM 卡黑名单 – SIM 卡的提供程序是方块列表的成员应不允许在任何网络上注册。
2.  网络提供程序黑名单 – 方块列表上的网络应不允许注册而不考虑哪些 SIM 卡是设备上存在。

调制解调器必须维护每个调制解调器这两个阻止列表和在 SIM 交换中保持原样，电源周期。 可以使用查询或一组访问这两个阻止列表在任何时候，而不考虑 SIM 状态。

为一组命令它应覆盖现有项列入黑名单，在使用 Set 命令的有效负载的调制解调器。

#### <a name="query"></a>查询

MBIM_MS_NETWORK_BLACKLIST_INFO InformationBuffer 中已完成的查询和设置消息返回。 对于查询，InformationBuffer 为 NULL。

#### <a name="set"></a>设置

对于集，InformationBuffer 包含 MBIM_MS_NETWORK_BLACKLIST_INFO。 在设置操作中，应到调制解调器提供 mnc / MCC 组合的列表。 当 SIM 卡 IMSI 匹配指定的 mnc 和 MCC 值时，调制解调器应取消注册，从网络和不应尝试重新注册之前插入新的 SIM 卡与 mnc / MCC 不匹配。

#### <a name="unsolicited-event"></a>未经请求的事件

如果任何方块列表状态已更改从启动以不启动，应未经请求的事件，反之亦然;例如，如果 SIM 将插入的提供程序与 SIM 提供程序方块列表匹配。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_MS_NETWORK_BLACKLIST_INFO | 不适用 | 不适用 |
| 响应 | MBIM_MS_NETWORK_BLACKLIST_INFO | MBIM_MS_NETWORK_BLACKLIST_INFO | MBIM_MS_NETWORK_BLACKLIST_INFO |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询

InformationBuffer 应为 NULL，并且将 InformationBufferLength 应该为零。

#### <a name="set"></a>设置

应在 InformationBuffer 中使用以下 MBIM_MS_NETWORK_BLACKLIST_INFO 结构。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | BlacklistState | MBIM_MS_NETWORK_BLACKLIST_STATE | 指示是否满足的任何方块列表条件是该调制解调器未注册到网络中的结果。 有关详细信息，请参阅 MBIM_MS_NETWORK_BLACKLIST_STATE 表。 |
| 4 | 4 | ElementCount (EC) | UINT32 | 按照中 DataBuffer MBIM_MS_NETWORK_BLACKLIST_PROVIDER 计数结构。 |
| 8 | 8 * EC | BlacklistProviderRefList | OL_PAIR_LIST | 该对的第一个元素是一个 4 字节偏移量，从一开始 （偏移量为 0） 的此 MBIM_MS_NETWORK_BLACKLIST_INFO 结构，计算到 MBIM_MS_NETWORK_BLACKLIST_PROVIDER 结构。 有关详细信息，请参阅 MBIM_MS_NETWORK_BLACKLIST_PROVIDER 表。  该对的第二个元素是指针的指向相应 MBIM_MS_NETWORK_BLACKLIST_PROVIDER 结构的 4 字节大小。 |
| 8 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_NETWORK_BLACKLIST_PROVIDER 结构的数组。 |

前面的表中使用以下数据结构。

MBIM_MS_NETWORK_BLACKLIST_STATE 描述了可能的状态的两个不同的阻止列表。

| 在任务栏的搜索框中键入 | 掩码 | 描述 |
| --- | --- | --- |
| MbimMsNetworkBlacklistStateNotActuated | 0h | 不满足这两个方块列表条件。 |
| MbimMsNetworkBlacklistSIMProviderActuated | 1h | 为其提供程序 ID 匹配 SIM 提供程序 id 方块列表插入的 SIM 已被列入黑名单 |
| MbimMsNetworkBlacklistNetworkProviderActuated | 2h | 由于其提供程序 Id 是为网络提供程序 id。 方块列表中的所有可用网络都已列入黑名单 |

MBIM_MS_NETWORK_BLACKLIST_PROVIDER 指定方块列表的提供程序。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MCC | UINT32 | 指定 3GPP，MCC 是 IMSI 的一部分，它指定提供程序的国家/地区。 |
| 4 | 4 | MNC | UINT32 | 指定 3GPP，mnc 是 IMSI 的一部分，它指定提供程序的网络。 |
| 8 | 4 | NetworkBlacklistType | MBIM_MS_NETWORK_BLACKLIST_TYPE | 指定为其使用的方块的 MCC/mnc 对列表的类型。 有关详细信息，请参阅 MBIM_MS_NETWORK_BLACKLIST_TYPE 表。 |

MBIM_MS_NETWORK_BLACKLIST_TYPE 使用上述数据结构。 它指定将使用这两个阻止列表。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | ---- |
| MbimMsNetworkBlacklistTypeSIM | 0 | MCC/mnc 对用于 SIM 提供程序方块列表。 |
| MbimMsNetworkBlacklistTypeNetwork | 1 | MCC/mnc 对用于网络提供程序方块列表。 |

#### <a name="response"></a>响应

有关详细信息，请参阅 MBIM_MS_NETWORK_BLACKLIST_INFO 表。

### <a name="status-codes"></a>状态代码

对于查询和设置的操作：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | 操作失败，因为设备无法检索预配的上下文。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持该操作。 |

对于集合运算：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_WRITE_FAILURE | 操作失败，因为在更新请求未成功。 |
