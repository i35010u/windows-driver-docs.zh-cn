---
title: 驱动程序保护
description: 视频内存管理器以及每个虚拟地址，允许独立硬件供应商 (Ihv) 可以定义一个驱动程序 / 硬件特定的保护 （即
ms.assetid: 3D636BD1-683D-49B4-A7E5-176853EA11EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16293ebf7c7e687d2f6e16ed00365553f865a154
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563167"
---
# <a name="driver-protection"></a>驱动程序保护


视频内存管理器以及每个虚拟地址，允许独立硬件供应商 (Ihv) 可以定义一个驱动程序 / 硬件特定的保护 （即页表条目编码） 专门与该虚拟地址相关联。 考虑一下作为额外位，但该驱动程序必须控制以便访问内存在图形处理单元 (GPU)，以最佳方式的视频内存管理器不知道的页表条目中的驱动程序保护。

**请注意**  驱动程序保护是可选的可以将其保留为不需要此功能的任意平台上的零。

 

映射或保留 GPU 虚拟地址范围时，驱动程序可能指定的 64 位驱动程序保护值。 初始化与该特定的虚拟地址对应的页表项时，将视频内存管理器使用指定的驱动程序保护。 具体而言，驱动程序保护会送回给该驱动程序的任何[ *BuildPagingBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff559587)**DXGK\_操作\_更新\_页\_表**对应于指定的虚拟地址。

多个虚拟地址可以映射到单个分配使用不同的驱动程序保护功能。 将使用相应的驱动程序保护更新的每个这些虚拟地址的页表条目。

驱动程序保护仅适用于级别 0 页表项，且将设置为零的任何其他页表条目级别。

## <a name="span-idpaginganduniquedriverprotectionspanspan-idpaginganduniquedriverprotectionspanspan-idpaginganduniquedriverprotectionspanpaging-and-unique-driver-protection"></a><span id="Paging_and_unique_driver_protection"></span><span id="paging_and_unique_driver_protection"></span><span id="PAGING_AND_UNIQUE_DRIVER_PROTECTION"></span>分页和唯一驱动程序保护


时分页入或移出内存段的分配，视频内存管理器将从用于分配的内容传输的系统设备地址空间分配一个临时的虚拟地址。 当创建此映射，分配相关的驱动程序保护是不明确，因为可能存在各种不同的驱动程序保护的进程地址空间中的多个映射。

正因为如此，视频内存管理器将指定任何系统设备映射，默认情况下用于分页的零的驱动程序的保护。

驱动程序可以通过设置更改此行为**唯一**位时指定的虚拟地址与关联的驱动程序保护。

`#define D3DGPU_UNIQUE_DRIVER_PROTECTION 0x8000000000000000ULL`

视频内存管理器时设置此位，则将强制执行任何映射到相同的分配区域使用相同的驱动程序保护值，或映射请求将失败，**状态\_无效\_参数**.

使用唯一的驱动程序保护值、 映射的分配范围不能再次映射具有不同的保护值。 在这种情况下更改保护的唯一方法是映射具有无访问权限的范围。

可以与任何保护值再次映射具有非唯一的驱动程序保护值映射的分配范围。

当将逐出已映射到驱动程序保护的虚拟地址范围的分配设置为*唯一*，视频内存管理器将在安装程序用于在对具有相应的驱动程序保护这些范围的分页进程映射无歧义地的值。

下图显示了 VA 映射的分配不同的驱动程序保护值。

![使用不同的驱动程序保护分配的虚拟地址映射](images/driver-protection.1.png)

在分页操作期间分配将被复制以块的形式：

1. 复制分配范围\[0，A1\]与驱动程序保护 0
2. 复制分配范围\[A1、 A2\]与驱动程序保护 P1
3. 复制分配范围\[A2、 A4\]与驱动程序保护 0
4. 复制分配范围\[A4、 A5\]与驱动程序保护 P4
5. 复制分配范围\[A5、 大小\]使用驱动程序保护 0 就可能的分页进程页表项时，将设置一个驱动程序保护值逐出分配并将其设置为不同的值时将会进行分配已提交。 假定更新的虚拟地址映射后，该驱动程序应刷新分配数据。
例如，考虑一种情况时将组映射的当前分配是 M1 和用户模式驱动程序调用[ *UpdateGpuVirtualAddress* ](https://msdn.microsoft.com/library/windows/hardware/dn906365)映射设置 M2。 映射集应用 M2 之前, 的视频内存管理器可以被逐出分配。 M2 应用的映射集和分配会提交回。 现在的本地内存段中的分配内容可能不同于原始。

## <a name="span-idtiledresourcesspanspan-idtiledresourcesspanspan-idtiledresourcesspantiled-resources"></a><span id="Tiled_Resources"></span><span id="tiled_resources"></span><span id="TILED_RESOURCES"></span>平铺的资源


平铺资源时保留虚拟地址范围指定驱动程序保护。 用户模式驱动程序调用[ *UpdateGpuVirtualAddress* ](https://msdn.microsoft.com/library/windows/hardware/dn906365)将继承虚拟地址的最新驱动程序保护。

 

 





