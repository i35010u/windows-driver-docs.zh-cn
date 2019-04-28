---
title: 多平面覆盖支持
description: Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序可以支持 multiplane 覆盖。 此功能是从 Windows 8.1 新增功能。
ms.assetid: 8B2F5497-554D-4D4A-B44E-985A9F89143D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23daa66180396b6b4a65458a13a122e977777db5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345615"
---
# <a name="multiplane-overlay-support"></a>多平面覆盖支持


Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序可以支持 multiplane 覆盖。 此功能是从 Windows 8.1 新增功能。

以下部分介绍如何在您的驱动程序中实现此功能。

## <a name="multiplane-overlay-functions-called-by-user-mode-display-drivers"></a>Multiplane 覆盖函数所调用的用户模式显示驱动程序

操作系统实现的所有用户模式下 multiplane 覆盖函数。

| 函数 | 描述 |
|:--|:--|
|[pfnPresentMultiPlaneOverlayCb (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentmultiplaneoverlaycb)|将内容从源 multiplane 覆盖分配给目标分配。 可由 Windows 显示驱动程序模型 (WDDM) 1.3 或更高版本的用户模式显示驱动程序调用。|
|[pfnPresentMultiPlaneOverlayCb (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/nc-dxgiddi-pfnddxgiddi_present_multiplane_overlaycb)|将内容从源 multiplane 覆盖分配给目标分配。 可以通过 WDDM 1.3 或更高版本的用户模式显示驱动程序调用。|

## <a name="multiplane-overlay-functions-implemented-by-the-user-mode-driver"></a>Multiplane 覆盖由用户模式驱动程序实现的函数

本部分包含 Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的用户模式显示驱动程序必须实现为了支持 multiplane 覆盖的函数。

驱动程序提供的成员通过 DXGI multiplane 覆盖函数的指针[DXGI1_3_DDI_BASE_FUNCTIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)结构对用户模式显示驱动程序的调用中的特定于适配器的[CreateDevice(D3D10)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。 有关详细信息，请参阅[支持 DXGI DDI](supporting-the-dxgi-ddi.md)。

驱动程序提供的成员通过 Microsoft Direct3D multiplane 覆盖函数的指针[D3DDDI_DEVICEFUNCS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs)驱动程序的调用中的结构[CreateDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)函数。

用户模式驱动程序必须实现为了支持 multiplane 覆盖层的所有函数。

| 函数 | 描述 |
|:--|:--|
|[pfnCheckMultiPlaneOverlaySupport (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkmultiplaneoverlaysupport)| 调用由 Direct3D 运行时，若要检查有关 multiplane 叠加的硬件支持的详细信息。|
|[pfnCheckMultiPlaneOverlaySupport (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)| 由要检查的详细信息的 multiplane 叠加硬件支持的 Microsoft DirectX 图形基础结构 (DXGI) 运行时调用。|
|[pfnGetMultiPlaneOverlayCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)| 由 DXGI 运行时调用，以请求用户模式显示驱动程序会获得基本覆盖平面功能。 （可选） 通过 WDDM 1.3 和更高版本的用户模式显示驱动程序实现。|
|[pfnGetMultiplaneOverlayGroupCaps](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)| DXGI 运行时调用，以请求用户模式显示驱动程序 get 覆盖平面功能的组。 （可选） 通过 WDDM 1.3 和更高版本的用户模式显示驱动程序实现。|
|[pfnPresentMultiplaneOverlay (D3D)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_presentmultiplaneoverlay)| 调用由 Direct3D 运行时，通知用户模式显示驱动程序，应用程序已完成呈现和请求的驱动程序通过复制或翻转显示源图面或驱动程序执行颜色填充操作。 必须通过 WDDM 1.3 或更高版本的驱动程序支持 multiplane 覆盖层的实现。|
|[pfnPresentMultiplaneOverlay (DXGI)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)| DXGI 运行时调用，以通知用户模式显示驱动程序，应用程序已完成呈现和请求的驱动程序通过复制或翻转显示源图面或驱动程序执行颜色填充操作。 必须通过 WDDM 1.3 或更高版本的驱动程序支持 multiplane 覆盖层的实现。|
 
## <a name="multiplane-overlay-user-mode-structures-and-enumerations"></a>Multiplane 覆盖用户模式下结构和枚举

所有用户模式下结构和与 multiplane 覆盖设备驱动程序接口 (DDIs) 一起使用的枚举。

| DDI | 描述 |
|:--|:--|
|[D3DDDI_MULTIPLANE_ALLOCATION_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_allocation_info)|指定有关 multiplane 覆盖分配的信息。|
|[D3DDDI_MULTIPLANE_OVERLAY_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_multiplane_overlay_attributes)| 由用户模式显示驱动程序用于指定叠加平面特性。|
|[D3DDDI_MULTIPLANE_OVERLAY_BLEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_blend)| 标识要覆盖平面上执行混合操作。|
|[D3DDDI_MULTIPLANE_OVERLAY_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_caps)| 由用户模式显示驱动程序用于指定覆盖平面功能。|
|[D3DDDI_MULTIPLANE_OVERLAY_FEATURE_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_feature_caps)| 标识覆盖功能。|
|[D3DDDI_MULTIPLANE_OVERLAY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddi_multiplane_overlay_flags)| 标识要覆盖平面上执行翻转操作。|
|[D3DDDI_MULTIPLANE_OVERLAY_GROUP_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_group_caps)| 由用户模式显示驱动程序来指定覆盖平面功能的组。|
|[D3DDDI_MULTIPLANE_OVERLAY_GROUP_CAPS_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddi_multiplane_overlay_group_caps_input)| 指定一个 multiplane 覆盖功能组的信息。|
|[D3DDDI_MULTIPLANE_OVERLAY_STRETCH_QUALITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_stretch_quality)| 标识筛选硬件在其拉伸或收缩 multiplane 覆盖数据时应执行的进程。
|[D3DDDI_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_video_frame_format)|标识覆盖平面的视频帧格式。 支持仅 D3DDDI_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT_PROGRESSIVE 值。|
|[D3DDDI_MULTIPLANE_OVERLAY_YCbCr_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-d3dddi_multiplane_overlay_ycbcr_flags)| 标识介绍 multiplane 覆盖的 YUV 范围和转换信息。|
|[D3DDDI_PRESENT_MULTIPLANE_OVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_present_multiplane_overlay)| 指定要显示覆盖平面。|
|[D3DDDIARG_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_checkmultiplaneoverlaysupport)| 在对 pfnCheckMultiPlaneOverlaySupport (D3D) 函数的调用中用于检查 multiplane 叠加的硬件支持的详细信息。|
|[D3DDDIARG_PRESENTMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddiarg_presentmultiplaneoverlay)| 指定要显示的 multiplane 覆盖资源。|
|[D3DDDICB_PRESENTMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddicb_presentmultiplaneoverlay)| 介绍的内容复制到和从 multiplane 覆盖分配。|
 
## <a name="multiplane-overlay-kernel-mode-driver-implemented-functions"></a>Multiplane 覆盖内核模式驱动程序实现函数

显示微型端口驱动程序实现的所有 multiplane 覆盖函数。

|函数|描述|
|:--|:--|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport)| 若要检查对于 multiplane 叠加的硬件支持的详细信息的 Microsoft DirectX 图形内核子系统由调用。|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport3)| 以下新函数调用以确定是否支持特定的多平面覆盖配置。|
|[DXGKDDI_GETMULTIPLANEOVERLAYCAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_getmultiplaneoverlaycaps)| 调用以检索 multiplane 覆盖功能。 对此 DDI 是为想要支持多个平面任何 WDDM 2.2 驱动程序所需的支持。|
|[DXGKDDI_POSTMULTIPLANEOVERLAYPRESENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_postmultiplaneoverlaypresent)| 新的多平面覆盖配置已生效，从而允许驱动程序来优化硬件状态后调用。 对于 Windows 显示器驱动程序模型 (WDDM) 2.0 或更高版本驱动程序支持多平面叠加的可选。|
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay3)|调用以更改所显示的覆盖配置。|
|[DXGKDDI_CHECKMULTIPLANEOVERLAYSUPPORT2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_checkmultiplaneoverlaysupport2)|DxgkDdiCheckMultiPlaneOverlaySupport2 调用以确定是否支持特定的多平面覆盖配置。 |
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay)|设置与特定的视频显示源相关联的多个表面，包括桌面窗口管理器 (DWM) 的 swapchain 的地址。 此函数用于显示多个应用层协议 （包括 DWM 的 swapchain） 到屏幕。|
|[DXGKDDI_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setvidpnsourceaddresswithmultiplaneoverlay2)| DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 调用以更改所显示的覆盖配置。|

## <a name="multiplane-overlay-kernel-mode-structures"></a>Multiplane 覆盖内核模式结构

显示微型端口驱动程序使用的所有结构。

|结构|描述|
|:--|:--|
|[DXGK_CHECK_MULTIPLANE_OVERLAY_SUPPORT_PLANE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_check_multiplane_overlay_support_plane)| 指定硬件提供了对 multiplane 覆盖的支持属性。|
|[DXGK_CHECK_MULTIPLANE_OVERLAY_SUPPORT_RETURN_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-dxgk_check_multiplane_overlay_support_return_info)| 指定的 multiplane 叠加的硬件支持的限制。|
|[DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_attributes)| 用于显示微型端口驱动程序指定叠加平面特性。|
|[DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_attributes2)|显示微型端口驱动程序使用 DXGK_MULTIPLANE_OVERLAY_ATTRIBUTES2 指定覆盖平面属性。 |
|[DXGK_MULTIPLANE_OVERLAY_BLEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_blend)| 标识要覆盖平面上执行混合操作。|
|[DXGK_MULTIPLANE_OVERLAY_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_flags)| 标识要覆盖平面上执行翻转操作。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane)| 指定要在对 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay 函数的调用中显示的覆盖平面。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane2)|DXGK_MULTIPLANE_OVERLAY_PLANE2 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 函数用于指定要显示覆盖平面。|
|[DXGK_MULTIPLANE_OVERLAY_PLANE_WITH_SOURCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_plane_with_source)|DXGK_MULTIPLANE_OVERLAY_PLANE_WITH_SOURCE 介绍多平面覆盖平面属性、 分配和视频存在网络源标识号。|
|[DXGK_MULTIPLANE_OVERLAY_VSYNC_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_vsync_info)|指定要显示垂直同步间隔期间覆盖平面。|
|[DXGK_MULTIPLANE_OVERLAY_YCbCr_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_multiplane_overlay_ycbcr_flags)|标识介绍 multiplane 覆盖的 YUV 范围和转换信息。|
|[DXGK_PRESENTMULTIPLANEOVERLAYINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentmultiplaneoverlayinfo)|指定 VidPN 输入和显示覆盖平面上的信息。|
|[DXGK_PRESENTMULTIPLANEOVERLAYLIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentmultiplaneoverlaylist)|指定要在对 DxgkDdiPresent 函数的调用中显示的覆盖平面。|
|[DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_checkmultiplaneoverlaysupport)|在对 DxgkDdiCheckMultiPlaneOverlaySupport 函数的调用中用于检查 multiplane 叠加的硬件支持的详细信息。|
|[DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_checkmultiplaneoverlaysupport2)|DXGKARG_CHECKMULTIPLANEOVERLAYSUPPORT2 传递到 DxgkDdiCheckMultiPlaneOverlaySupport2 函数，以确定是否支持特定的多平面覆盖配置。|
|[DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay)|包含为 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay 函数的参数。|
|[DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay2)|DXGKARG_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY2 传递给 DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay2 函数来更改显示的覆盖配置。|
 

## <a name="multiplane-overlay-kernel-mode-enumerations"></a>Multiplane 覆盖内核模式枚举

显示微型端口驱动程序使用的所有枚举。

| 枚举 | 描述 |
|:--|:--|
|[DXGK_MULTIPLANE_OVERLAY_STEREO_FLIP_MODE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stereo_flip_mode)|标识的覆盖平面立体声翻转模式。 支持仅 DXGK_MULTIPLANE_OVERLAY_STEREO_FLIP_NONE 值。 |
|[DXGK_MULTIPLANE_OVERLAY_STEREO_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stereo_format)|标识的覆盖平面立体声的显示格式。 支持仅 DXGK_MULTIPLANE_OVERLAY_STEREO_FORMAT_MONO 值。|
|[DXGK_MULTIPLANE_OVERLAY_STRETCH_QUALITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_stretch_quality)|标识筛选硬件在其拉伸或收缩 multiplane 覆盖数据时应执行的进程。|
|[DXGK_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_multiplane_overlay_video_frame_format)|标识覆盖平面的视频帧格式。 支持仅 DXGK_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT_PROGRESSIVE 值。|
 

此用户模式枚举常量值支持 multiplane 覆盖，是 Windows 8.1 的新增功能：

-   [**D3DDDICAPS\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff544132) (**D3DDDICAPS\_获取\_MULTIPLANE\_覆盖\_组\_CAPS**常量值)

 

 





