---
title: 控制多重采样渲染的质量
description: 控制多重采样渲染的质量
ms.assetid: 5a2f2d36-ab0d-4267-a921-c42621fa5d47
keywords:
- 多样本渲染 WDK DirectX 9.0，控制质量
- 呈现 multisamples WDK DirectX 9.0，控制质量
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec39e897975a5c0111c18dee295480ba022f4f54
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715206"
---
# <a name="controlling-quality-of-multiple-sample-rendering"></a>控制多重采样渲染的质量


## <span id="ddk_controlling_quality_of_multiple_sample_rendering_gg"></span><span id="DDK_CONTROLLING_QUALITY_OF_MULTIPLE_SAMPLE_RENDERING_GG"></span>


在应用程序可以请求创建具有特定多级多级方法的图面之前，应调用 **IDirect3D9：： CheckDeviceMultiSampleType** 方法来验证显示设备是否支持该技术。 然后，运行时将使用**D3DGDI2 \_ 类型 \_ GETMULTISAMPLEQUALITYLEVELS**值发送**GetDriverInfo2**请求，以检索与该技术关联的特定多级采样类型和表面格式的质量级别数。 有关 **GetDriverInfo2**的详细信息，请参阅 [支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

无论显示设备是否支持多样本呈现目标格式 (多个样本和消除锯齿支持 () 的多个样本和消除锯齿支持) ，设备的驱动程序必须提供 D3DMULTISAMPLE \_ 不可屏蔽多示例类型的质量级别。 只需使用多级采样进行抗锯齿的应用程序，只需查询驱动程序支持的不可屏蔽多示例质量级别。

除了验证显示设备是否支持多级采样技术外， **IDirect3D9：： CheckDeviceMultiSampleType** 还返回与该技术关联的质量级别数。

当应用程序请求创建图面时，它将使用曲面格式、多级采样类型和其支持之前验证的质量级别的组合。 这可确保成功创建图面。 运行时调用驱动程序的 [*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))、 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))或 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 函数来创建图面。 在此调用中，运行时将多采样面上的样本数编码为五位 (DDSCAPS3 的 \_ 多级 \_) ，并将多样本质量级别的数量转换为三位 (\_ \_ \_ 图面的[**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))结构的**dwCaps3**成员) 。

有关 **IDirect3D9：： CheckDeviceMultiSampleType**的详细信息，请参阅最新的 DirectX SDK 文档。

 

