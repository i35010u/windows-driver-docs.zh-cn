---
title: 支持独立于路径的旋转
description: 从 Windows 8.1 更新开始，操作系统支持按横向显示的克隆，第一种方式是以最大的可能分辨率进行显示。
ms.assetid: 136CEDA5-2839-4E6E-A032-1A9222C769C6
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8943554eb1bbae99acffbc0f814a16cebe0017e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829383"
---
# <a name="span-iddisplaysupporting_path-independent_rotationspansupporting-path-independent-rotation"></a><span id="display.supporting_path-independent_rotation"></span>支持独立于路径的旋转


从 Windows 8.1 更新开始，操作系统支持按横向显示的克隆，第一种方式是以最大的可能分辨率进行显示。 显示微型端口驱动程序必须在[**D3DKMDT\_VIDPN\_存在\_路径**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)中设置正确的偏移量值，\_旋转\_*主要克隆路径*和*辅助克隆路径*的支持结构，如在[支持显示微型端口驱动程序](supporting-rotation-in-a-display-miniport-driver.md)中的旋转中进行了介绍。

这些设备驱动程序接口（DDIs）是 Windows 8.1 更新中的新界面：

-   D3DKMDT_VPPR_GET_CONTENT_ROTATION
-   D3DKMDT_VPPR_GET_CONTENT_ROTATION_PART
-   D3DKMDT_VPPR_GET_OFFSET_ROTATION

Windows 8.1 更新中更新了这些 DDIs：

-   [**D3DKMDT\_VIDPN\_提供\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)

-   [**D3DKMDT\_VIDPN\_提供\_路径\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)

## <a name="span-idcloning_a_portrait-first_devicespanspan-idcloning_a_portrait-first_devicespanspan-idcloning_a_portrait-first_devicespancloning-a-portrait-first-device"></a><span id="Cloning_a_portrait-first_device"></span><span id="cloning_a_portrait-first_device"></span><span id="CLONING_A_PORTRAIT-FIRST_DEVICE"></span>克隆纵向第一台设备


当请求将纵向设备的驱动程序克隆到横向第一台监视器时，它应报告与主要克隆路径中的解决方案匹配的源模式（*x*，*y*）分辨率。 然后，辅助克隆路径可以支持90和270度的偏移值（[**D3DKMDT\_VIDPN\_提供\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)。**Offset90**或。**Offset270**为**TRUE**。 因此，当使用[**D3DKMDT\_vidpn 提交 vidpn 时\_存在\_路径\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)枚举值指示90或270度的偏移量，这意味着（*x*，*y*）分辨率在此特定路径。

默认情况下，操作系统将辅助克隆路径选为内部显示面板。 如果内部面板为纵向，则操作系统需要[**D3DKMDT\_VIDPN\_提供\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)。要在此路径上设置的**Offset270** ，以便在横向模式下显示在内部显示面板上。 对于辅助克隆路径中的第一个横向外部监视器，操作系统期望驱动程序支持**D3DKMDT\_VIDPN\_提供\_路径\_旋转\_支持**。**Offset90**，尽管这可能是罕见情况。

## <a name="span-idexample_clone_scenariosspanspan-idexample_clone_scenariosspanspan-idexample_clone_scenariosspanexample-clone-scenarios"></a><span id="Example_clone_scenarios"></span><span id="example_clone_scenarios"></span><span id="EXAMPLE_CLONE_SCENARIOS"></span>示例克隆方案


下面是典型的方案，其中使用纯分辨率800（宽度） x 1280 像素（高）的纵向第一台设备在克隆模式下连接到高度为1080像素的横向电视。 该驱动程序会将此信息报告给操作系统：

<span id="source_mode"></span><span id="SOURCE_MODE"></span>源模式  
1280 x 800

<span id="TV_target_mode"></span><span id="tv_target_mode"></span><span id="TV_TARGET_MODE"></span>电视目标模式  
1920 x 1080 （纵横比保留缩放）

<span id="device_target_mode"></span><span id="DEVICE_TARGET_MODE"></span>设备目标模式  
800 x 1280 （标识缩放）

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>主要克隆路径（电视）  
驱动程序仅支持[ **\_VIDPN\_提供\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)。**Offset0**，以及正常旋转支持

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>辅助克隆路径（设备）  
驱动程序仅支持[ **\_VIDPN\_提供\_路径\_旋转\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation_support)。**Offset270**，以及正常旋转支持

<span></span>  

然后，对[*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)函数的调用将从[**D3DKMDT\_VIDPN\_提供\_路径\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)枚举中返回这些路径设置：

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>主要克隆路径（电视）  
**D3DKMDT\_VPPR\_标识**

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>辅助克隆路径（设备）  
**D3DKMDT\_VPPR\_标识\_OFFSET270**

操作系统期望驱动程序将所提供的内容旋转270度。

如果在 "**显示**控制面板" 的 "**方向**" 下拉框中，用户选择 "**横向" （翻转）** 选项，则对[*DxgkDdiCommitVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn)函数的调用将从 D3DKMDT 中返回这些路径设置[ **\_VIDPN\_提供\_路径\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_vidpn_present_path_rotation)枚举：

<span id="primary_clone_path__TV_"></span><span id="primary_clone_path__tv_"></span><span id="PRIMARY_CLONE_PATH__TV_"></span>主要克隆路径（电视）  
**D3DKMDT\_VPPR\_ROTATE180**

<span id="secondary_clone_path__device_"></span><span id="SECONDARY_CLONE_PATH__DEVICE_"></span>辅助克隆路径（设备）  
**D3DKMDT\_VPPR\_ROTATE180\_OFFSET270**

如果桌面窗口管理器（DWM）已经旋转了180度的内容，则驱动程序仍然必须在辅助克隆路径中将其旋转另一个270度。 否则，驱动程序必须为设备旋转180度的电视度和90度。 请注意，若要旋转内容，驱动程序必须将 DXGK 的**旋转**成员设置为[ **\_的 PRESENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentflags)结构。

 

 





