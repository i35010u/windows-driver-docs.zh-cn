---
title: 支持拉伸位图传送操作
description: 支持拉伸位图传送操作
ms.assetid: 1d279e56-41fd-4189-84d2-858e51db281d
keywords:
- blit 延伸操作 WDK DirectX 9.0
- 拉伸位块操作 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4269f3d0ed6899c4af7149c1f949c84692df79e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575796"
---
# <a name="supporting-stretch-blit-operations"></a>支持拉伸位图传送操作


## <span id="ddk_supporting_stretch_blit_operations_gg"></span><span id="DDK_SUPPORTING_STRETCH_BLIT_OPERATIONS_GG"></span>


驱动程序执行延伸位块的方式取决于其运行所在的平台。 为 Windows 98 / 我的平台，当驱动程序的[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)函数收到位块请求时，该驱动程序可以计算从中的剪辑矩形区域的扩展系数**rOrigDest**并**rOrigSrc**的成员[ **DD\_BLTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550474)结构并执行位块时纳入计算操作。

有关 DirectX 9.0 和更高版本在基于 NT 的操作系统，驱动程序可以计算，并接收 DDBLT 的位块请求时记录扩展系数\_扩展\_标志和 DDBLT\_扩展\_演示文稿\_STRETCHFACTOR 标记中的设置**dwFlags** DD 成员\_BLTDATA。 该驱动程序计算中的剪辑源和目标矩形区域的延伸因子**rSrc**并**bltFX**分别的 DD 成员\_与 DDBLTBLTDATA\_扩展\_演示文稿\_STRETCHFACTOR 集。 请注意，驱动程序必须从 DDBLTFX 结构中的以下成员获取未剪辑的目标矩形区域**bltFX**，并不使用中的信息**rDest**成员。

-   在结构中以下成员 DDCOLORKEY 的左侧和顶部坐标**ddckDestColorkey** DDBLTFX 的成员：
    -   从左侧坐标**dwColorSpaceLowValue** DDCOLORKEY 的成员。
    -   从上的边缘坐标**dwColorSpaceHighValue** DDCOLORKEY 的成员。
-   在结构中以下成员 DDCOLORKEY 的右侧和底部坐标**ddckSrcColorkey** DDBLTFX 的成员：
    -   从角坐标**dwColorSpaceLowValue** DDCOLORKEY 的成员。
    -   从下的边缘坐标**dwColorSpaceHighValue** DDCOLORKEY 的成员。

请注意，驱动程序会将这些坐标解释为有符号的整数，而不是 dword 值。 另请注意，驱动程序必须验证这些坐标之前计算扩展系数和编程的图形设备中的延伸因素形成的矩形。 有关 DDBLTFX 和 DDCOLORKEY 的详细信息，请参阅最新的 DirectDraw SDK 文档。

当驱动程序收到与 DDBLT blit\_扩展\_演示文稿\_STRETCHFACTOR 集，该驱动程序必须不使用未剪辑的矩形区域来进行任何实际的平面闪。

该驱动程序随后接收位块请求与 DDBLT\_演示文稿和 DDBLT\_最后一个\_演示文稿标记集、 驱动程序可以纳入位块操作中此记录扩展系数。 该驱动程序完成与 DDBLT 最后一位块后\_最后一个\_演示文稿设置标志，该驱动程序必须清除 stretch 身份记录以防止任何后续 blits 的干扰。 详细了解 DDBLT\_演示文稿和 DDBLT\_上次\_演示文稿标记，请参阅[演示文稿](presentation.md)。

由于扩展系数是浮点计算，并非所有图形设备可以都支持它。 因此，此类设备的驱动程序不需要计算和使用扩展系数。 但是，即使 stretch 因素计算是不受支持，DirectX 9.0 和更高版本上基于 NT 的操作系统的驱动程序必须仍确定是否存在 DDBLT\_扩展\_演示文稿\_STRETCHFACTOR 标志因为尝试在其中执行实际位块操作 DDBLT\_扩展\_演示文稿\_STRETCHFACTOR 标志设置会导致呈现损坏。

有关扩展的 blit 标志的详细信息，请参阅[扩展 Blt 标志](extended-blt-flags.md)。

 

 





