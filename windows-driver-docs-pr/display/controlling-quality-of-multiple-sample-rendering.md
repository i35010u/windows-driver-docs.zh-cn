---
title: 控制多重采样渲染的质量
description: 控制多重采样渲染的质量
ms.assetid: 5a2f2d36-ab0d-4267-a921-c42621fa5d47
keywords:
- 多个示例呈现 WDK DirectX 9.0、 控制质量
- 呈现 multisamples WDK DirectX 9.0，控制质量
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b4b71247737f24c1e33a4bb1da921d907d3796e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370297"
---
# <a name="controlling-quality-of-multiple-sample-rendering"></a>控制多重采样渲染的质量


## <span id="ddk_controlling_quality_of_multiple_sample_rendering_gg"></span><span id="DDK_CONTROLLING_QUALITY_OF_MULTIPLE_SAMPLE_RENDERING_GG"></span>


应用程序可以请求与特定的多级取样方法创建一个面之前，它应调用**IDirect3D9::CheckDeviceMultiSampleType**方法以验证是否显示设备支持该技术。 在运行时将发送**GetDriverInfo2**请求使用**D3DGDI2\_类型\_GETMULTISAMPLEQUALITYLEVELS**要检索的质量级别的值特定的多重采样类型和与方法关联的图面格式。 有关详细信息**GetDriverInfo2**，请参阅[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

设备的驱动程序是否显示设备支持屏蔽多重采样 （多个示例的呈现器目标格式以及消除锯齿支持多个示例） 或只是 nonmaskable 多重采样 （仅消除锯齿支持），必须提供的数量质量级别的 D3DMULTISAMPLE\_不可屏蔽多个示例类型。 应用程序只需使用多重采样抗锯齿用于者然后只需查询的不可屏蔽的驱动程序支持的多个样本质量级别数。

验证显示设备是否支持多级取样的技术，除了**IDirect3D9::CheckDeviceMultiSampleType**也会返回与方法关联的质量级别数。

当应用程序请求创建图面时，它使用图面格式、 多重采样类型和数个质量级别，之前验证其支持的组合。 这可确保在图面已成功创建。 运行时调用的驱动程序[ *DdCanCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))， [ *DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))，或[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)函数来创建在图面。 在此调用中，运行时将编码为多个采样图面到五位的样本数 (DDSCAPS3\_MULTISAMPLE\_掩码掩码) 和三位到多个样本质量级别数 (DDSCAPS3\_MULTISAMPLE\_质量\_掩码掩码) 的**dwCaps3**的成员[ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))面的的结构。

有关详细信息**IDirect3D9::CheckDeviceMultiSampleType**，请参阅最新的 DirectX SDK 文档。

 

 





