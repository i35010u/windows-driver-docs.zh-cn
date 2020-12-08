---
title: 同时渲染到多个目标
description: 同时渲染到多个目标
keywords:
- 呈现多个目标 WDK DirectX 9。0
- 多个呈现目标 WDK DirectX 9。0
- 同时呈现目标 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eec193478df96de74bc4a2afe73847419458f183
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783983"
---
# <a name="rendering-to-multiple-targets-simultaneously"></a>同时渲染到多个目标


## <span id="ddk_rendering_to_multiple_targets_simultaneously_gg"></span><span id="DDK_RENDERING_TO_MULTIPLE_TARGETS_SIMULTANEOUSLY_GG"></span>


如果驱动程序指示其设备支持多个呈现目标，则 DirectX 9.0 版本驱动程序可以同时呈现到多个目标。 为了指明设备支持的呈现器目标数，驱动程序在 D3DCAPS9 结构的 **NumSimultaneousRTs** 成员中设置此数字。 如果只支持向单个目标进行呈现，则驱动程序必须将此数字设置为1。 驱动程序将返回 D3DCAPS9 结构，以响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

多呈现器目标组中的呈现目标必须具有相同的维度，但可以具有不同的表面格式。

\_如果应用程序请求为多个组中的一个呈现器目标设置颜色缓冲区，则驱动程序将接收 D3DDP2OP SETRENDERTARGET2 操作代码。

如果 DirectX 9.0 驱动程序支持同时呈现到多个目标，则它必须支持某些功能，并可以支持扩展功能。 以下主题介绍了这些必需功能和可选功能：

[多个渲染器目标的必需功能](required-features-for-multiple-render-targets.md)

[多个渲染器目标的可选功能](optional-features-for-multiple-render-targets.md)

 

 





