---
title: 扩展格式感知要求
description: 扩展格式感知要求
ms.assetid: eab9c254-fca7-449d-a6cf-1b20d2e7173c
keywords:
- 扩展格式识别要求的 Direct3D 版本 10.1 WDK Windows 7 显示
- 扩展的格式的识别要求 WDK Windows 7 显示
- XR_BIAS WDK Windows 7 显示
- XR_BIAS WDK Windows 7 显示 PresentDXGI
- XR_BIAS WDK Windows 7 显示 BltDXGI
- 显示 PresentDXGI 和 XR_BIAS WDK Windows 7
- 显示 BltDXGI 和 XR_BIAS WDK Windows 7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f81c0837544feb8c612a09b31a73c934a3d2d36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363372"
---
# <a name="extended-format-aware-requirements"></a>扩展格式感知要求


本部分仅适用于 Windows 7 和更高版本的操作系统。

识别的格式进行了扩展的用户模式显示驱动程序保证返回准确的值从其[ **CheckFormatSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff539390)入口点函数的每种格式的表中[扩展格式的详细信息](details-of-the-extended-format.md)部分。 但是，驱动程序不一定支持每种格式。

支持扩展的格式中识别驱动程序隐式保证完全类型化后台缓冲区的该强制转换。

识别驱动程序隐式支持的所有 BGRX 和 BGRA 扩展格式中的表中定义设置的格式功能[扩展格式的详细信息](details-of-the-extended-format.md)部分。

扩展的格式中识别驱动程序隐式支持 BGRA 和 BGRA\_SRGB 扫描出中所述[BGRA 扫描扩展支持](bgra-scan-out-support.md)部分。

如果扩展的格式中识别驱动程序返回的任何一种新格式的任何支持位，它必须返回的所有所需的位中的表中[扩展格式的详细信息](details-of-the-extended-format.md)部分。 该驱动程序不能返回表中不需要任何位。

### <a name="span-idclaimingsupportunderdirect3dversion101spanspan-idclaimingsupportunderdirect3dversion101spanclaiming-support-under-direct3d-version-101"></a><span id="claiming_support_under_direct3d_version_10_1"></span><span id="CLAIMING_SUPPORT_UNDER_DIRECT3D_VERSION_10_1"></span>声明下 Direct3D 版本 10.1 的支持

Direct3D 10.1 和更高版本 DDIs 已更新以允许用户模式显示驱动程序，以声明的两个新版本的支持。 一个版本对应于想要支持功能级别 10.0，驱动程序，另一个版本对应于想要支持功能级别 10.1 的驱动程序。 新的版本定义如下：

```cpp
// D3D10.0 or D3D10.1 with extended format support (but not Windows 7 scheduling)
#define D3D10_0_x_DDI_BUILD_VERSION 10
#define D3D10_0_x_DDI_SUPPORTED ((((UINT64)D3D10_0_DDI_INTERFACE_VERSION) << 32) | (((UINT64)D3D10_0_x_DDI_BUILD_VERSION) << 16))
#define D3D10_1_x_DDI_BUILD_VERSION 10
#define D3D10_1_x_DDI_SUPPORTED ((((UINT64)D3D10_1_DDI_INTERFACE_VERSION) << 32) | (((UINT64)D3D10_1_x_DDI_BUILD_VERSION) << 16))
```

### <a name="span-idxrbiasandpresentdxgispanspan-idxrbiasandpresentdxgispanxrbias-and-presentdxgi"></a><span id="xr_bias_and_presentdxgi"></span><span id="XR_BIAS_AND_PRESENTDXGI"></span>XR\_偏置和 PresentDXGI

驱动程序不需要支持开窗存在 XR\_偏置资源通过调用其[ **PresentDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff569179)函数。 在运行时级别，这种情况下会受到限制。 与其他所有格式，驱动程序执行的 XR 全屏幕存在\_偏差通过翻转操作或位块传输 (bitblt) 操作中使用相同的源和目标资源。 没有拉伸或转换是必需的。

### <a name="span-idxrbiasandbltdxgispanspan-idxrbiasandbltdxgispanxrbias-and-bltdxgi"></a><span id="xr_bias_and_bltdxgi"></span><span id="XR_BIAS_AND_BLTDXGI"></span>XR\_偏置和 BltDXGI

Direct3D 运行时调用的驱动程序[ **BltDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff538252)函数以执行只对执行以下操作 XR\_偏差源资源：

-   复制到一个目标，它也是 XR\_偏差

-   未修改的源数据的副本

-   示例中的哪个点是可接受 stretch

-   旋转

因为 XR\_偏置不支持多个采样抗锯齿 (MSAA)，驱动程序不需要解决 XR\_偏置资源。

 

 





