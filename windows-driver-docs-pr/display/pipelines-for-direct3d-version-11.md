---
title: Direct3D 版本 11 的管道
description: Direct3D 版本 11 的管道
ms.assetid: 7d724751-761e-409c-8398-d1b5d58c057c
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，管道
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，管道
- Direct3D 版本 11 WDK Windows 7 显示管道
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示的管道
- 球面着色器 WDK Windows 7 显示
- 球面着色器 WDK Windows Server 2008 R2 显示
- 细化器 WDK Windows 7 显示
- 细化器 WDK Windows Server 2008 R2 显示
- 域着色器 WDK Windows 7 显示
- 域着色器 WDK Windows Server 2008 R2 显示
- 计算着色器 WDK Windows 7 显示
- 计算着色器 WDK Windows Server 2008 R2 显示
- 无序访问资源视图 WDK Windows 7 显示
- 无序访问资源视图 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d659bbfd55d0db3b99f5b44ae6925846851e7a9b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829809"
---
# <a name="pipelines-for-direct3d-version-11"></a>Direct3D 版本 11 的管道


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

Direct3D 版本11的图形呈现管道从[direct3d 版本10的图形呈现管道](rendering-pipeline.md)进行扩展。 除了支持 Direct3D 版本10的共享可编程着色器内核，Direct3D 版本11还支持 "球面"、"域" 和 "计算" 着色器核心。

Direct3D 版本11实际支持两个单独的管道：绘制管道（图形呈现管道）和调度管道（计算着色器管道）。 绘图和调度管道在技术上是松散连接的，因为不能将相同的 subresource 绑定到同时在这两个管道中写入，也不能将其绑定在一个管道中并在另一个管道中读取。

下图显示了 Direct3D 版本11的绘制管道的功能块。

![说明绘制管道的功能块的关系图](images/pipeline-dx11.png)

下图显示了 Direct3D 11 版的调度管道的功能块。

![说明调度管道的功能块的关系图](images/pipeline-compute.png)

以下各节介绍了前面的插图中所示的新的-Direct3D 11 块。

### <a name="span-idhull_shaderspanspan-idhull_shaderspanhull-shader"></a><span id="hull_shader"></span><span id="HULL_SHADER"></span>凸着色器

此球面着色器每个修补程序运行一次。 可以将 "球面" 着色器与输入汇编程序提供的修补程序结合使用。 "球面" 着色器可以将构成修补程序的输入控制点转换为输出控制点。 可以对 fixed 函数细化器阶段执行其他设置。 例如，"球面" 着色器可以输出 tess 系数，这是指示进行分割的数量。

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁此球面着色器：

[**CalcPrivateShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateshadersize)

[**CalcPrivateTessellationShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)

[*CreateHullShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createhullshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**HsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**HsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**HsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**HsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**HsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

### <a name="span-idtessellatorspanspan-idtessellatorspantessellator"></a><span id="tessellator"></span><span id="TESSELLATOR"></span>细化器

细化器是一个固定函数单元，其操作由 "球面" 着色器中的声明定义。 细化器对每个由凸着色器输出的修补程序运行一次。 外凸着色器生成 tess 因素，这些因素是在修补程序的域上通知细化器多少到进行分割（生成几何和连接）的数字。

Direct3D 运行时调用驱动程序的[**CalcPrivateTessellationShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)函数来计算用于球面或域着色器的内存区域的大小。

### <a name="span-iddomain_shaderspanspan-iddomain_shaderspandomain-shader"></a><span id="domain_shader"></span><span id="DOMAIN_SHADER"></span>域着色器

每个顶点调用一次域着色器，这是由细化器生成的。 每个调用都通过其在泛型域上的坐标进行标识。 域着色器的作用是将此坐标转换为在域着色器的下边缘使用的有形内容（例如，3-d 空间中的一个点）。 修补程序的每个域着色器调用还会访问所有球面着色器输出的共享输入（如输出控制点）。

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁域着色器：

[**CalcPrivateTessellationShaderSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivatetessellationshadersize)

[*CreateDomainShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdomainshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**DsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**DsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**DsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**DsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**DsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

### <a name="span-idcompute_shaderspanspan-idcompute_shaderspancompute-shader"></a><span id="compute_shader"></span><span id="COMPUTE_SHADER"></span>计算着色器

计算着色器允许将 GPU 视为数据并行处理器的通用网格，无需绘制管道的任何图形障碍。 计算着色器具有对快速共享内存的显式访问权限，以便于着色器调用组之间进行通信。 计算着色器还能够对内存执行分散的读取和写入操作。 使用原子操作的可用性可以唯一访问共享内存地址。 计算着色器不是绘制管道的一部分。 计算着色器独立存在。 但是，计算着色器与所有其他着色器阶段位于同一设备上。 Direct3D 运行时调用驱动程序的*DispatchXxx*函数，而不是驱动程序的*DrawXxx*函数来调用计算着色器。

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁计算着色器：

[*CreateComputeShader*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createcomputeshader)

[**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)

[**CsSetShaderResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshaderresources)

[**CsSetShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setshader)

[**CsSetSamplers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setsamplers)

[**CsSetConstantBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setconstantbuffers)

[**CsSetShaderWithIfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setshader_with_ifaces)

[**CsSetUnorderedAccessViews**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setunorderedaccessviews)

[**Dispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_dispatch)

[**DispatchIndirect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_dispatchindirect)

### <a name="span-idunordered_access_resource_viewsspanspan-idunordered_access_resource_viewsspanunordered-access-resource-views"></a><span id="unordered_access_resource_views"></span><span id="UNORDERED_ACCESS_RESOURCE_VIEWS"></span>无序访问资源视图

无序访问资源视图是可绑定到计算着色器或像素着色器的读/写资源。 无序访问资源视图的绑定类似于将着色器资源视图（只读资源）绑定到任何着色器阶段的方式。

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁无序访问资源视图：

[**CalcPrivateUnorderedAccessViewSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_calcprivateunorderedaccessviewsize)

[**CreateUnorderedAccessView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createunorderedaccessview)

[**DestroyUnorderedAccessView**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_destroyunorderedaccessview)

[**ClearUnorderedAccessViewFLOAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_clearunorderedaccessviewfloat)

[**ClearUnorderedAccessViewUINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_clearunorderedaccessviewuint)

[**CopyStructureCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_copystructurecount)

[**SetRenderTargets （D3D11）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_setrendertargets)

 

 





