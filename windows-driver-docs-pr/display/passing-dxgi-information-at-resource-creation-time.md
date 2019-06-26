---
title: 创建资源时传递 DXGI 信息
description: 创建资源时传递 DXGI 信息
ms.assetid: d99fc77a-7192-4e45-852a-7a2ae87cc9a2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6597ddccb98d6abce6025bf6a51634938aac662
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377377"
---
# <a name="passing-dxgi-information-at-resource-creation-time"></a>创建资源时传递 DXGI 信息


Direct3D 版本 10 运行时可以调用用户模式显示驱动程序时，传递 DXGI 特有的信息[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)函数来创建资源。 在运行时可以传递一个指向[ **DXGI\_DDI\_主\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)结构**pPrimaryDesc**的成员[ **D3D10DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)结构，以指定资源可作为主 （也就是说，资源可以扫描出到显示）。 运行时设置**pPrimaryDesc**为非 NULL 值，仅当运行时还会设置 D3D10\_DDI\_绑定\_存在比以**BindFlags**的成员D3D10DDIARG\_CREATERESOURCE。

在运行时可以指定 DXGI\_DDI\_主\_中的可选标志**标志**DXGI 成员\_DDI\_主\_DESC 通知用户模式驱动程序可以选择退出从翻页样式演示文稿中使用资源的显示驱动程序。 通知运行时，它应使用该资源中翻页样式演示文稿，驱动程序设置 DXGI\_DDI\_主\_驱动程序\_标志\_否\_中SCANOUT标志**DriverFlags**成员的 DXGI\_DDI\_主\_DESC。

如果该驱动程序返回 DXGI\_DDI\_主\_驱动程序\_标志\_否\_SCANOUT 中的[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)调用来创建资源，运行时将始终执行位块传输 (bitblt) 的样式 （而不是翻页样式演示文稿） 的演示文稿时的资源是演示文稿源。 此功能很有用，如果图形硬件无法扫描出给定的资源类型的特定子集。 例如，图形硬件可能会或可能不能扫描资源多级采样后台缓冲区类型。 此外，能够扫描出多级采样后台缓冲区可能进一步依赖于表面的格式。 如果不能扫描出特定的多级采样格式的图形硬件，用户模式显示驱动程序将设置 DXGI\_DDI\_主\_驱动程序\_标志\_否\_中的 SCANOUT 标志**DriverFlags** DXGI 成员\_DDI\_主\_DESC 为此格式的资源。

如果在运行时不会设置 DXGI\_DDI\_主\_中的可选标志**标志**DXGI 成员\_DDI\_主\_DESC 来通知该驱动程序有关选择退出翻页样式演示文稿中使用资源的可能性，该驱动程序仍会返回 DXGI\_DDI\_ERR\_不受支持的错误代码，连同 DXGI\_DDI\_主\_驱动程序\_标志\_否\_调用 SCANOUT 标志[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)。 在驱动程序*CreateResource(D3D10)* 传递 DXGI\_DDI\_ERR\_不受支持的调用中[ **pfnSetErrorCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)如果该驱动程序不能扫描出此类主要，函数。 返回 DXGI\_DDI\_ERR\_不受支持的以及 DXGI\_DDI\_主\_驱动程序\_标志\_否\_SCANOUT 导致到 DXGIinterpose 代理图面之间的后台缓冲区和主表面的演示文稿路径中。 代理面始终与大小、 multisample 和旋转方面的主 （扫描扩展） 面相匹配。 此过程的第一步是确定哪些 multisample dxgi 或旋转的设置会导致驱动程序以拒绝扫描出使用这些设置的表面。 DXGI 进行缩放后尝试创建主没有旋转，而无需多重采样，或没有同时做出该决定。 DXGI 确定对扫描扩展功能的驱动程序的支持后，DXGI 创建主服务器和代理应用层，该驱动程序应该能够这些两个图面间切换。 DXGI 仍将接着将通过调用驱动程序的满足自动旋转或多级采样后台缓冲区的应用程序的请求[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数以从备份执行 bitblts 缓冲到代理面。 这些 bitblts 请求驱动程序来执行多重采样解析或旋转。 有关详细信息*BltDXGI*，请参阅**BltDXGI**参考页。

 

 





