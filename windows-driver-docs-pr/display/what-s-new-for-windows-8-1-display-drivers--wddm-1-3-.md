---
title: Windows 8.1 显示驱动程序 (WDDM 1.3) 的新增功能
description: 本主题列出了 Windows 8.1 的新的或更新的显示驱动程序功能。 Windows 8.1 引入了 1.3 (WDDM) 版本的 Windows 显示驱动程序模型。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd427b7c32922ca997af5b7f7bc3b4ae6cbd42cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826035"
---
# <a name="whats-new-for-windows-81-display-drivers-wddm-13"></a>Windows 8.1 显示驱动程序 (WDDM 1.3) 的新增功能


本主题列出了 Windows 8.1 的新的或更新的显示驱动程序功能。 Windows 8.1 引入了 1.3 (WDDM) 版本的 Windows 显示驱动程序模型。

<span id="Enumerating_GPU_engine_capabilities"></span><span id="enumerating_gpu_engine_capabilities"></span><span id="ENUMERATING_GPU_ENGINE_CAPABILITIES"></span>[枚举 GPU 引擎功能](enumerating-gpu-nodes.md)  
用于查询 GPU 节点引擎功能的接口。

<span id="Using_cross-adapter_resources_in_a_hybrid_system"></span><span id="using_cross-adapter_resources_in_a_hybrid_system"></span><span id="USING_CROSS-ADAPTER_RESOURCES_IN_A_HYBRID_SYSTEM"></span>[在混合系统中使用跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)  
描述如何处理在集成 Gpu 和离散 Gpu 之间共享的资源。

<span id="YUV_format_ranges_in_"></span><span id="yuv_format_ranges_in_"></span><span id="YUV_FORMAT_RANGES_IN_"></span>[Windows 8.1 中的 YUV 格式范围](yuv-format-ranges.md)  
一种接口，用于向用户模式显示驱动程序发出信号，指示视频输入在工作室亮度范围内或在扩展范围内。

<span id="Wireless_displays__Miracast_"></span><span id="wireless_displays__miracast_"></span><span id="WIRELESS_DISPLAYS__MIRACAST_"></span>[无线显示 (Miracast) ](wireless-displays--miracast-.md)  
描述如何启用无线 (Miracast) 显示。

<span id="Multiplane_overlay_support"></span><span id="multiplane_overlay_support"></span><span id="MULTIPLANE_OVERLAY_SUPPORT"></span>[Multiplane 覆盖支持](multiplane-overlay-support.md)  
描述如何实现 multiplane 覆盖。

<span id="Tiled_resource_support"></span><span id="tiled_resource_support"></span><span id="TILED_RESOURCE_SUPPORT"></span>[平铺资源支持](tiled-resource-support.md)  
介绍如何支持平铺资源。

<span id="Adaptive_refresh_for_playing_24_fps_video_content"></span><span id="adaptive_refresh_for_playing_24_fps_video_content"></span><span id="ADAPTIVE_REFRESH_FOR_PLAYING_24_FPS_VIDEO_CONTENT"></span>[播放 24 fps 视频内容的自适应刷新](adaptive-refresh-for-playing-24-fps-content.md)  
介绍驱动程序如何实现 48-Hz 自适应刷新，以节省通常以 60 Hz 运行的电源监视器。

<span id="Direct3D_rendering_performance_improvements"></span><span id="direct3d_rendering_performance_improvements"></span><span id="DIRECT3D_RENDERING_PERFORMANCE_IMPROVEMENTS"></span>[Direct3D 呈现性能改进](direct3d-rendering-performance-improvements.md)  
介绍驱动程序如何提高 Microsoft Direct3D 9 硬件的呈现性能。

<span id="Graphics_kernel_performance_improvements"></span><span id="graphics_kernel_performance_improvements"></span><span id="GRAPHICS_KERNEL_PERFORMANCE_IMPROVEMENTS"></span>[图形内核性能改进](graphics-kernel-performance-improvements.md)  
介绍驱动程序如何管理历史记录缓冲区以提供有关在 (DMA) 缓冲区的直接内存访问中执行 API 调用的准确计时数据。

<span id="Present_overhead_improvements"></span><span id="present_overhead_improvements"></span><span id="PRESENT_OVERHEAD_IMPROVEMENTS"></span>[呈现开销提高](present-overhead-improvements.md)  
介绍驱动程序如何支持其他纹理格式和新的现有设备驱动程序接口 (DDI) 。

<span id="Specifying_device_state_and_frame_latency"></span><span id="specifying_device_state_and_frame_latency"></span><span id="SPECIFYING_DEVICE_STATE_AND_FRAME_LATENCY"></span>[指定设备状态和帧延迟](specifying-device-state-and-frame-latency-starting-in-wddm-1-3.md)  
介绍用户模式显示驱动程序如何将设备状态和帧延迟信息传递到显示微型端口驱动程序。

<span id="Supporting_Path-Independent_Rotation"></span><span id="supporting_path-independent_rotation"></span><span id="SUPPORTING_PATH-INDEPENDENT_ROTATION"></span>[支持 Path-Independent 旋转](supporting-path-independent-rotation.md)  
从 Windows 8.1 更新开始支持。 描述显示微型端口驱动程序如何支持 "纵向复制"-第一次显示时，具有尽可能高的分辨率。

 

 





