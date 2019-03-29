---
title: Direct3D 版本 11 的管道
description: Direct3D 版本 11 的管道
ms.assetid: 7d724751-761e-409c-8398-d1b5d58c057c
keywords:
- 有关管道 Direct3D 11 版 WDK Windows 7 显示，
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，请为管道
- 管道 Direct3D 版本 11 WDK Windows 7 显示
- 管道 Direct3D 11 版 WDK Windows Server 2008 R2 显示
- 外壳着色器 WDK Windows 7 显示
- 外壳着色器 WDK Windows Server 2008 R2 显示
- 细化器 WDK Windows 7 显示
- 细化器 WDK Windows Server 2008 R2 显示
- 域着色器 WDK Windows 7 显示
- 域着色器 WDK Windows Server 2008 R2 显示
- 计算着色器 WDK Windows 7 显示
- 计算着色器 WDK Windows Server 2008 R2 显示
- 显示无序的访问资源视图 WDK Windows 7
- 无序的访问资源视图 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 788c3c5ee9f1ad42fc9855044ca71bb4fb497c60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568435"
---
# <a name="pipelines-for-direct3d-version-11"></a>Direct3D 版本 11 的管道


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

从扩展图形呈现管道 Direct3D 版本 11[图形呈现管道 Direct3D 版本 10](rendering-pipeline.md)。 除了共享可编程的着色器内核支持 Direct3D 版本 10，Direct3D 11 版还支持外壳，域中，和计算着色器内核。

11 实际上支持两个单独的管道 Direct3D 版本： draw 管道 （图形呈现管道） 和分派管道 （计算着色器管道）。 绘图和调度管道从技术上讲在意义上说，您不能具有相同的子资源的同时，在这两个管道编写绑定或绑定在一个管道中编写和读取另一个管道中的松散连接。

下图显示了绘图管道 Direct3D 版本 11 的功能块。

![说明描述管道的功能块的关系图](images/pipeline-dx11.png)

下图显示了 Direct3D 版本 11 分派管道的功能块。

![说明分派管道的功能块的关系图](images/pipeline-compute.png)

以下部分介绍上述各图所示的新的 Direct3D 11 块。

### <a name="span-idhullshaderspanspan-idhullshaderspanhull-shader"></a><span id="hull_shader"></span><span id="HULL_SHADER"></span>外壳着色器

每个补丁的外壳着色器一次操作。 外壳着色器可用于从输入装配器修补程序。 外壳着色器可以转换的输入的控件构成了一个修补程序输出控制的点到的点。 外壳着色器可以执行其他安装程序的固定功能细化器阶段。 例如，外壳着色器可以输出为数字，指示多少以对 tess 因素。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁外壳着色器：

[**CalcPrivateShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538315)

[**CalcPrivateTessellationShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538318)

[*CreateHullShader*](https://msdn.microsoft.com/library/windows/hardware/ff540655)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**HsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff567300)

[**HsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff567294)

[**HsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff567290)

[**HsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff567286)

[**HsSetShaderWithIfaces**](https://msdn.microsoft.com/library/windows/hardware/ff567306)

### <a name="span-idtessellatorspanspan-idtessellatorspantessellator"></a><span id="tessellator"></span><span id="TESSELLATOR"></span>细化器

细化器是由外壳着色器中的声明定义其操作的固定功能单元。 细化器操作后，每个修补程序是由外壳着色器输出。 外壳着色器生成 tess 因素，是多少通知细化器以对数字 （生成几何和连接） 的修补程序的域上。

Direct3D 运行时调用的驱动程序[ **CalcPrivateTessellationShaderSize** ](https://msdn.microsoft.com/library/windows/hardware/ff538318)函数来计算的外壳或域着色器的内存区域的大小。

### <a name="span-iddomainshaderspanspan-iddomainshaderspandomain-shader"></a><span id="domain_shader"></span><span id="DOMAIN_SHADER"></span>域着色器

域着色器每顶点，生成的细化器一次调用。 每次调用都由其坐标上一般的域标识。 域着色器的作用是启用相应的坐标转换的内容 （例如，在三维空间中点） 有形供下游域着色器的使用。 每个域着色器调用了修补程序还可访问共享 （例如，输出控制磅为单位） 的所有外壳着色器输出的输入。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁域着色器：

[**CalcPrivateTessellationShaderSize**](https://msdn.microsoft.com/library/windows/hardware/ff538318)

[*CreateDomainShader*](https://msdn.microsoft.com/library/windows/hardware/ff540637)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**DsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff557306)

[**DsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff557305)

[**DsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff557298)

[**DsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff557289)

[**DsSetShaderWithIfaces**](https://msdn.microsoft.com/library/windows/hardware/ff557316)

### <a name="span-idcomputeshaderspanspan-idcomputeshaderspancompute-shader"></a><span id="compute_shader"></span><span id="COMPUTE_SHADER"></span>计算着色器

计算着色器允许 GPU，您可以为泛型网格的数据并行处理器，而无需从绘图管道任何图形障碍。 计算着色器可以快速显式访问共享内存，以便于组的着色器调用之间的通信。 计算着色器还可以执行分散的读取和写入到内存。 原子操作的可用性可以唯一访问共享的内存地址。 计算着色器不是绘制管道的一部分。 其自身上存在计算着色器。 但是，计算着色器为所有其他着色器阶段在同一设备上存在。 Direct3D 运行时调用的驱动程序*DispatchXxx*而不是驱动程序的函数*DrawXxx*函数要调用的计算着色器。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁计算着色器：

[*CreateComputeShader*](https://msdn.microsoft.com/library/windows/hardware/ff540606)

[**DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805)

[**CsSetShaderResources**](https://msdn.microsoft.com/library/windows/hardware/ff540802)

[**CsSetShader**](https://msdn.microsoft.com/library/windows/hardware/ff540799)

[**CsSetSamplers**](https://msdn.microsoft.com/library/windows/hardware/ff540795)

[**CsSetConstantBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff540794)

[**CsSetShaderWithIfaces**](https://msdn.microsoft.com/library/windows/hardware/ff540805)

[**CsSetUnorderedAccessViews**](https://msdn.microsoft.com/library/windows/hardware/ff540808)

[**调度**](https://msdn.microsoft.com/library/windows/hardware/ff553896)

[**DispatchIndirect**](https://msdn.microsoft.com/library/windows/hardware/ff553899)

### <a name="span-idunorderedaccessresourceviewsspanspan-idunorderedaccessresourceviewsspanunordered-access-resource-views"></a><span id="unordered_access_resource_views"></span><span id="UNORDERED_ACCESS_RESOURCE_VIEWS"></span>无序的访问资源视图

无序的访问资源视图是可以将绑定到的计算着色器或像素着色器的读/写资源。 类似于如何将着色器资源视图，这是只读的资源，绑定到任何着色器阶段是无序的访问资源视图的绑定。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁无序的访问资源视图：

[**CalcPrivateUnorderedAccessViewSize**](https://msdn.microsoft.com/library/windows/hardware/ff538320)

[**CreateUnorderedAccessView**](https://msdn.microsoft.com/library/windows/hardware/ff540711)

[**DestroyUnorderedAccessView**](https://msdn.microsoft.com/library/windows/hardware/ff552812)

[**ClearUnorderedAccessViewFLOAT**](https://msdn.microsoft.com/library/windows/hardware/ff539412)

[**ClearUnorderedAccessViewUINT**](https://msdn.microsoft.com/library/windows/hardware/ff539414)

[**CopyStructureCount**](https://msdn.microsoft.com/library/windows/hardware/ff540544)

[**SetRenderTargets(D3D11)**](https://msdn.microsoft.com/library/windows/hardware/ff569554)

 

 





