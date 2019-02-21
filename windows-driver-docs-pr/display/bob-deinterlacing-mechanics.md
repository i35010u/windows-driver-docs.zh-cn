---
title: Bob 取消隔行扫描机制
description: Bob 取消隔行扫描机制
ms.assetid: 1735f9c6-ac83-4a6a-bc6f-4d4a193876dd
keywords:
- bob 去隔行 WDK DirectX va，因此机制
- 交错字段 WDK DirectX VA
- stride WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA，bob、 机制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afedf91ae8d5627c2bb96dd6d6a9998888f2dd71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523004"
---
# <a name="bob-deinterlacing-mechanics"></a>Bob 取消隔行扫描机制


## <span id="ddk_bob_deinterlacing_mechanics_gg"></span><span id="DDK_BOB_DEINTERLACING_MECHANICS_GG"></span>


可以执行位块传输的所有图形适配器可以都执行简单的 bob 样式去隔行。 当图面中包含两个交错的字段时，可以重新解释的内存布局图面的来隔离每个字段。 这被通过加倍原始面 stride 和除以在下半部分图面的高度。 在这种方式中隔离的两个字段后，它们可以 deinterlaced 通过延伸到正确的帧高度的各个字段中。

额外的水平拉伸或收缩可还用于更正纵横比的视频图像像素。 显示驱动程序可以确定执行此操作 DirectX 视频混合使用呈现器 (VMR) 到其功能。 通过行复制或，最好是通过筛选 stretch 可以垂直拉伸各个字段的高度。 如果使用的行复制方法，则生成的映像有块状外观。 如果使用已筛选的 stretch，则生成的映像可能略有模糊的外观。

下图显示了包含两个交错的字段的视频表面。

![说明包含交错的两个字段的表面的内存布局的关系图](images/deinterlace.png)

如果视频的示例包含两个交错的字段作为由指定**DXVA\_SampleFieldInterleavedEvenFirst**并**DXVA\_SampleFieldInterleavedOddFirst**成员[ **DXVA\_SampleFormat** ](https://msdn.microsoft.com/library/windows/hardware/ff564045)枚举，第二个字段的开始时间的计算使用**rtStart**和**rtEnd**的成员[ **DXVA\_VideoSample** ](https://msdn.microsoft.com/library/windows/hardware/ff564085)结构，如下所示：

(**rtStart** + **rtEnd**) / 2

第一个字段的结束时间是第二个字段的开始时间。

 

 





