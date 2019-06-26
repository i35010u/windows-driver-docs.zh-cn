---
title: 将反交错 DDI 映射到 DirectDraw 和 DirectX VA
description: 将反交错 DDI 映射到 DirectDraw 和 DirectX VA
ms.assetid: a060265f-e1a2-416c-8533-6971cc9e2156
keywords:
- 去隔行 WDK DirectX VA，映射取消隔行扫描 DDI
- 去隔行 DDI 的映射
- 容器方法，WDK DirectX VA
- 设备方法 WDK DirectX VA
- 运动补偿 WDK DirectX VA
- 回调 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ca7b655e5bef9973b680676221bbefeedd700ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370123"
---
# <a name="mapping-the-deinterlace-ddi-to-directdraw-and-directx-va"></a>将反交错 DDI 映射到 DirectDraw 和 DirectX VA


## <span id="ddk_mapping_the_deinterlace_ddi_to_directdraw_and_directx_va_gg"></span><span id="DDK_MAPPING_THE_DEINTERLACE_DDI_TO_DIRECTDRAW_AND_DIRECTX_VA_GG"></span>


去隔行功能必须通过 DirectDraw 的访问[动作补偿回调函数](motion-compensation-callbacks.md)所属[取消隔行扫描 DDI](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-ddi)可以映射。

DDI 划分为两个功能组取消隔行扫描： DirectX VA 容器方法和 DirectX VA 设备方法。 容器方法确定的每个 DirectX VA 设备显示硬件所包含的功能。 设备方法直接设备执行特定于设备的操作。 DirectX VA 驱动程序可以有一个容器，但它可以支持多个设备。

可以将取消隔行扫描 DDI 映射到运动补偿回调，因为它们不使用类型化的参数 （即，其单个参数是指向一个结构的指针）。 换而言之，可以根据其信息类型处理传递给运动补偿回调函数的单个参数中的信息。 例如，如果**DXVA\_DeinterlaceBltFnCode**的类型信息传递给[ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)函数， *DdMoCompRender*可以调用[ **DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)函数取消隔行扫描 DDI 执行位块取消隔行扫描的视频流对象。 但是，如果**DXVA\_DeinterlaceQueryModeCapsFnCode**的类型信息传递给*DdMoCompRender*而*DdMoCompRender*可以调用[**DeinterlaceQueryModeCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)函数取消隔行扫描 DDI 查询取消隔行扫描模式的功能。

以下主题描述如何取消隔行扫描 DDI 映射到运动补偿回调：

[取消隔行扫描适用于去隔行容器设备](deinterlace-container-device-for-deinterlacing.md)

[调用取消隔行扫描 DDI 从用户模式组件](calling-the-deinterlace-ddi-from-a-user-mode-component.md)

 

 





