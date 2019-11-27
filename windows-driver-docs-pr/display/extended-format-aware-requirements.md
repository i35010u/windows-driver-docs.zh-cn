---
title: 扩展格式感知要求
description: 扩展格式感知要求
ms.assetid: eab9c254-fca7-449d-a6cf-1b20d2e7173c
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，可扩展格式感知要求
- 扩展格式感知要求 WDK Windows 7 显示
- XR_BIAS WDK Windows 7 显示
- XR_BIAS WDK Windows 7 显示，PresentDXGI
- XR_BIAS WDK Windows 7 显示，BltDXGI
- PresentDXGI 和 XR_BIAS WDK Windows 7 显示
- BltDXGI 和 XR_BIAS WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3a7ae4eaf7c5c41f768be5b2b9d09caba0ed3f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838944"
---
# <a name="extended-format-aware-requirements"></a>扩展格式感知要求


本部分仅适用于 Windows 7 及更高版本的操作系统。

用户模式显示扩展了扩展格式的驱动程序，可确保在 "扩展格式[](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport) " 部分的[详细信息](details-of-the-extended-format.md)中，为表中的每种格式返回准确值。 但是，驱动程序不一定支持每种格式。

可扩展格式感知驱动程序隐式保证支持强制转换完全类型的后台缓冲区。

扩展格式感知驱动程序隐式支持 BGRX 和 BGRA 格式，这些格式与 "扩展格式" 部分的[详细信息](details-of-the-extended-format.md)中的表中定义的功能相同。

扩展格式感知驱动程序隐式支持 BGRA 和 BGRA\_SRGB 扫描，如[BGRA 扫描支持](bgra-scan-out-support.md)部分所述。

如果扩展格式感知驱动程序为任何新格式返回任何支持位，则必须在 "扩展格式" 部分的[详细信息](details-of-the-extended-format.md)中返回表中所需的所有位。 驱动程序无法返回表中不需要的任何位。

### <a name="span-idclaiming_support_under_direct3d_version_10_1spanspan-idclaiming_support_under_direct3d_version_10_1spanclaiming-support-under-direct3d-version-101"></a><span id="claiming_support_under_direct3d_version_10_1"></span><span id="CLAIMING_SUPPORT_UNDER_DIRECT3D_VERSION_10_1"></span>Direct3D 10.1 版下的申报支持

Direct3D 10.1 和更高版本的 DDIs 已更新，以允许用户模式显示驱动程序声明支持两个新版本。 一个版本对应于要支持功能级别10.0 的驱动程序，另一个版本对应于要支持功能级别10.1 的驱动程序。 下面是新的版本定义：

```cpp
// D3D10.0 or D3D10.1 with extended format support (but not Windows 7 scheduling)
#define D3D10_0_x_DDI_BUILD_VERSION 10
#define D3D10_0_x_DDI_SUPPORTED ((((UINT64)D3D10_0_DDI_INTERFACE_VERSION) << 32) | (((UINT64)D3D10_0_x_DDI_BUILD_VERSION) << 16))
#define D3D10_1_x_DDI_BUILD_VERSION 10
#define D3D10_1_x_DDI_SUPPORTED ((((UINT64)D3D10_1_DDI_INTERFACE_VERSION) << 32) | (((UINT64)D3D10_1_x_DDI_BUILD_VERSION) << 16))
```

### <a name="span-idxr_bias_and_presentdxgispanspan-idxr_bias_and_presentdxgispanxr_bias-and-presentdxgi"></a><span id="xr_bias_and_presentdxgi"></span><span id="XR_BIAS_AND_PRESENTDXGI"></span>XR\_偏向和 PresentDXGI

驱动程序无需支持通过对其[**PresentDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数的调用来支持 XR\_偏向资源的有窗口显示。 在运行时级别限制这些情况。 与所有其他格式一样，驱动程序通过使用相同源和目标资源的翻转操作或位块传输（bitblt）操作来执行\_XR 的全屏显示。 无需 stretch 或转换。

### <a name="span-idxr_bias_and_bltdxgispanspan-idxr_bias_and_bltdxgispanxr_bias-and-bltdxgi"></a><span id="xr_bias_and_bltdxgi"></span><span id="XR_BIAS_AND_BLTDXGI"></span>XR\_偏向和 BltDXGI

Direct3D 运行时调用驱动程序的[**BltDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数，以便仅对 XR\_偏向源资源执行以下操作：

-   指向还 XR\_偏向的目标的副本

-   未修改源数据的副本

-   可接受点样本的 stretch

-   旋转

由于 XR\_偏差不支持多个样本抗锯齿（MSAA），因此不需要驱动程序来解析 XR\_偏向资源。

 

 





