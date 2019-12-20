---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS_V2
description: 本主题介绍 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2
ms.assetid: 3897A898-2B00-45DF-AC05-7EC719EB7353
keywords: OID_GEN_RECEIVE_SCALE_PARAMETERS_V2，OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 RSSv2
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: b11da5dced57bb7240b713eeb7d79cb27a6a7ddf
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210859"
---
[!include[RSSv2 Beta Prerelease](../includes/rssv2-beta-prerelease.md)]

# <a name="oid_gen_receive_scale_parameters_v2"></a>OID_GEN_RECEIVE_SCALE_PARAMETERS_V2

OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 OID 发送到支持[RSSv2](receive-side-scaling-version-2-rssv2-.md)的微型端口驱动程序，以设置缩放实体的运行时参数，而不是间接表。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 替换 RSSv1 中的[OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md) OID，在 ndis 6.80 之前不会对 Ndis 轻型筛选器（LWFs）显示。 此 OID 为常规 OID，可以作为查询或设置请求发出。 它以 IRQL = = PASSIVE_LEVEL 颁发。 如果在 NIC 交换机创建时设置了*NDIS_OID_REQUEST_FLAGS_VPORT_ID_VALID*标志，则它可以针对给定的 VPort。 否则，在本机 RSS 案例中，它以物理 NIC 为目标。

作为查询，NDIS 和过量驱动程序可以使用 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 来查询 NIC 的 RSS 参数。 NDIS 返回定义当前 RSS 参数的[NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)结构。

作为一个集，此 OID 的用途是执行以下操作：

- 最初配置缩放实体（本机 RSS 模式下的微型端口适配器或 VMQ 模式下的 VPort）。
- 启用或禁用 RSS。
- 在 RSS 模式下，执行非计时关键管理功能，例如更改哈希键、哈希类型和哈希函数、队列数或缩放实体的间接表项的数目。

## <a name="remarks"></a>备注

启用 RSS 并设置 RSS 参数的步骤可以是一步。 在上层使用此 OID 启用 RSS 后，缩放实体的初始状态如下所示：

- 主处理器变为*非活动状态*。
- 默认处理器变为*活动状态*。
- 所有 ITEs 将变为*活动状态*。
- 微型端口驱动程序开始计算 RSS 哈希，为所有数据包设置相应的 OOB，并将数据包定向到由间接表条目或默认处理器参数指定的处理器。

启用 RSS 后，上层会发出[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID，将 ITEs 移动到不同的处理器。 在 RSSv2 中， **DefaultQueue**和**PrimaryProcessor**还会使用 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 移动到不同的处理器。

在禁用 RSS 的过程中，上层会将所有 ITEs 指向主处理器，然后再调用此 OID 以关闭 RSS。 此时，接收流量应以主处理器为目标。 但是，小型小型驱动程序不应期望在 VPort 删除之前禁用 RSS。 上层可以将 VPort 上的接收筛选器设置为零，从而确保没有接收流量流经 VPort，然后继续删除 VPort，而不会禁用 RSS。

上层将确保在执行管理功能之前不违反重要的固定条件。 例如：

- 在更改队列的数目之前，上层将确保间接寻址表不引用超过为 VPort 配置的处理器。
在更改 VMMQ 限制的适配器的间接表条目数之前，上层将确保间接寻址表的内容已规范化为2的幂。

### <a name="error-conditions-and-status-codes"></a>错误情况和状态代码

当发生错误时，此 OID 返回以下状态代码：

| 状态代码 | 错误条件 |
| --- | --- |
| NDIS_STATUS_INVALID_LENGTH | OID 的格式不正确。 |
| NDIS_STATUS_NO_QUEUES | 启用 RSS 时，将更改队列数量，但当前的间接寻址表引用的处理器比新数量的队列多。 |
| NDIS_STATUS_INVALID_DATA | <ul><li>间接寻址表大小减小，但不包含两次幂的重复模式。</li><li>在 RSS 状态转换（到 *"打开" 或 "* *关闭*"）期间，将*处于活动*状态的方向盘参数的处理器不属于适配器的 RSS 处理器集。 请注意，*非活动*控制参数只跟踪对处理器的写入，不会强制执行。 当参数变为*活动*状态时，会在 RSS 状态转换期间发生强制执行。</li></ul> |
| NDIS_STATUS_INVALID_PARAMETER | 标头或 OID 本身中的其他字段包含无效的值。 |

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

- [接收方缩放版本2（RSSv2）](receive-side-scaling-version-2-rssv2-.md)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)

