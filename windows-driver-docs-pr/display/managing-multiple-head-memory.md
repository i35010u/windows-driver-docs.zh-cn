---
title: 管理多头内存
description: 管理多头内存
ms.assetid: 37cda124-0c3b-4af4-92b8-329440dd3221
keywords:
- 多头硬件 WDK DirectX 9.0，内存管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 270b30bc4ca51c716e44c766abc13e267cd531a9
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715306"
---
# <a name="managing-multiple-head-memory"></a>管理多头内存


## <span id="ddk_managing_multiple_head_memory_gg"></span><span id="DDK_MANAGING_MULTIPLE_HEAD_MEMORY_GG"></span>


\_在 DDSCAPS2 ADDITIONALPRIMARY 的**dwCaps2**成员中，为从属标题上[**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))的每个曲面设置 "" 功能位，将通知这些曲面是从分配给打印头的视频内存中分配的最后一个表面。 然后，从属头应该放弃控制将其视频内存分配给主头，因为从属头保证在应用程序的生存期内不会收到后续的 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 调用。

驱动程序必须确保主头能够分配与从属磁头关联的内存。

当运行时调用驱动程序的 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 函数来销毁设置 DDSCAPS2 ADDITIONALPRIMARY 功能位的从属头上的图面时 \_ ，会通知驱动程序，使从属头再次控制其视频内存管理。

大多数情况下，在现有 DirectDraw 过程中，这种选择哪一种拥有视频内存是固有的。 尤其是在下列情况下：

-   使用 DDSCAPS2 ADDITIONALPRIMARY 位进行 *DdCreateSurface* 调用后，运行时保证不会在从属机头上发出后续分配请求 \_ 。 因此，在任何时候，都不需要驱动程序限制其自己的视频内存池的分配。

-   当应用程序被终止或最小化时，将销毁所有表面。 因此，会清除从从属头池中的主头创建的所有纹理。

-   如果 \_ 没有为从属标题上的表面设置 DDSCAPS2 ADDITIONALPRIMARY 位，则这些磁头会继续分配视频内存，就好像它们是独立的。 事实上，此类从属机头在功能上等同于其他任何多监视器适配器。

-   驱动程序需要提供一个实现，在此实现中，主头从从属头池分配内存，包括确定何时可以从从属头的池分配特定资源。 请注意，主 head 不会有任何有关它是否参与多头方案的信息本身。 当主头在其自己的视频内存中运行时，它必须遍历其组中的所有从属 head，以确定其中是否有任何磁头可以由主 (使用的池，以确定是否有任何从属方使用 DDSCAPS2 *DdCreateSurface* \_ ADDITIONALPRIMARY 位集) 接收到 DdCreateSurface 的调用。

-   最后请注意，运行时确保组中的所有 head 都参与多头方案。 因此，驱动程序必须只维护一位状态，指示它当前是否处于多头模式。

 

