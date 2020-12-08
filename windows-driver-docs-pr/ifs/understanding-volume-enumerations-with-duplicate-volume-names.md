---
title: 了解具有重复卷名称的卷枚举
description: 了解具有重复卷名称的卷枚举
keywords:
- 卷 WDK 文件系统，名称重复
- 卷 WDK 文件系统，枚举
- 筛选器管理器 WDK 文件系统微筛选器，卷
- 重复卷名称 WDK 文件系统
- 枚举卷 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f0fef9409aae3dd88461ec45866cef55d1ebdb7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841131"
---
# <a name="understanding-volume-enumerations-with-duplicate-volume-names"></a>了解具有重复卷名称的卷枚举


枚举卷时，重复的卷名将出现在生成的卷信息列表中。

为了帮助了解这种情况的原因，请考虑以下方案：卷枚举例程 [**FltEnumerateVolumeInformation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumeinformation) 用于枚举所有系统卷。 这会生成一个缓冲区，其中包含卷信息结构-一个用于筛选器管理器识别的每个卷。 在此缓冲区中，每个卷信息结构可以是 [**筛选器 \_ 卷 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_basic_information) 或 [**筛选器 \_ 批量 \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_standard_information)，但不能同时为两者。

给定此卷信息结构列表，多个列表元素可以包含相同的卷名称。 也就是说，两个或多个列表元素的 **FilterVolumeName** 成员可能相同。 这是可能的，因为所有筛选器管理器枚举例程（如 [**FltEnumerateVolumes**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumes)）都枚举了卷，其中包括已卸除但尚未被 (的卷，因为打开的文件仍然存在于卷) 上。 因此，当卷被卸载时，其名称可以在卷信息列表中多次显示-一次适用于其当前装载状态，在最简单的情况下为一次已卸载但未被破坏的状态。

如果卷信息列表中出现重复的卷名称，则上述说明将对每组相同的名称进行说明。 但是，可以使用以下过程来确认上述方案：

-   如果列表是使用筛选器批量标准信息类型的结构填充的 \_ \_ ，则 \_ 标识其 **FilterVolumeName** 成员相等的一组结构。 如果此组中的一个或多个结构在 \_ \_ \_ 其 **Flags** 成员中设置了 FLTFL 的 .vsi 分离卷标志，则与该组关联的卷处于已卸除但未解除锁定状态。 这会确认存在重复卷名称的原因。 对于所有此类剩余组，请重复此过程（如果适用）。

-   如果列表中填充了类型为 "筛选器 \_ \_ " "基本信息" 的结构 \_ ，则将此列表转换为其等效的筛选器 \_ 批量 \_ 标准 \_ 信息结构窗体，然后在上一项目符号点中继续。

**注意**  \_ \_ \_ 仅从 Windows VISTA 开始使用筛选器卷标准信息结构。

 

此主题影响的例程和结构包括：

[**筛选 \_ 卷 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_basic_information)

[**筛选 \_ 批量 \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_standard_information)

[**FilterVolumeFindFirst**](/windows/win32/api/fltuser/nf-fltuser-filtervolumefindfirst)

[**FilterVolumeFindNext**](/windows/win32/api/fltuser/nf-fltuser-filtervolumefindnext)

[**FltEnumerateVolumeInformation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumeinformation)

[**FltEnumerateVolumes**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumes)

[**FltGetVolumeInformation**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumeinformation)

 

