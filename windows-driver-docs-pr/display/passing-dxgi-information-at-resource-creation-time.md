---
title: 创建资源时传递 DXGI 信息
description: 创建资源时传递 DXGI 信息
ms.assetid: d99fc77a-7192-4e45-852a-7a2ae87cc9a2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a01b7c3ac1a563d629c984a45b92c178c7062af
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064684"
---
# <a name="passing-dxgi-information-at-resource-creation-time"></a>创建资源时传递 DXGI 信息


当 Direct3D 版本10运行时在调用用户模式显示驱动程序的 [**CreateResource (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource) 函数以创建资源时，可以传递特定于 DXGI 的信息。 运行时可以将指针传递到[**D3D10DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)结构的**PPrimaryDesc**成员中的[**DXGI \_ DDI \_ 主要 \_ DESC**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)结构，以指定该资源可用作主 (，即，可将资源扫描到显示) 。 仅当运行**pPrimaryDesc**时还 \_ \_ \_ 在 D3D10DDIARG CREATERESOURCE 的**BindFlags**成员中设置 D3D10 DDI BIND PPrimaryDesc 时，运行时才将设置为非 NULL 值 \_ 。

运行时可以 \_ \_ \_ 在 "dxgi Ddi 主要 DESC **标志** " 成员中指定 dxgi ddi 主要可选标志 \_ \_ \_ ，以通知用户模式显示驱动程序，驱动程序可以通过使用反转样式演示文稿中的资源来进行选择。 若要通知运行时它不应使用反转样式演示文稿中的资源，驱动程序会在 \_ \_ \_ \_ \_ \_ **DriverFlags** dxgi \_ ddi 主要 DESC 的 DriverFlags 成员中设置 \_ dxgi ddi 主驱动程序标志 NO SCANOUT 标志 \_ 。

如果驱动程序返回 DXGI \_ DDI \_ 主 \_ 驱动 \_ 程序 \_ 标志 \_ ，而 [**CreateResource (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource) 调用来创建资源，则运行时将始终执行位块传输 (bitblt) 样式表示形式 (而不是在资源为表示形式的源时) 翻转样式的表示形式。 如果图形硬件无法扫描给定资源类型的特定子集，则此功能很有用。 例如，图形硬件可能会也可能不能扫描多级采样后台缓冲区类型的资源。 此外，能否进一步扫描多级采样后台缓冲区可能会进一步依赖于图面的格式。 如果图形硬件无法扫描特定的多级采样格式，则用户模式显示驱动程序会 \_ \_ \_ \_ \_ \_ **DriverFlags**在 \_ \_ \_ 具有此格式的资源的 dxgi ddi 主要 DESC 的 DriverFlags 成员中设置 dxgi ddi 主驱动程序标志 NO SCANOUT 标志。

如果运行时未 \_ \_ \_ 在 dxgi ddi 主要 DESC 的 **FLAGS** 成员中设置 dxgi ddi 主要可选 \_ 标志 \_ \_ 来通知驱动程序，可能是因为选择不使用在翻转样式的演示中使用资源，则驱动程序仍可以返回 dxgi \_ ddi \_ 错误 \_ 代码，以及 \_ \_ \_ \_ \_ \_ 从 [**CreateResource (D3D10) **](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)调用的 dxgi ddi 主驱动程序标志 NO SCANOUT 标志。 如果驱动程序无法扫描此类主副本，则驱动程序的 *CreateResource (D3D10) * 传递 \_ \_ \_ 对 [**pfnSetErrorCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_seterror_cb) 函数的调用中不支持的 DXGI DDI ERR。 返回 \_ \_ \_ 不受支持的 dxgi DDI ERR 以及 dxgi \_ ddi \_ 主 \_ 驱动程序 \_ 标志 \_ NO \_ SCANOUT 导致 DXGI 在后端缓冲区与主表面之间的表示路径中 interpose 代理图面。 在大小、多级采样和旋转方面，代理图面总是与) 图面上 (扫描的主匹配。 此过程的第一步是为 DXGI 确定哪些采样或旋转设置导致驱动程序拒绝使用这些设置来扫描图面。 DXGI 通过以下方式来确定这一点：向后缩放，尝试创建不带旋转的主副本，无需进行多级采样，或不使用两者。 在 DXGI 确定驱动程序对扫描功能的支持后，DXGI 会创建主表面和代理面，驱动程序应能够在这两个曲面之间切换。 DXGI 仍会通过调用驱动程序的 [**BltDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) 函数来执行从后台缓冲区到代理表面的 bitblts，进而满足应用程序自动轮替或多级采样后台缓冲区的请求。 这些 bitblts 请求驱动程序执行多级（解析或旋转）。 有关 *BltDXGI*的详细信息，请参阅 **BltDXGI** 参考页。

 

