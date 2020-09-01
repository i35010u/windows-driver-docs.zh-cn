---
title: DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
description: DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
ms.assetid: 2aef590f-2328-4175-ab60-c72b1fd83db7
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
- 扩展格式 WDK Windows 7 显示，DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
- DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf86af5461020f6fd97b65508a8d5c501d1b5884
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065468"
---
# <a name="dxgi_format_r10g10b10_xr_bias_a2_unorm"></a>DXGI \_ FORMAT \_ R10G10B10 \_ XR \_ 偏向 \_ A2 \_ UNORM


本部分仅适用于 Windows 7 及更高版本的操作系统。

DXGI \_ format \_ R10G10B10 \_ XR \_ 偏向 \_ A2 \_ UNORM FORMAT 要求应用程序注意与格式相关的数据的偏向特性。 正如以下各节中的转换规则所示，着色器必须知道 XR 偏量， \_ 并且必须对从读取或写入到 DXGI 格式的任何数据进行缩放 \_ \_ R10G10B10 \_ XR \_ 偏向 \_ A2 \_ UNORM 格式。

扫描硬件必须能够应用偏向和缩放。

DXGI \_ FORMAT \_ R10G10B10 \_ XR \_ 偏向 \_ A2 \_ UNORM FORMAT 仅具有显示扫描、CPU 锁定和在位布局中强制转换的资源特性。 因此，应用程序通常会创建一个格式为 DXGI 格式 R10G10B10A2 的呈现目标视图 \_ \_ \_ \* 。

若要获得完整功能，显示的微型端口驱动程序必须支持 XR \_ 偏向作为显示格式。 已将新的 D3DDDIFMT \_ A2B10G10R10 \_ XR \_ 偏量值添加到 [**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat) 枚举，以获得 XR \_ 偏向支持。

 

