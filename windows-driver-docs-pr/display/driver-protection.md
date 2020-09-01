---
title: 驱动程序保护
description: 除了每个虚拟地址，视频内存管理器还允许独立的硬件供应商 (Ihv) 来定义驱动程序/特定于硬件的保护 (即
ms.assetid: 3D636BD1-683D-49B4-A7E5-176853EA11EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 836c1656f3752845a643eb40232f0a1e36761753
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067438"
---
# <a name="driver-protection"></a>驱动程序保护


除了每个虚拟地址，视频内存管理器还允许独立的硬件供应商 (Ihv) 来定义特定于该虚拟地址的特定于驱动程序/硬件的保护 (即页面表条目编码) 。 将驱动程序保护看作是视频内存管理器不知道的页表条目中的额外位，但驱动程序必须控制以使图形处理单元 (GPU) 以最佳方式访问内存。

**注意**   驱动程序保护是可选的，可以在任何不需要此功能的平台上将其留空。

 

映射或保留 GPU 虚拟地址范围时，驱动程序可能会指定64位驱动程序保护值。 指定的驱动程序保护是在初始化与特定虚拟地址相对应的页表项时由视频内存管理器使用的。 具体而言，驱动程序保护将返回到对应于指定虚拟地址的任何 [*BuildPagingBuffer*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)**DXGK \_ 操作 \_ 更新 \_ 页 \_ 表** 的驱动程序。

可以使用不同的驱动程序保护将多个虚拟地址映射到单个分配。 将使用适当的驱动程序保护来更新每个虚拟地址的页表项。

驱动程序保护仅适用于级别0的页表项，对于任何其他页表项级别，都将设置为零。

## <a name="span-idpaging_and_unique_driver_protectionspanspan-idpaging_and_unique_driver_protectionspanspan-idpaging_and_unique_driver_protectionspanpaging-and-unique-driver-protection"></a><span id="Paging_and_unique_driver_protection"></span><span id="paging_and_unique_driver_protection"></span><span id="PAGING_AND_UNIQUE_DRIVER_PROTECTION"></span>寻呼和唯一的驱动程序保护


当对内存段中的分配进行分页时，视频内存管理器会从系统设备地址空间分配一个临时虚拟地址，以便传输分配的内容。 创建此映射时，与分配相关的驱动程序保护是不明确的，因为可能存在多个具有不同驱动程序保护的进程地址空间中的映射。

因此，默认情况下，对于用于分页的任何系统设备映射，视频内存管理器将指定零的驱动程序保护。

驱动程序可以通过在指定与虚拟地址相关联的驱动程序保护时设置 **唯一** 位来更改此行为。

`#define D3DGPU_UNIQUE_DRIVER_PROTECTION 0x8000000000000000ULL`

设置此位后，视频内存管理器将强制对相同分配范围的任何映射使用相同的驱动程序保护值，否则，映射请求将失败，并显示 " **状态 \_ 无效" \_ 参数**。

使用不同的保护值无法再次映射使用唯一的驱动程序保护值映射的分配范围。 在这种情况下，更改保护的唯一方法是映射范围而不进行访问。

使用不唯一的驱动程序保护值映射的分配范围可以与任何保护值重新映射。

当逐出虚拟地址范围被设置为 *unique*的驱动程序保护的分配时，视频内存管理器将使用适当的驱动程序保护值（不明确）设置用于这些范围的分页过程映射。

下图显示了具有不同的驱动程序保护值的分配的 VA 映射。

![具有不同驱动程序保护的分配的虚拟地址映射](images/driver-protection.1.png)

在分页操作期间，将以区块形式复制分配：

1. 复制分配范围 \[ 0，A1， \] 驱动程序保护0
2. 复制分配范围 \[ A1，A2 \] 与驱动程序保护 P1
3. 复制分配范围 \[ A2， \] 含驱动程序保护的 A4 0
4. 复制分配范围 \[ A4、 \] 带有驱动程序保护的 A5 P4
5. 复制分配范围 \[ A5，大小 \] ，使用驱动程序保护0可以在分配分配时，使用一个驱动程序保护值设置分页进程页表项，并在提交分配时将其设置为其他值。 假定驱动程序应在更新虚拟地址映射后刷新分配数据。
例如，当当前分配映射集为 M1 并且用户模式驱动程序名为 [*UpdateGpuVirtualAddress*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb) ，并且映射设置为 M2 时，请考虑使用这种情况。 就在应用映射集 M2 之前，可以通过视频内存管理器逐出分配。 应用映射集 M2 并提交分配。 现在本地内存段中的分配内容可能不同于原始内容。

## <a name="span-idtiled_resourcesspanspan-idtiled_resourcesspanspan-idtiled_resourcesspantiled-resources"></a><span id="Tiled_Resources"></span><span id="tiled_resources"></span><span id="TILED_RESOURCES"></span>平铺资源


对于平铺资源，在保留虚拟地址范围时指定驱动程序保护。 用户模式驱动程序对 [*UpdateGpuVirtualAddress*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb) 的调用将继承虚拟地址当前驱动程序保护。

 

