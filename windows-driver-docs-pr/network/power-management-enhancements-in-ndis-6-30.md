---
title: 在 NDIS 6.30 电源管理增强功能
ms.assetid: A3B64252-DD6C-4715-8D4B-8D8176BC585B
description: 引入了 NDIS 6.30 电源管理增强功能，以减少计算机的功率消耗
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e73c806ca55185eac4c4410cedfd1e443bd65ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556066"
---
# <a name="power-management-enhancements-in-ndis-630"></a>在 NDIS 6.30 电源管理增强功能


NDIS 6.20 包括电源管理的新功能和改进，可减少计算机的功率消耗。 NDIS 6.30 扩展 NDIS 6.20 电源管理支持具有以下功能，如中所述[电源管理 (NDIS 6.30)](power-management--ndis-6-30-.md):

### <a name="ndis-packet-coalescing"></a>NDIS 数据包合并

从 NDIS 6.30，网络适配器可以支持 NDIS 数据包合并。 此功能可以减少处理由于接收的随机广播或多播的数据包的主机系统上的开销和电源消耗。

有关详细信息，请参阅[NDIS 数据包合并](ndis-packet-coalescing.md)。

### <a name="ndis-selective-suspend"></a>NDIS 选择性挂起

从开始 NDIS 6.30，NDIS 选择性挂起接口允许通过转换到低功耗状态适配器挂起空闲的网络适配器的 NDIS。 这使系统来减少开销上 CPU 和网络适配器的电源。

有关详细信息，请参阅[NDIS 选择性挂起](ndis-selective-suspend.md)。

### <a name="ndis-wake-reason-status-indications"></a>NDIS 唤醒原因状态指示

从开始 NDIS 6.30，微型端口驱动程序发出 NDIS 唤醒原因状态指示 ([**NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)) 到通知 NDIS 和系统唤醒事件的原因有关的基础驱动程序。 如果网络适配器生成唤醒事件时，微型端口驱动程序会立即发出此 NDIS 状态指示系统恢复到全功率状态时。

**请注意**  支持 NDIS 唤醒原因状态指示是可选的移动宽带 (MB) 微型端口驱动程序。

 

有关详细信息，请参阅[NDIS 唤醒原因状态指示](ndis-wake-reason-status-indications.md)。

### <a name="ndis-no-pause-on-suspend"></a>NDIS 上的没有暂停挂起

从开始 NDIS 6.30，微型端口驱动程序可以指定属性标志 (**NDIS\_微型端口\_特性\_否\_暂停\_ON\_挂起**) 中[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)结构。 该驱动程序将指针传递到此结构中对其调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

如果微型端口设置**NDIS\_微型端口\_特性\_否\_暂停\_ON\_挂起**属性标志 NDIS 不会调用微型端口驱动程序的[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)函数的对象标识符 (OID) 的请求之前[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)颁发给该驱动程序。 当微型端口驱动程序处理 OID 请求时，它必须假设，它具有之前暂停转换到低功耗状态为准备微型端口适配器时。

有关详细信息，请参阅[ **NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)。

 

 





