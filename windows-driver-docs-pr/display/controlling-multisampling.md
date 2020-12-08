---
title: 控制多重采样
description: 控制多重采样
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多级显示，控制
- 以多级显示方式呈现 WDK DirectX 8.0，控制
- 呈现 multisamples WDK DirectX 8.0，控制
- D3DRS_MULTISAMPLEANTIALIAS
- D3DRS_MULTISAMPLEMASK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e18a0fdd5587c2c2d8f1a2050a6c1a1571ba613
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810137"
---
# <a name="controlling-multisampling"></a>控制多重采样


## <span id="ddk_controlling_multisampling_gg"></span><span id="DDK_CONTROLLING_MULTISAMPLING_GG"></span>


D3DRENDERSTATETYPE 枚举控制多级显示的两个呈现状态。 有关 D3DRENDERSTATETYPE 的详细信息，请参阅 DirectX 8.0 SDK 文档。

### <a name="span-idd3drs_multisampleantialiasspanspan-idd3drs_multisampleantialiasspand3drs_multisampleantialias"></a><span id="d3drs_multisampleantialias"></span><span id="D3DRS_MULTISAMPLEANTIALIAS"></span>D3DRS \_ MULTISAMPLEANTIALIAS

一个布尔值，该值确定使用多级显示目标缓冲区时如何计算各个样本。 如果设置为 **TRUE**，则计算多个样本，以便在每个多个样本的不同样本位置上进行采样来执行完整场景的抗锯齿。 如果设置为 " **FALSE**"，则多个样本都用相同的样本值编写， (在像素中心) ，这允许 nonantialiased 呈现为多级采样缓冲区。 在呈现为单个样本缓冲区时，此呈现状态不起作用。 默认值为 **TRUE**。

### <a name="span-idd3drs_multisamplemaskspanspan-idd3drs_multisamplemaskspand3drs_multisamplemask"></a><span id="d3drs_multisamplemask"></span><span id="D3DRS_MULTISAMPLEMASK"></span>D3DRS \_ MULTISAMPLEMASK

此掩码中的每个位（从 LSB 开始）控制在多级呈现目标中修改某个示例。 因此，对于8示例呈现器目标，低字节包含为每个8个样本启用的8次写入。 在呈现为单个样本缓冲区时，此呈现状态不起作用。 默认值为 0xFFFFFFFF。

此呈现状态允许使用多级采样缓冲区作为累积缓冲区，并执行几何的 multipass 渲染，其中每个阶段都将更新示例的子集。

多级呈现目标中的每个示例都为最终呈现的图像提供统一的强度。 例如，请考虑，采样模式为3，使用多级采样屏蔽启用的样本数为2。 因此，呈现的图像的生成亮度为2/3。 也就是说，每个像素的每个红色、绿色和蓝色分量的强度都由2/3 来分解。

 

 





