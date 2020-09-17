---
title: 锁定体积纹理的子体积
description: 锁定体积纹理的子体积
ms.assetid: fff7b9c6-5f83-4691-9e44-99e45897ae3a
keywords:
- 纹理 WDK DirectX 8。0
- DirectX 8.0 发行说明 WDK Windows 2000 显示，音量纹理
- 卷纹理 WDK DirectX 8。0
- subvolume 锁定 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 880a4e4c3cd7b288b0616b14b5f1345422159508
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716278"
---
# <a name="locking-a-subvolume-of-a-volume-texture"></a>锁定体积纹理的子体积


## <span id="ddk_locking_a_subvolume_of_a_volume_texture_gg"></span><span id="DDK_LOCKING_A_SUBVOLUME_OF_A_VOLUME_TEXTURE_GG"></span>


DirectX 8.1 引入了一项新功能，该功能允许驱动程序只锁定一 subvolume 的卷纹理。 调用驱动程序的 [*DdLock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_lock) 函数时，驱动程序可以通过只锁定 subvolume 而不是整个卷纹理来提高系统性能。

若要指示此功能的支持，驱动程序必须 \_ 在 D3DCAPS8 结构的 **DevCaps** 成员中设置 D3DDEVCAPS SUBVOLUMELOCK 位。 驱动程序将返回 D3DCAPS8 结构来响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

确定对此功能的支持后，驱动程序可以接收 *DdLock* 调用，并在 \_ 传递的 DD LOCKDATA 结构的 **DWFLAGS** 成员中设置 DdLock HASVOLUMETEXTUREBOXRECT 位 \_ 。 此位通知驱动程序锁定指定的 subvolume 纹理。 然后，该驱动程序必须从 DD LOCKDATA 的**rArea**成员中指定的 RECTL 结构的**左侧**和**右侧**成员那里获取锁定的 subvolume 的前后坐标 \_ 。 驱动程序将分别从 **左** 成员和 **右** 成员的更高16位获取前后坐标。

锁定的 subvolume 的左坐标和右坐标限制为 **左** 成员和 **右** 成员的小写16位。 驱动程序使用**rArea**中 RECTL 结构的**顶部**和**底部**成员保持不变，以指定锁定的 subvolume 的上坐标和下坐标。 通过这种方式， **rArea** 成员有效地提供三个坐标集来指定锁定的 subvolume。 Microsoft Windows SDK 文档中介绍了 RECTL 结构。

下面的代码演示如何获取前后坐标：

```cpp
"real" left = rArea.left && 0xFFFF;
"real" right = rArea.right && 0xFFFF;
front = rArea.left >> 16;
back = rArea.right >> 16;
```

此功能在 Windows Me 和 Windows XP 及更高版本上可用。 此功能也适用于安装了 DirectX 8.1 运行时的 Windows 2000 和 Windows 98 操作系统版本。

 

