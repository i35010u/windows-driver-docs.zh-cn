---
title: DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
description: DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
ms.assetid: 2aef590f-2328-4175-ab60-c72b1fd83db7
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示 DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
- 扩展的格式 WDK Windows 7 显示，DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
- DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM WDK Windows 7 display
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a3014a8650c368c7d2a2b88596bb745c46fb378
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338670"
---
# <a name="dxgiformatr10g10b10xrbiasa2unorm"></a>DXGI\_FORMAT\_R10G10B10\_XR\_BIAS\_A2\_UNORM


本部分仅适用于 Windows 7 和更高版本的操作系统。

DXGI\_格式\_R10G10B10\_XR\_偏差\_A2\_UNORM 格式要求应用程序需要注意的有偏差为格式相关的数据的性质。 着色器可以看出从以下各节中的转换规则，必须了解 XR\_偏置，必须在读取或写入到 DXGI 的任何数据上执行其自己的偏差和规模\_格式\_R10G10B10\_XR\_偏差\_A2\_UNORM 格式。

扫描扩展硬件必须能够将应用的偏差和小数位数。

DXGI\_格式\_R10G10B10\_XR\_偏差\_A2\_UNORM 格式具有显示扫描扩展、 可锁定，CPU 和"强制转换位布局中的"资源属性。 因此，若要呈现到的资源，应用程序通常会创建呈现目标视图的 DXGI 格式\_格式\_R10G10B10A2\_\*。

获取完整功能，显示微型端口驱动程序必须支持 XR\_偏差为显示格式。 新 D3DDDIFMT\_A2B10G10R10\_XR\_偏置值已添加到[ **D3DDDIFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff544312)枚举为 XR\_偏差的支持。

 

 





