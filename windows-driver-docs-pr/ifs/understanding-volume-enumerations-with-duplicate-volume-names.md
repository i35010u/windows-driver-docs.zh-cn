---
title: 了解具有重复卷名称的卷枚举
description: 了解具有重复卷名称的卷枚举
ms.assetid: c05982dc-4124-4f9a-93b8-0e56ac296d1b
keywords:
- WDK 卷文件系统，重复的名称
- 文件系统中，卷 WDK 枚举
- 筛选器管理器 WDK 文件系统微筛选器卷
- 重复的卷名称 WDK 文件系统
- 枚举卷 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a60af89126e6cce160d1149a6b168f0ffaea8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350031"
---
# <a name="understanding-volume-enumerations-with-duplicate-volume-names"></a>了解具有重复卷名称的卷枚举


在枚举卷，就可以重复的卷名称显示在生成的卷信息列表中。

为了帮助您了解此问题，请考虑以下方案： 卷枚举例程[ **FltEnumerateVolumeInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff542091)用于枚举所有的系统卷。 这会导致卷信息结构的一个已知的筛选器管理器的每个卷用于填充一个缓冲区。 在此缓冲区中的每个卷的信息结构可以是类型[**筛选器\_卷\_BASIC\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff541631)或[ **筛选器\_卷\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff541647)，但不可同时使用两者。

有了此列表的卷信息结构，就可以为多个列表元素以包含相同的卷名称。 即**FilterVolumeName**两个或多个列表元素的成员可以是完全相同。 这可能是因为所有筛选器管理器枚举例程，如[ **FltEnumerateVolumes**](https://msdn.microsoft.com/library/windows/hardware/ff542092)，枚举卷包括那些已卸载，但尚未数据被破坏列表 (由于打开文件的这一事实仍存在于一个卷）。 因此，卷将成为卸除时，其名称可以出现不止一次在卷的信息列表中的一次其当前已装载的状态和为其前一次卸除但非数据被破坏下状态，最简单的情况。

如果在卷的信息列表中出现重复的卷名称，是通过上面的说明解释每个组相同的名称。 但是，就可以通过使用以下过程来确认上述情况中：

-   如果列表中填充了类型筛选器的结构\_卷\_标准\_信息，标识结构的一组其**FilterVolumeName**成员是否相等。 如果一个或多个此组中的结构具有 FLTFL\_VSI\_DETACHED\_卷标志中设置其**标志**成员与组相关联的卷已在已卸载，但非数据被破坏列表状态。 这会确认为什么存在重复的卷名称。 如果适用，请重复此过程的剩余组所有此类。

-   如果列表中填充了类型筛选器的结构\_卷\_BASIC\_信息，将此列表转换为其等效的筛选器\_卷\_标准\_信息结构，窗体，然后继续如以前的项目符号点中所示。

**请注意**  筛选器\_卷\_标准\_信息结构是仅从 Windows Vista 开始提供。

 

例程和结构受本主题包括：

[**筛选器\_卷\_BASIC\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff541631)

[**筛选器\_卷\_标准\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff541647)

[**FilterVolumeFindFirst**](https://msdn.microsoft.com/library/windows/hardware/ff541525)

[**FilterVolumeFindNext**](https://msdn.microsoft.com/library/windows/hardware/ff541530)

[**FltEnumerateVolumeInformation**](https://msdn.microsoft.com/library/windows/hardware/ff542091)

[**FltEnumerateVolumes**](https://msdn.microsoft.com/library/windows/hardware/ff542092)

[**FltGetVolumeInformation**](https://msdn.microsoft.com/library/windows/hardware/ff543238)

 

 




