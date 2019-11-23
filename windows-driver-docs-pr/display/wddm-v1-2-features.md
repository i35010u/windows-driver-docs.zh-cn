---
title: WDDM 1.2 功能
description: 本主题介绍 Windows 显示驱动程序模型（WDDM）版本1.2 功能集，其中包括一些新的增强功能，这些增强功能可提高性能、可靠性和最终用户体验。
ms.assetid: 65072545-76F0-43A8-9E46-703CA99BFE90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e49e1b0ef745ba83689778755a7c6ee3fef354c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829178"
---
# <a name="wddm-12-features"></a>WDDM 1.2 功能


本主题介绍 Windows 显示驱动程序模型（WDDM）版本1.2 功能集，其中包括一些新的增强功能，这些增强功能可提高性能、可靠性和最终用户体验。

其中每项功能都需要第三方 WDDM 1.2 和更高版本驱动程序的特殊支持。 本部分然后详细阐述了如何构成 WDDM 1.2 功能集。

WDDM 1.2 具有强制功能和可选功能。 驱动程序必须实现所有必需的功能，将其自身声明为 "WDDM 1.2 驱动程序"，同时驱动程序可以实现任何可选功能的组合（或无）。 非 WDDM 1.2 驱动程序必须报告 WDDM 1.2 的任何功能。

下表汇总了 WDDM 1.2 功能集。 "M" 指示必需，"O" 表示可选，"NA" 指示不适用。 若要阅读有关每个功能的详细信息，请单击左侧列中的链接。

**WDDM 1.2 功能集**

| WDDM 1.2 启用的 Windows 8 功能                                                                         | 功能权益                                                                                                            | WDDM 驱动程序类型：完整图形 | WDDM 驱动程序类型：仅呈现 | WDDM 驱动程序类型：仅显示 |
|----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|---------------------------------|-------------------------------|--------------------------------|
| [视频内存优惠和回收](video-memory-offer-and-reclaim.md)                                           | 能够更高效地使用视频内存                                                                               | M                               | M                             | 不可用                             |
| [GPU 抢占](gpu-preemption.md)                                                                           | 提高桌面响应能力                                                                                            | M                               | M                             | 不可用                             |
| [Windows 8 中的 TDR 更改](tdr-changes-in-windows-8.md)                                                       | 改善了 GPU 挂起的复原                                                                                           | M                               | M                             | 不可用                             |
| [优化屏幕旋转支持](optimized-screen-rotation-support.md)                                     | 无闪烁的屏幕旋转体验                                                                                 | M                               | 不可用                            | M                              |
| [Stereoscopic 3D](stereoscopic-3d.md)                                                                         | 提供一致的 API 和 DDI 平台来启用 Stereoscopic 3D 方案                                             | O                               | 不可用                            | 不可用                             |
| [Direct3D 11 视频播放改进](d3d11-video-playback-improvements.md)                               | 视频播放应用程序的简化编程体验                                                          | M\*                             | M\*                           | 不可用                             |
| [视频内存的直接翻转](direct-flip-of-video-memory.md)                                                 | 视频播放和组合堆栈改进，以减少能耗                                       | M                               | 不可用                            | 不可用                             |
| [提供无缝状态转换](seamless-state-transitions-in-wddm-1-2-and-later.md)                   | 在状态转换和 bug 检查期间维护高分辨率                                                   | M                               | 不可用                            | M                              |
| [即插即用（PnP）启动和停止](plug-and-play--pnp--start-and-stop-cases.md)                             | 维护高分辨率，因为在固件、Windows 和驱动程序之间过渡显示所有权                        | M                               | 不可用                            | M                              |
| [备用休眠优化](standby-hibernate-optimizations.md)                                         | 启用对图形堆栈的优化，以提高睡眠和恢复性能                                     | O                               | O                             | 不可用                             |
| [空闲状态和活动电源的 GPU 电源管理](gpu-power-management-of-idle-and-active-power.md)      | 为细化设备电源管理提供标准化的基础结构                                            | O                               | O                             | O                              |
| [GPU 上的 XPS 光栅化](xps-rasterization-on-the-gpu.md)                                               | 使用第三方驱动程序在 Windows 上启用质量打印体验                                                  | M\*\*                           | M\*\*                         | 不可用                             |
| [容器 ID 支持显示](container-id-support-for-displays-.md)                                    | 有助于在类似于设备中心的用户界面中将监视设备连接和关联状态与用户交互 | M                               | 不可用                            | M                              |
| [禁用帧指针省略（FPO）优化](disabling-frame-pointer-omission--fpo--optimization.md) | 改善与字段中的 FPO 相关的性能问题的调试                                                     | M                               | M                             | M                              |
| [用户模式驱动程序日志记录](user-mode-driver-logging.md)                                                       | 通过提供更好的内存使用量视图，提高诊断和调查与内存相关的问题的能力              | M                               | M                             | 不可用                             |

 

\*此功能对于所有 WDDM 1.2 驱动程序都是必需的，可与 Microsoft Direct3D 10、10.1、、11或11.1 硬件（或更高版本）配合。

\*\*没有新的设备驱动程序接口（DDI）或行为更改。 但是，WDDM 1.2 和更高版本的驱动程序必须能够传递 XML 纸张规范（XPS）光栅化测试，以确保硬件加速 XPS 打印方案的质量打印体验。

**请注意**   从 Windows 8 开始提供一组新的 api，以便为协作方案复制桌面。 有关更多详细信息，请参阅[桌面复制](desktop-duplication-api.md)。

 

## <a name="span-idadditional_new_features_in_windows_8spanspan-idadditional_new_features_in_windows_8spanspan-idadditional_new_features_in_windows_8spanadditional-new-features-in-windows8"></a><span id="Additional_new_features_in_Windows_8"></span><span id="additional_new_features_in_windows_8"></span><span id="ADDITIONAL_NEW_FEATURES_IN_WINDOWS_8"></span>Windows 8 中的其他新功能


Windows 8 中还提供了以下新的或已更新的显示驱动程序 DDIs：

[**内核模式仅显示驱动程序（KMDOD）接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

提供一组有限的显示功能，无需呈现功能。

**请注意**  另请参阅[内核模式仅显示小型端口驱动程序](https://go.microsoft.com/fwlink/p/?linkid=258742)示例。

 

[**支持通过 SPB 接口对芯片（SoC）体系结构进行系统**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

让显示微型端口驱动程序能够访问 SoC 系统上的总线资源。

### <a name="span-idsurprise_removal_of_secondary_adapterspanspan-idsurprise_removal_of_secondary_adapterspanspan-idsurprise_removal_of_secondary_adapterspansurprise-removal-of-secondary-adapter"></a><span id="Surprise_removal_of_secondary_adapter"></span><span id="surprise_removal_of_secondary_adapter"></span><span id="SURPRISE_REMOVAL_OF_SECONDARY_ADAPTER"></span>删除辅助适配器的意外删除

-   [*DxgkDdiNotifySurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_surprise_removal)
-   [**DXGK\_意外\_删除\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ne-dispmprt-_dxgk_surprise_removal_type)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**D3DKMT\_WDDM\_1\_2\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/display/d3dkmt-wddm-1-2-caps)

[**系统固件表接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_firmware_table_interface)

允许显示微型端口驱动程序枚举并读取系统固件表。

[**亮度控制接口5V （自适应和平滑亮度控制）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

允许显示微型端口驱动程序减少显示器背景光的电量，并平稳地适应环境光的变化和用户请求的变化亮度。

另请参阅[适用于集成显示器的 Windows 8 亮度控件](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614018(v=vs.85))。

### <a name="span-idmicrosoft_directx_graphics_infrastructure_ddi__dxgi_spanspan-idmicrosoft_directx_graphics_infrastructure_ddi__dxgi_spanspan-idmicrosoft_directx_graphics_infrastructure_ddi__dxgi_spanmicrosoft-directx-graphics-infrastructure-ddi-dxgi"></a><span id="Microsoft_DirectX_Graphics_Infrastructure_DDI__DXGI_"></span><span id="microsoft_directx_graphics_infrastructure_ddi__dxgi_"></span><span id="MICROSOFT_DIRECTX_GRAPHICS_INFRASTRUCTURE_DDI__DXGI_"></span>Microsoft DirectX 图形基础结构 DDI （DXGI）

-   [*Blt1DXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)
-   [**DXGI\_DDI\_ARG\_BLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_blt1)
-   [**DXGI\_DDI\_基本\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)
-   [**DXGI1\_2\_DDI\_基\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

### <a name="span-idallocation_sharing___enqueing_gpu_eventsspanspan-idallocation_sharing___enqueing_gpu_eventsspanspan-idallocation_sharing___enqueing_gpu_eventsspanallocation-sharing--enqueing-gpu-events"></a><span id="Allocation_sharing___enqueing_GPU_events"></span><span id="allocation_sharing___enqueing_gpu_events"></span><span id="ALLOCATION_SHARING___ENQUEING_GPU_EVENTS"></span>& Enqueing GPU 事件的分配共享

-   [*pfnCreateSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createsynchronizationobject2cb)
-   [*pfnSignalSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobject2cb)
-   [*pfnWaitForSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobject2cb)
-   [**D3DDDI\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)
-   [**D3DDDI\_SYNCHRONIZATIONOBJECT\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DDDICB\_CREATESYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_createsynchronizationobject2)
-   [**D3DDDICB\_SIGNALFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddicb_signalflags)
-   [**D3DDDICB\_SIGNALSYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_signalsynchronizationobject2)
-   [**D3DDDICB\_WAITFORSYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_waitforsynchronizationobject2)
-   [**D3DKMT\_CREATEALLOCATIONFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createallocationflags)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2)
-   [**D3DKMT\_CREATEKEYEDMUTEX2\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2_flags)
-   [**D3DKMT\_RELEASEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_releasekeyedmutex2)
-   [**D3DKMTShareObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtshareobjects)

### <a name="span-idcancel_command_interfacespanspan-idcancel_command_interfacespanspan-idcancel_command_interfacespancancel-command-interface"></a><span id="Cancel_command_interface"></span><span id="cancel_command_interface"></span><span id="CANCEL_COMMAND_INTERFACE"></span>取消命令界面

-   [*DxgkDdiCancelCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_cancelcommand)
-   [**DXGKARG\_CANCELCOMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_cancelcommand)
-   [**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)

### <a name="span-idoutput_duplicationspanspan-idoutput_duplicationspanspan-idoutput_duplicationspanoutput-duplication"></a><span id="Output_duplication"></span><span id="output_duplication"></span><span id="OUTPUT_DUPLICATION"></span>输出重复

-   [**D3DKMTOutputDuplPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtoutputduplpresent)
-   [**D3DKMTOutputDuplReleaseFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtoutputduplreleaseframe)
-   [**D3DKMT\_OUTPUTDUPL\_版本\_帧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputdupl_release_frame)
-   [**D3DKMT\_OUTPUTDUPL\_快照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputdupl_snapshot)
-   [**D3DKMT\_OUTPUTDUPLCONTEXTSCOUNT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplcontextscount)
-   [**D3DKMT\_OUTPUTDUPLPRESENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplpresent)
-   [**D3DKMT\_OUTPUTDUPLPRESENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplpresentflags)
-   [**D3DKMT\_\_RGNS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_present_rgns)

[**Windows 8 OpenGL 增强功能**](supporting-opengl-enhancements.md)

OpenGL 可安装客户端驱动程序（ICDs）可以调用新函数来控制对资源的访问，以及在对象和标识符之间进行映射。

 

 





