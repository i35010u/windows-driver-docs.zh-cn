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
ms.openlocfilehash: 5ad036b530d8443c05fd4de31ee01976a12d26d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838974"
---
# <a name="dxgi_format_r10g10b10_xr_bias_a2_unorm"></a>DXGI\_格式\_R10G10B10\_XR\_偏移\_A2\_UNORM


本部分仅适用于 Windows 7 及更高版本的操作系统。

DXGI\_格式\_R10G10B10\_XR\_偏向\_A2\_UNORM 格式要求应用程序知道与格式相关的数据的偏向特性。 正如以下各节中的转换规则所示，着色器必须了解 XR\_偏差，并且必须对读取或写入到 DXGI\_格式的任何数据执行自己的偏移，并对其进行缩放\_R10G10B10\_XR\_偏向\_A2\_UNORM 格式。

扫描硬件必须能够应用偏向和缩放。

DXGI\_格式\_R10G10B10\_XR\_偏移\_A2\_UNORM 格式仅具有 "在位布局中显示扫描"、"CPU 锁定" 和 "强制转换" 资源特性。 因此，若要呈现到资源，应用程序通常会创建格式为 DXGI\_格式的呈现目标视图\_R10G10B10A2\_\*。

若要获得完整功能，显示器微型端口驱动程序必须支持 XR\_偏向格式的显示格式。 已将新的 D3DDDIFMT\_A2B10G10R10\_XR\_偏向值添加到[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举中，以便 XR\_偏向支持。

 

 





