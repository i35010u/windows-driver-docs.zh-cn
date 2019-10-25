---
title: 了解具有重复卷名称的卷枚举
description: 了解具有重复卷名称的卷枚举
ms.assetid: c05982dc-4124-4f9a-93b8-0e56ac296d1b
keywords:
- 卷 WDK 文件系统，名称重复
- 卷 WDK 文件系统，枚举
- 筛选器管理器 WDK 文件系统微筛选器，卷
- 重复卷名称 WDK 文件系统
- 枚举卷 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3def983b51fb587531dec2b0d0fb20c2a89f6a1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840947"
---
# <a name="understanding-volume-enumerations-with-duplicate-volume-names"></a>了解具有重复卷名称的卷枚举


枚举卷时，重复的卷名将出现在生成的卷信息列表中。

为了帮助了解这种情况的原因，请考虑以下方案：卷枚举例程[**FltEnumerateVolumeInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumeinformation)用于枚举所有系统卷。 这会生成一个缓冲区，其中包含卷信息结构-一个用于筛选器管理器识别的每个卷。 在此缓冲区中，每个卷信息结构可以是[**筛选器\_卷\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_basic_information)或[**筛选器\_卷\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_standard_information)，但不能同时为两者。

给定此卷信息结构列表，多个列表元素可以包含相同的卷名称。 也就是说，两个或多个列表元素的**FilterVolumeName**成员可能相同。 这是可能的，因为所有筛选器管理器枚举例程（如[**FltEnumerateVolumes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumes)）都枚举了一些卷，其中包括那些已卸除但尚未关闭的卷（因为打开的文件仍然存在于卷上）。 因此，当卷被卸载时，其名称可以在卷信息列表中多次显示-一次适用于其当前装载状态，在最简单的情况下为一次已卸载但未被破坏的状态。

如果卷信息列表中出现重复的卷名称，则上述说明将对每组相同的名称进行说明。 但是，可以使用以下过程来确认上述方案：

-   如果使用筛选器类型的结构填充列表\_卷\_标准\_信息，则标识**FilterVolumeName**成员相等的一组结构。 如果此组中的一个或多个结构具有 FLTFL\_的 .VSI\_在其**标志**成员中\_卷标志分离，则与该组关联的卷处于已卸除但未解除锁定状态。 这会确认存在重复卷名称的原因。 对于所有此类剩余组，请重复此过程（如果适用）。

-   如果列表中填充了类型为 FILTER 的结构\_卷\_基本\_信息，请将此列表转换为其等效的筛选器\_卷\_标准\_信息结构窗体，并像以前一样项目符号点。

**请注意**   筛选器\_卷\_标准\_信息结构仅适用于 Windows Vista。

 

此主题影响的例程和结构包括：

[**筛选\_卷\_基本\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_basic_information)

[**筛选\_卷\_标准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltuserstructures/ns-fltuserstructures-_filter_volume_standard_information)

[**FilterVolumeFindFirst**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindfirst)

[**FilterVolumeFindNext**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filtervolumefindnext)

[**FltEnumerateVolumeInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumeinformation)

[**FltEnumerateVolumes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenumeratevolumes)

[**FltGetVolumeInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumeinformation)

 

 




