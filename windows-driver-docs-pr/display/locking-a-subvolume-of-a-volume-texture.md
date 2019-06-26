---
title: 锁定体积纹理的子体积
description: 锁定体积纹理的子体积
ms.assetid: fff7b9c6-5f83-4691-9e44-99e45897ae3a
keywords:
- 纹理 WDK DirectX 8.0
- DirectX 8.0 发行说明 WDK Windows 2000 显示，体积纹理
- 体积纹理 WDK DirectX 8.0
- 子宗卷锁定 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d8f79b87df37573d47ec63d4f8b246b6f7f9911
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360899"
---
# <a name="locking-a-subvolume-of-a-volume-texture"></a>锁定体积纹理的子体积


## <span id="ddk_locking_a_subvolume_of_a_volume_texture_gg"></span><span id="DDK_LOCKING_A_SUBVOLUME_OF_A_VOLUME_TEXTURE_GG"></span>


DirectX 8.1 引入了一项新功能，可让锁定只是子宗卷的卷纹理的驱动程序。 当驱动程序的[ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)调用函数，该驱动程序可以通过锁定只是子宗卷而不是整个卷纹理提高系统性能。

若要指示此功能的支持，该驱动程序必须设置 D3DDEVCAPS\_SUBVOLUMELOCK 位**DevCaps** D3DCAPS8 结构中的成员。 该驱动程序在响应中返回 D3DCAPS8 结构**GetDriverInfo2**查询中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

确定支持此功能后，该驱动程序可以接收*DdLock*调用 DDLOCK\_HASVOLUMETEXTUREBOXRECT 中的设置位**dwFlags**成员传递 DD\_LOCKDATA 结构。 此位告知驱动程序可以锁定指定子宗卷纹理。 然后，驱动程序必须获取从锁定子宗卷的前端和后端坐标**左**并**右**RECTL 结构中指定的成员**rArea**DD 成员\_LOCKDATA。 驱动程序将获取从更高的 16 位的前端和后端坐标**左**并**右**成员分别。

锁定子宗卷的左侧和右侧坐标约束为较低的 16 位**左**并**右**成员。 驱动程序使用**顶部**并**底部**RECTL 的成员结构**rArea**不变，以指定锁定子宗卷的顶部和底部坐标。 这样一来， **rArea**成员能够有效地提供三个坐标集来指定锁定子宗卷。 RECTL 结构是 Microsoft Windows SDK 文档中所述。

下面的代码演示如何获取前端和后坐标：

```cpp
"real" left = rArea.left && 0xFFFF;
"real" right = rArea.right && 0xFFFF;
front = rArea.left >> 16;
back = rArea.right >> 16;
```

在 Windows Me 和 Windows XP 和更高版本上提供了此功能。 此外在 Windows 2000 和 Windows 98 操作系统版本中，将其上安装的 DirectX 8.1 运行时提供了此功能。

 

 





