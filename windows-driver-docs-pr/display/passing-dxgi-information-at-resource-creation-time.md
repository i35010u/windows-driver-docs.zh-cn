---
title: 创建资源时传递 DXGI 信息
description: 创建资源时传递 DXGI 信息
ms.assetid: d99fc77a-7192-4e45-852a-7a2ae87cc9a2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af50947aa02fb92a8b73742c43c36baaed8415b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829862"
---
# <a name="passing-dxgi-information-at-resource-creation-time"></a>创建资源时传递 DXGI 信息


当 Direct3D 版本10运行时在调用用户模式显示驱动程序的[**CreateResource （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)函数创建资源时，可以传递特定于 DXGI 的信息。 运行时可以在[**D3D10DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)结构的**pPrimaryDesc**成员中传递一个指向[**DXGI\_\_\_DDI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)的指针，以指定该资源可用作主资源（也就是说，可以将资源扫描到显示中。 仅当运行时还会将 D3D10\_\_DDI 设置为非 NULL 值时，运行时**才会将**D3D10DDIARG\_CREATERESOURCE 的**BindFlags**成员中\_存在位。

运行时可以在 DXGI 的**Flags**成员中指定 DXGI\_DDI\_主要\_可选标志\_DDI\_主\_DESC）通知用户模式显示驱动程序，驱动程序可以选择通过使用翻转样式的演示。 为了通知运行时，它不应使用反转样式演示文稿中的资源，驱动程序将 DXGI\_DDI\_主\_驱动程序\_标志，在 DXGI 的**DriverFlags**成员中不\_\_SCANOUT 标志。_ DDI\_主\_DESC。

如果驱动程序在[**CreateResource （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)调用中\_DDI 返回 DXGI\_PRIMARY\_驱动程序\_\_标志，以创建资源，则运行时将始终执行位块传输（bitblt）样式表示形式（而不是翻转样式的表示形式）。 如果图形硬件无法扫描给定资源类型的特定子集，则此功能很有用。 例如，图形硬件可能会也可能不能扫描多级采样后台缓冲区类型的资源。 此外，能否进一步扫描多级采样后台缓冲区可能会进一步依赖于图面的格式。 如果图形硬件无法扫描特定的多级采样格式，则用户模式显示驱动程序会在**DriverFlags**中将 DXGI\_DDI\_PRIMARY\_驱动程序\_标志\_没有\_的 SCANOUT 标志。此格式的资源的 DXGI\_DDI\_主\_DESC 的成员。

如果运行时未在 DXGI 的**Flags**成员中设置 DXGI\_DDI\_主要\_可选标志\_DDI\_主要\_DESC，以通知驱动程序在翻转样式表示形式，驱动程序仍可以返回 DXGI\_DDI\_ERR\_不支持的错误代码以及 DXGI\_DDI\_PRIMARY\_to [**CreateResource （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)。 驱动程序的*CreateResource （D3D10）* 传递 DXGI\_DDI\_ERR\_如果驱动程序无法扫描此类主副本，则调用[**PFNSETERRORCB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb)函数时不支持该函数。 返回 DXGI\_DDI\_ERR\_不受支持连同 DXGI\_DDI\_主\_驱动程序\_标志\_\_不会导致 DXGI interpose 表示路径中的代理表面在后台缓冲区和主表面之间。 在大小、多级采样和旋转方面，代理图面始终与主（扫描出）图面匹配。 此过程的第一步是为 DXGI 确定哪些采样或旋转设置导致驱动程序拒绝使用这些设置来扫描图面。 DXGI 通过以下方式来确定这一点：向后缩放，尝试创建不带旋转的主副本，无需进行多级采样，或不使用两者。 在 DXGI 确定驱动程序对扫描功能的支持后，DXGI 会创建主表面和代理面，驱动程序应能够在这两个曲面之间切换。 DXGI 仍会通过调用驱动程序的[**BltDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数来执行从后台缓冲区到代理表面的 bitblts，进而满足应用程序自动轮替或多级采样后台缓冲区的请求。 这些 bitblts 请求驱动程序执行多级（解析或旋转）。 有关*BltDXGI*的详细信息，请参阅**BltDXGI**参考页。

 

 





