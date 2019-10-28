---
title: 多平面覆盖支持
description: Windows 显示驱动程序模型（WDDM）1.3 和更高版本的驱动程序可以支持 Multiplane 覆盖。 此功能是从 Windows 8.1 开始的新功能。
ms.assetid: 8B2F5497-554D-4D4A-B44E-985A9F89143D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 376894a3d327542af472a13d242d1c0f23a6c1f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840540"
---
# <a name="multiplane-overlay-support"></a>多平面覆盖支持


Windows 显示驱动程序模型（WDDM）1.3 和更高版本的驱动程序可以支持 Multiplane 覆盖。 此功能是从 Windows 8.1 开始的新功能。

以下部分介绍如何在你的驱动程序中实现此功能。

## <a name="multiplane-overlay-functions-called-by-user-mode-display-drivers"></a>用户模式显示驱动程序调用的 Multiplane 覆盖函数

操作系统实现的所有用户模式 multiplane 覆盖函数。

| 函数 | 描述 |
|:--|:--|
|[pfnPresentMultiPlaneOverlayCb （D3D）](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentmultiplaneoverlaycb)|将源 multiplane 覆盖分配中的内容复制到目标分配。 可由 Windows 显示驱动程序模型（WDDM）1.3 或更高版本的用户模式显示驱动程序调用。|
|[pfnPresentMultiPlaneOverlayCb （DXGI）](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)|将源 multiplane 覆盖分配中的内容复制到目标分配。 可由 WDDM 1.3 或更高版本的用户模式显示驱动程序调用。|

## <a name="multiplane-overlay-functions-implemented-by-the-user-mode-driver"></a>用户模式驱动程序实现的 Multiplane 覆盖函数

本部分包含的函数必须实现 Windows 显示驱动程序模型（WDDM）1.3 和更高版本的用户模式显示驱动程序才能支持 multiplane 覆盖。

驱动程序在对用户模式显示驱动程序的特定于适配器的[CreateDevice （D3D10）](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数的调用中，通过[DXGI1_3_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)结构的成员向 DXGI multiplane 叠加函数提供指针。 有关详细信息，请参阅[支持 DXGI DDI](supporting-the-dxgi-ddi.md)。

驱动程序在对驱动程序的[CreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)函数的调用中通过[D3DDDI_DEVICEFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)结构的成员提供指向 Microsoft Direct3D multiplane 覆盖函数的指针。

为了支持 multiplane 覆盖，用户模式驱动程序必须实现的所有函数。

| 函数 | 描述 |
|:--|:--|
|[pfnCheckMultiPlaneOverlaySupport （D3D）](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkmultiplaneoverlaysupport)| 由 Direct3D 运行时调用，用于检查有关 multiplane 叠加硬件支持的详细信息。|
|[pfnCheckMultiPlaneOverlaySupport （DXGI）](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)| 由 Microsoft DirectX 图形基础结构（DXGI）运行时调用，用于检查有关 multiplane 叠加硬件支持的详细信息。|
|[pfnGetMultiPlaneOverlayCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)| 由 DXGI 运行时调用，用于请求用户模式显示驱动程序获取基本覆盖面功能。 选择性地由 WDDM 1.3 和更高版本的用户模式显示驱动程序实现。|
|[pfnGetMultiplaneOverlayGroupCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)| 由 DXGI 运行时调用，用于请求用户模式显示驱动程序获取一组覆盖面功能。 选择性地由 WDDM 1.3 和更高版本的用户模式显示驱动程序实现。|
|[pfnPresentMultiplaneOverlay （D3D）](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_presentmultiplaneoverlay)| 由 Direct3D 运行时调用，用于通知用户模式显示驱动程序，应用程序已完成呈现，并请求驱动程序通过复制或翻转或驱动程序执行填充颜色操作来显示源图面。 必须由支持 multiplane 覆盖的 WDDM 1.3 或更高版本驱动程序实现。|
|[pfnPresentMultiplaneOverlay （DXGI）](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)| 由 DXGI 运行时调用，用于通知用户模式显示驱动程序，应用程序已完成呈现，并请求驱动程序通过复制或翻转或驱动程序执行填充颜色操作来显示源图面。 必须由支持 multiplane 覆盖的 WDDM 1.3 或更高版本驱动程序实现。|
 
## <a name="multiplane-overlay-user-mode-structures-and-enumerations"></a>Multiplane 覆盖用户模式结构和枚举

与 multiplane 覆盖设备驱动程序接口（DDIs）一起使用的所有用户模式结构和枚举。

| DDI | 描述 |
|:--|:--|
|[D3DDDI_MULTIPLANE_ALLOCATION_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_allocation_info)|指定有关 multiplane 覆盖分配的信息。|
|[D3DDDI_MULTIPLANE_OVERLAY_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_multiplane_overlay_attributes)| 由用户模式显示驱动程序用来指定覆盖面属性。|
|[D3DDDI_MULTIPLANE_OVERLAY_BLEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_blend)| 标识要对叠加平面执行的混合操作。|
|[D3DDDI_MULTIPLANE_OVERLAY_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_caps)| 由用户模式显示驱动程序用来指定覆盖面功能。|
|[D3DDDI_MULTIPLANE_OVERLAY_FEATURE_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_feature_caps)| 标识覆盖功能。|
|[D3DDDI_MULTIPLANE_OVERLAY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_flags)| 标识要对叠加平面执行的翻转操作。|
|[D3DDDI_MULTIPLANE_OVERLAY_GROUP_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_group_caps)| 由用户模式显示驱动程序用来指定一组覆盖面功能。|
|[D3DDDI_MULTIPLANE_OVERLAY_GROUP_CAPS_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_group_caps_input)| 指定有关 multiplane 覆盖功能组的信息。|
|[D3DDDI_MULTIPLANE_OVERLAY_STRETCH_QUALITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_stretch_quality)| 标识当硬件拉伸或收缩 multiplane 覆盖数据时应执行的筛选进程。
|[D3DDDI_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_video_frame_format)|标识覆盖平面的视频帧格式。 仅支持 D3DDDI_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT_PROGRESSIVE 值。|
|[D3DDDI_MULTIPLANE_OVERLAY_YCbCr_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_ycbcr_flags)| 标识描述 multiplane 覆盖的 YUV 范围和转换信息。|
|[D3DDDI_PRESENT_MULTIPLANE_OVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_present_multiplane_overlay)| 指定要显示的覆盖面。|
|[D3DDDIARG_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_checkmultiplaneoverlaysupport)| 在对 pfnCheckMultiPlaneOverlaySupport （D3D）函数的调用中使用，以检查有关 multiplane 叠加硬件支持的详细信息。|
|[D3DDDIARG_PRESENTMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_presentmultiplaneoverlay)| 指定要显示的 multiplane 覆盖资源。|
|[D3DDDICB_PRESENTMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicb_presentmultiplaneoverlay)| 描述内容复制到和的 multiplane 覆盖分配。|
 
## <a name="multiplane-overlay-kernel-mode-driver-implemented-functions"></a>Multiplane 覆盖内核模式驱动程序实现的函数

显示微型端口驱动程序实现的所有 multiplane 覆盖功能。

|函数|描述|
|:--|:--|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport)| 由 Microsoft DirectX 图形内核子系统调用，用于检查 multiplane 重叠硬件支持的详细信息。|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT3](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport3)| 调用以下新函数来确定是否支持特定的多平面覆盖配置。|
|[DXGKDDI_GETMULTIPLANEOVERLAYCAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getmultiplaneoverlaycaps)| 调用以检索 multiplane 覆盖功能。 需要支持多个平面的任何 WDDM 2.2 驱动程序都需要对此 DDI 的支持。|
|[DXGKDDI_POSTMULTIPLANEOVERLAYPRESENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_postmultiplaneoverlaypresent)| 在新的多平面覆盖配置生效后调用，使驱动程序能够优化硬件状态。 可选，适用于 Windows 显示器驱动程序模型（WDDM）2.0 或更高版本的支持多平面覆盖的驱动程序。|
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY3](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay3)|调用以更改正在显示的覆盖配置。|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport2)|调用 DxgkDdiCheckMultiPlaneOverlaySupport2 来确定是否支持特定的多平面覆盖配置。 |
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)|设置包含与特定视频现有源相关联的多个表面的地址，包括桌面窗口管理器（DWM）的存在。 此函数用于向屏幕显示多个表面（包括 DWM 的存在）。|
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay2)| 调用 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 来更改正在显示的覆盖配置。|

## <a name="multiplane-overlay-kernel-mode-structures"></a>Multiplane 叠加内核模式结构

显示微型端口驱动程序使用的所有结构。

|结构|描述|
|:--|:--|
|[DXGK_CHECK_MULTIPLANE_OVERLAY_SUPPORT_PLANE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_check_multiplane_overlay_support_plane)| 指定硬件为 multiplane 叠加提供的支持属性。|
|[DXGK_CHECK_MULTIPLANE_OVERLAY_SUPPORT_RETURN_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-dxgk_check_multiplane_overlay_support_return_info)| 指定对 multiplane 叠加硬件支持的限制。|
|[DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_attributes)| 由显示微型端口驱动程序用来指定覆盖面属性。|
|[DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_attributes2)|显示微型端口驱动程序使用 DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES2 来指定覆盖面属性。 |
|[DXGK_MULTIPLANE_OVERLAY_BLEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_blend)| 标识要对叠加平面执行的混合操作。|
|[DXGK_MULTIPLANE_OVERLAY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_flags)| 标识要对叠加平面执行的翻转操作。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane)| 指定要在对 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay 函数的调用中显示的覆盖面。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane2)|DXGK_MULTIPLANE_OVERLAY_PLANE2 用于 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 函数来指定要显示的覆盖面。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE_WITH_SOURCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane_with_source)|DXGK_MULTIPLANE_OVERLAY_PLANE_WITH_SOURCE 介绍多平面覆盖面属性、分配和视频显示网络源标识号。|
|[DXGK_MULTIPLANE_OVERLAY_VSYNC_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_vsync_info)|指定在 VSync 间隔期间显示的覆盖面。|
|[DXGK_MULTIPLANE_OVERLAY_YCbCr_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_ycbcr_flags)|标识描述 multiplane 覆盖的 YUV 范围和转换信息。|
|[DXGK_PRESENTMULTIPLANEOVERLAYINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentmultiplaneoverlayinfo)|指定有关 VidPN 输入的信息和要显示的覆盖面。|
|[DXGK_PRESENTMULTIPLANEOVERLAYLIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentmultiplaneoverlaylist)|指定要在对 DxgkDdiPresent 函数的调用中显示的覆盖面。|
|[DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_checkmultiplaneoverlaysupport)|在对 DxgkDdiCheckMultiPlaneOverlaySupport 函数的调用中使用，以检查有关 multiplane 叠加硬件支持的详细信息。|
|[DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_checkmultiplaneoverlaysupport2)|DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT2 传递给 DxgkDdiCheckMultiPlaneOverlaySupport2 函数，以确定是否支持特定的多平面覆盖配置。|
|[DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay)|包含 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay 函数的参数。|
|[DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay2)|DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2 传递给 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 函数以更改正在显示的覆盖配置。|
 

## <a name="multiplane-overlay-kernel-mode-enumerations"></a>Multiplane 叠加内核模式枚举

显示微型端口驱动程序使用的所有枚举。

| 枚举 | 描述 |
|:--|:--|
|[DXGK_MULTIPLANE_OVERLAY_STEREO_FLIP_MODE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stereo_flip_mode)|标识覆盖平面的立体声翻转模式。 仅支持 DXGK_MULTIPLANE_OVERLAY_STEREO_FLIP_NONE 值。 |
|[DXGK_MULTIPLANE_OVERLAY_STEREO_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stereo_format)|标识覆盖平面的立体声表示格式。 仅支持 DXGK_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO 值。|
|[DXGK_MULTIPLANE_OVERLAY_STRETCH_QUALITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stretch_quality)|标识当硬件拉伸或收缩 multiplane 覆盖数据时应执行的筛选进程。|
|[DXGK_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_video_frame_format)|标识覆盖平面的视频帧格式。 仅支持 DXGK_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT_PROGRESSIVE 值。|
 

此用户模式枚举常量值支持 multiplane 覆盖，是 Windows 8.1 的新的：

-   [**D3DDDICAPS\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)（**D3DDDICAPS\_获取\_MULTIPLANE\_覆盖\_\_大写**常量值）

 

 





