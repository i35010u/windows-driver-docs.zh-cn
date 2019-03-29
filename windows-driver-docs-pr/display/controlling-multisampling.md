---
title: 控制多重采样
description: 控制多重采样
ms.assetid: 73cdfda8-f67a-470b-a17e-0bf78a5d1df1
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多重采样呈现、 控制
- 多重采样呈现 DirectX WDK 8.0，控制
- 呈现 multisamples WDK DirectX 8.0，控制
- D3DRS_MULTISAMPLEANTIALIAS
- D3DRS_MULTISAMPLEMASK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545ad75a6ef2a188fb48fda65cd27daa731bdd71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564520"
---
# <a name="controlling-multisampling"></a>控制多重采样


## <span id="ddk_controlling_multisampling_gg"></span><span id="DDK_CONTROLLING_MULTISAMPLING_GG"></span>


两个呈现 D3DRENDERSTATETYPE 枚举控制多重采样呈现的状态。 有关 D3DRENDERSTATETYPE 详细信息，请参阅 DirectX 8.0 SDK 文档。

### <a name="span-idd3drsmultisampleantialiasspanspan-idd3drsmultisampleantialiasspand3drsmultisampleantialias"></a><span id="d3drs_multisampleantialias"></span><span id="D3DRS_MULTISAMPLEANTIALIAS"></span>D3DRS\_MULTISAMPLEANTIALIAS

确定如何各个示例的 BOOL 值计算时使用多重采样呈现器目标缓冲区。 如果设置为 **，则返回 TRUE**，多个样本计算，以便由多个示例采样间隔为每个不同的示例位置执行完整场景抗锯齿。 如果设置为**FALSE**，多个示例编写示例值相同 （采样像素中心），它允许 nonantialiased 呈现到多重采样的缓冲区。 呈现给单一样本缓冲区时，则此呈现器状态无效。 默认值是 **，则返回 TRUE**。

### <a name="span-idd3drsmultisamplemaskspanspan-idd3drsmultisamplemaskspand3drsmultisamplemask"></a><span id="d3drs_multisamplemask"></span><span id="D3DRS_MULTISAMPLEMASK"></span>D3DRS\_MULTISAMPLEMASK

开始 LSB，此掩码中的每个位 multisample 中的控件修改其中一个示例的呈现器目标。 因此，对于 8 示例呈现器目标的低位字节的每个 8 示例包含 8 写启用。 呈现给单一样本缓冲区时，则此呈现器状态无效。 默认值为 0xFFFFFFFF。

此呈现器状态启用为累积缓冲区，其中每次更新的示例子集执行多次呈现的几何图形的多重采样缓冲区使用。

多重采样呈现目标中的每个示例都提供统一到最终的已呈现图像亮度。 例如，请考虑，多重采样模式为 3，并启用了使用多重采样掩码的样本数是 2。 因此，生成呈现的图像的强度为 2/3。 也就是说，每个像素的每个红色、 绿色和蓝色分量的强度的分解情况按 2/3。

 

 





