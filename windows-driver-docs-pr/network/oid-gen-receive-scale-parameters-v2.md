---
title: OID_GEN_RECEIVE_SCALE_PARAMETERS_V2
description: 本主题介绍 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2
ms.assetid: 3897A898-2B00-45DF-AC05-7EC719EB7353
keywords: OID_GEN_RECEIVE_SCALE_PARAMETERS_V2, OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 RSSv2
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 687db15ca59a2480ba2cf2a0a100599b3552b549
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364199"
---
[!include[RSSv2 Beta Prerelease](../rssv2-beta-prerelease.md)]

# <a name="oidgenreceivescaleparametersv2"></a>OID_GEN_RECEIVE_SCALE_PARAMETERS_V2

向发送 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 OID [RSSv2](receive-side-scaling-version-2-rssv2-.md)-支持的微型端口驱动程序设置的间接寻址表，缩放实体的运行时参数。 替换 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)从 RSSv1 OID 和对 NDIS Light 权重筛选器 (LWFs) NDIS 6.80 之前不可见。 此 OID 是正则 OID，可以作为查询或一组请求发出。 在 IRQL 发出 = = passive_level 调用。 它可以针对给定的 VPort，当*NDIS_OID_REQUEST_FLAGS_VPORT_ID_VALID* NIC 开关创建时设置标志。 否则，它面向在本机 RSS 的情况下的物理 NIC。

为查询，NDIS 和基础驱动程序可用于 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 查询 NIC 的 RSS 参数 返回 NDIS [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://msdn.microsoft.com/library/windows/hardware/96EAB6EE-BF9A-46AD-8DED-5D9BD2B6F219)结构，它定义当前的 RSS 参数。

作为一组此 OID 的用途是执行以下操作：

- 初始配置缩放实体 （在本机 RSS 模式下的微型端口适配器或 VPort VMQ 模式下的）。
- 启用或禁用 RSS。
- 在 RSS 模式下，执行非计时关键的管理功能，例如更改哈希键、 哈希类型和哈希函数、 数目的队列或缩放的实体的间接寻址表条目数。

## <a name="remarks"></a>备注

启用 RSS，并设置 RSS 参数可以在一个步骤中执行... 上层启用了 RSS 使用此 OID 缩放实体的初始状态后，按如下所示：

- 主处理器变得*处于非活动状态*。
- 默认处理器变得*active*。
- 成为所有 Ite *active*。
- 微型端口驱动程序启动 RSS 哈希，设置为相应 OOB 对于所有的数据包，或将定向到由间接表项或默认处理器参数指定的处理器的数据包的计算。

启用了 RSS 后，为上层颁发[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID Ite 移动到不同的处理器。 在 RSSv2， **DefaultQueue**并**PrimaryProcessor**也会一起移动到不同的处理器使用 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES。

在禁用 RSS 的过程中，为上层将指向所有 Ite 主处理器之前调用此 OID 以禁用 RSS。 此点之后，接收流量应以主处理器为目标。 但是，微型端口驱动程序不应期望 VPort 删除之前禁用 RSS。 为上层可以接收筛选器设置上 VPort 为零，从而确保不接收流量流经 VPort，然后继续 VPort 删除但不能禁用 RSS。

为上层可以确保重要的固定条件不会违反之前执行管理功能。 例如：

- 在更改之前的队列的数量，较高层可确保间接表不引用不是为 VPort 配置更多的处理器。
在更改之前的 VMMQ 限制适配器的间接寻址表条目数，为上层可以确保间接表的内容规范化为 2 的幂。

### <a name="error-conditions-and-status-codes"></a>错误情况和状态代码

发生错误时，此 OID 返回下面的状态代码：

| 状态代码 | 错误条件 |
| --- | --- |
| NDIS_STATUS_INVALID_LENGTH | OID 的格式不正确。 |
| NDIS_STATUS_NO_QUEUES | 当启用了 RSS，但当前的间接寻址表引用了新的队列数比多个处理器正在更改的队列数。 |
| NDIS_STATUS_INVALID_DATA | <ul><li>间接表的大小，正在缩小，但不包含电源的两个重复模式。</li><li>RSS 在状态转换 (到*上*或*关闭*)，从的控制参数，有一个处理器*active*不属于适配器的 RSS 处理器组。 请注意，*处于非活动状态*控制参数是只跟踪写入到处理器并不会强制执行。 该参数成为 RSS 状态转换期间发生强制*active*。</li></ul> |
| NDIS_STATUS_INVALID_PARAMETER | 其他字段，在标头或 OID 本身中的包含无效值。 |

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

- [接收方缩放版本 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://msdn.microsoft.com/library/windows/hardware/96EAB6EE-BF9A-46AD-8DED-5D9BD2B6F219)
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)

