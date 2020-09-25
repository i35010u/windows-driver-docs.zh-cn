---
title: NDIS 6.30 中的电源管理增强功能
ms.assetid: A3B64252-DD6C-4715-8D4B-8D8176BC585B
description: 介绍 NDIS 6.30 电源管理增强功能，以减少计算机能耗
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a535b910ba727777a2788fde0ab84b4f35e9f137
ms.sourcegitcommit: 29c2e6dd8a3de3c11822d990adf1edd774f8a136
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91230011"
---
# <a name="power-management-enhancements-in-ndis-630"></a>NDIS 6.30 中的电源管理增强


NDIS 6.20 包括电源管理的新功能和改进，以降低计算机的功耗。 NDIS 6.30 将 NDIS 6.20 电源管理支持扩展为以下功能，如 [电源管理 (NDIS 6.30) ](power-management--ndis-6-30-.md)中所述：

### <a name="ndis-packet-coalescing"></a>NDIS 数据包合并

从 NDIS 6.30 开始，网络适配器可支持 NDIS 数据包合并。 由于收到随机广播或多播数据包，此功能可减少主机系统上的处理开销和能耗。

有关详细信息，请参阅 [NDIS 数据包合并](ndis-packet-coalescing.md)。

### <a name="ndis-selective-suspend"></a>NDIS 选择性挂起

从 NDIS 6.30 开始，NDIS 选择性挂起接口允许 NDIS 通过将适配器转换为低功耗状态来挂起空闲网络适配器。 这使系统可以减少 CPU 和网络适配器的电源开销。

有关详细信息，请参阅 " [NDIS 选择性挂起](ndis-selective-suspend.md)"。

### <a name="ndis-wake-reason-status-indications"></a>NDIS 唤醒原因状态指示

从 NDIS 6.30 开始，微型端口驱动程序发出 NDIS 唤醒原因状态指示 ([**ndis \_ 状态 \_ PM \_ 唤醒 \_ 原因**](./ndis-status-pm-wake-reason.md)) 通知 ndis 和过量驱动程序有关系统唤醒事件的原因。 如果网络适配器生成唤醒事件，则当系统恢复到完全电源状态时，微型端口驱动程序会立即发出此 NDIS 状态指示。

**注意**   支持 NDIS 唤醒原因状态指示对于移动宽带 (MB) 微型端口驱动程序是可选的。

 

有关详细信息，请参阅 [NDIS 唤醒原因状态指示](overview-of-ndis-wake-reason-statue-indications.md)。

### <a name="ndis-no-pause-on-suspend"></a>挂起时不暂停 NDIS

从 NDIS 6.30 开始，微型端口驱动程序可以 (ndis 微型端口[** \_ \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构中的 " ** \_ \_ \_ \_ \_ \_ 挂起时暂停"**) 指定属性标志。 驱动程序在其对 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数的调用中传递指向此结构的指针。

如果微型端口将 **ndis \_ 微型端口属性设置为 " \_ \_ \_ \_ \_ 挂起时暂停"** 属性标志，ndis 不会调用微型端口驱动程序的 [*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause) 函数， (oid) 请求将 [oid \_ PNP 集的 \_ \_ 权限](./oid-pnp-set-power.md) 颁发给驱动程序。 当微型端口驱动程序处理 OID 请求时，它不能假定已在准备微型端口适配器时将其暂停，以便过渡到低功耗状态。

有关详细信息，请参阅 [**NDIS \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)。

 

