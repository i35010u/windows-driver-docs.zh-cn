---
title: 回顾旧式对齐方法
description: 回顾旧式对齐方法
ms.assetid: 4efc380f-6303-42e1-8651-c9d64498942a
keywords:
- 绘制扩展 WDK DirectDraw 图面上对齐
- DirectDraw 扩展图面上的对齐方式 WDK Windows 2000 显示
- WDK DirectDraw，扩展对齐方式的图面
- 扩展 WDK DirectDraw 图面上对齐
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8684bc1f207aafcd622f2397d29cede0c710ef50
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365625"
---
# <a name="review-of-the-older-alignment-method"></a>回顾旧式对齐方法


## <span id="ddk_review_of_the_older_alignment_method_gg"></span><span id="DDK_REVIEW_OF_THE_OLDER_ALIGNMENT_METHOD_GG"></span>


版本的 DirectX 5.0 之前的 DirectDraw 允许驱动程序来表示线性堆的间距的对齐要求。 出于本文的讨论，可以在三个步骤中看到使用 DirectDraw 通过这些对齐要求：

1.  创建在图面，并填写对齐**lPitch**成员基于驱动程序的全局对齐需求 (中返回[ **VIDEOMEMORYINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_videomemoryinfo)结构) 和面的**ddsCaps**成员。 之前的适当对齐需求的倍数增加此跨度。

2.  调用的驱动程序[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))回调中，如果定义。 该驱动程序可以修改**lPitch**由 Microsoft Windows 2000 及更高版本，将忽略值，但此更改。

3.  如果未处理的驱动程序调用，或请求分配，在图面为从一个驱动程序的堆分配显示内存。 需要采取的已分配的图面宽度是在步骤 1 中确定的对齐的音调，除非修改驱动程序，否则在第 2 步。

如果驱动程序实现[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))回调，它可以确信，具有传入的任何图面其**lPitch**成员设置为对齐的值。 用于向后兼容性，仍存在此行为。 第三步维护完全相同的行为，除非已经公开了驱动程序**GetHeapAlignment**入口点 (请参阅[ **DD\_GETHEAPALIGNMENTDATA** ](https://docs.microsoft.com/windows/desktop/api/dmemmgr/ns-dmemmgr-_dd_getheapalignmentdata)结构)。 当且仅当已定义的此入口点，以前计算**lPitch**对齐方式将被放弃，并且使用 GUID 报告的要求符合所有图面上的对齐方式\_GetHeapAlignment。 驱动程序可以保留其[ **VIDEOMEMORYINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_videomemoryinfo)结构的对齐要求，并希望在较旧的 DirectDraw 运行时上运行时相同的对齐方式行为。 已完全替换此对齐行为 for DirectX 5.0 和更高版本的 DirectDraw 运行时。 应注意的是，它公开**GetHeapAlignment**关闭此旧对齐过程对于所有堆，而不仅仅是那些用于哪个 GUID\_GetHeapAlignment 报告对齐要求。

 

 





