---
title: 将反交错 DDI 映射到 DirectDraw 和 DirectX VA
description: 将反交错 DDI 映射到 DirectDraw 和 DirectX VA
keywords:
- 取消隔行扫描 WDK DirectX VA，映射取消隔行扫描 DDI
- 映射取消隔行扫描 DDI
- 容器方法 WDK DirectX VA
- 设备方法 WDK DirectX VA
- 运动补偿 WDK DirectX VA
- 回调 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d43d8d6d646adf461e6bcf1e79c16ed0d6be1f0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793867"
---
# <a name="mapping-the-deinterlace-ddi-to-directdraw-and-directx-va"></a>将反交错 DDI 映射到 DirectDraw 和 DirectX VA


## <span id="ddk_mapping_the_deinterlace_ddi_to_directdraw_and_directx_va_gg"></span><span id="DDK_MAPPING_THE_DEINTERLACE_DDI_TO_DIRECTDRAW_AND_DIRECTX_VA_GG"></span>


必须通过 DirectDraw 的 [运动补偿回调函数](motion-compensation-callbacks.md) 访问取消隔行扫描功能，取消 [隔行扫描 DDI](./deinterlace-ddi.md) 可以映射到该函数。

隔行扫描 DDI 分为两个功能组： DirectX VA 容器方法和 DirectX VA 设备方法。 容器方法决定显示硬件包含的每个 DirectX VA 设备的功能。 设备方法指示设备执行特定于设备的操作。 DirectX VA 驱动程序只能有一个容器，但它可以支持多个设备。

可以将非隔行扫描 DDI 映射到运动补偿回调，因为它们不使用类型化参数 (也就是说，其单个参数是指向结构) 的指针。 换句话说，传递给运动补偿回调函数的单个参数中的信息可根据其信息类型进行处理。 例如，如果将 **DXVA \_ DeinterlaceBltFnCode** 类型的信息传递到 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 函数，则 *DdMoCompRender* 可以调用逐行处理 DDI 的 [**DeinterlaceBlt**](./dxva-deinterlacebobdeviceclass-deinterlaceblt.md) 函数，以执行视频流对象的位块取消隔行扫描。 但是，如果 **将 DXVA \_ DeinterlaceQueryModeCapsFnCode** 类型的信息传递给 *DdMoCompRender* ，则 *DdMoCompRender* 可以调用逐行扫描 DDI 的 [**DeinterlaceQueryModeCaps**](./dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md) 函数来查询取消隔行扫描模式的功能。

以下主题介绍如何将隔行扫描 DDI 映射到运动补偿回调：

[用于反交错的反交错容器设备](deinterlace-container-device-for-deinterlacing.md)

[从用户模式组件调用反交错 DDI](calling-the-deinterlace-ddi-from-a-user-mode-component.md)

 

