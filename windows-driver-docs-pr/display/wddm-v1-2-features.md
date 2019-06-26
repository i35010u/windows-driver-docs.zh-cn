---
title: WDDM 1.2 功能
description: 本主题介绍 Windows 显示器驱动程序模型 (WDDM) 版本 1.2 功能集，其中包括几个新的增强功能可提高性能、 可靠性和整体最终用户体验。
ms.assetid: 65072545-76F0-43A8-9E46-703CA99BFE90
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff70e630d512cb1581008534d8757ae0020eda5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353408"
---
# <a name="wddm-12-features"></a>WDDM 1.2 功能


本主题介绍 Windows 显示器驱动程序模型 (WDDM) 版本 1.2 功能集，其中包括几个新的增强功能可提高性能、 可靠性和整体最终用户体验。

每个功能需要第三方 WDDM 1.2 和更高版本的驱动程序的特殊支持。 本部分将详细介绍何种要素构成 WDDM 1.2 功能集。

WDDM 1.2 具有必需和可选功能。 该驱动程序必须实现所有必需的功能来声明本身作为"WDDM 1.2 驱动程序，"时，驱动程序可以实现的可选功能的任意组合 （或无）。 WDDM 1.2 驱动程序必须报告的任何 WDDM 1.2 功能。

此表总结了 WDDM 1.2 功能集。 "M"表示必需的"O"表示可选的而"NA"指示不适用。 若要阅读有关每个功能的详细信息，请在左侧列中的链接。

**WDDM 1.2 功能集**

| 启用的 WDDM 1.2 的 Windows 8 功能                                                                         | 功能权益                                                                                                            | WDDM 驱动程序类型：所有的图形 | WDDM 驱动程序类型：仅呈现 | WDDM 驱动程序类型：仅显示 |
|----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|---------------------------------|-------------------------------|--------------------------------|
| [视频内存产品/服务和回收](video-memory-offer-and-reclaim.md)                                           | 使效率更高的视频内存的使用情况                                                                               | M                               | M                             | NA                             |
| [GPU 抢占](gpu-preemption.md)                                                                           | 提高桌面响应能力                                                                                            | M                               | M                             | NA                             |
| [在 Windows 8 中 TDR 更改](tdr-changes-in-windows-8.md)                                                       | 改进了复原能力 GPU 挂起                                                                                           | M                               | M                             | NA                             |
| [优化的屏幕旋转支持](optimized-screen-rotation-support.md)                                     | 屏幕旋转体验，而无闪烁                                                                                 | M                               | NA                            | M                              |
| [立体 3D](stereoscopic-3d.md)                                                                         | 提供一个一致的 API 和 DDI 平台，来启用立体 3D 方案                                             | O                               | NA                            | NA                             |
| [Direct3D 11 视频播放的改进](d3d11-video-playback-improvements.md)                               | 视频播放应用程序的简化编程体验                                                          | M\*                             | M\*                           | NA                             |
| [Direct 翻转的视频内存](direct-flip-of-video-memory.md)                                                 | 要降低功率消耗的视频播放和复合堆栈中的改进                                       | M                               | NA                            | NA                             |
| [提供无缝的状态转换](seamless-state-transitions-in-wddm-1-2-and-later.md)                   | 在状态转换和错误检查的执行期间保持高分辨率                                                   | M                               | NA                            | M                              |
| [即插即用 (PnP) 开始和停止](plug-and-play--pnp--start-and-stop-cases.md)                             | 由于显示所有权过渡固件、 Windows 和驱动程序之间维护高分辨率                        | M                               | NA                            | M                              |
| [备用休眠优化](standby-hibernate-optimizations.md)                                         | 启用优化来提高睡眠的性能和恢复了图形堆栈                                     | O                               | O                             | NA                             |
| [GPU 电源管理的空闲状态和活动的电源](gpu-power-management-of-idle-and-active-power.md)      | 细粒度设备电源管理提供标准化的基础结构                                            | O                               | O                             | O                              |
| [在 GPU 上的 XPS 光栅化](xps-rasterization-on-the-gpu.md)                                               | 启用质量打印体验在 Windows 上的使用第三方驱动程序                                                  | M\*\*                           | M\*\*                         | NA                             |
| [显示的容器 ID 支持](container-id-support-for-displays-.md)                                    | 可帮助中的用户界面类似于设备中心向用户表示监视的设备连接和关联的状态 | M                               | NA                            | M                              |
| [禁用框架指针省略 (FPO) 优化](disabling-frame-pointer-omission--fpo--optimization.md) | 改进了调试的 FPO 字段中与相关的性能问题                                                     | M                               | M                             | M                              |
| [用户模式驱动程序日志记录](user-mode-driver-logging.md)                                                       | 改进了诊断和分析与内存相关的问题，从而更好地了解内存使用情况的功能              | M                               | M                             | NA                             |

 

\*此功能是必需的所有 WDDM 1.2 驱动程序与 Microsoft Direct3D 10-，10.1、 11 或 11.1 支持的硬件 （或更高版本）。

\*\*无需新的设备驱动程序接口 (DDI) 或行为更改。 但是，WDDM 1.2 和更高版本的驱动程序必须能够通过 XML 纸张规范 (XPS) 光栅化符合性测试，以确保硬件加速 XPS 打印方案提供质量的打印体验。

**请注意**  一组新的 Api 可从 Windows 8 开始复制协作应用场景的桌面。 有关更多详细信息，请参阅[桌面重复](desktop-duplication-api.md)。

 

## <a name="span-idadditionalnewfeaturesinwindows8spanspan-idadditionalnewfeaturesinwindows8spanspan-idadditionalnewfeaturesinwindows8spanadditional-new-features-in-windows8"></a><span id="Additional_new_features_in_Windows_8"></span><span id="additional_new_features_in_windows_8"></span><span id="ADDITIONAL_NEW_FEATURES_IN_WINDOWS_8"></span>Windows 8 中的其他新功能


显示在下面的新的或更新驱动程序 DDIs 还提供了 Windows 8:

[**内核模式下仅显示驱动程序 (KMDOD) 接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

提供了一组有限的显示功能而无需呈现功能。

**请注意**  请参考[内核模式仅显示微型端口驱动程序](https://go.microsoft.com/fwlink/p/?linkid=258742)示例。

 

[**支持通过存储接口的芯片 (SoC) 体系结构上的系统**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

可以让 SoC 系统上的显示微型端口驱动程序访问总线资源。

### <a name="span-idsurpriseremovalofsecondaryadapterspanspan-idsurpriseremovalofsecondaryadapterspanspan-idsurpriseremovalofsecondaryadapterspansurprise-removal-of-secondary-adapter"></a><span id="Surprise_removal_of_secondary_adapter"></span><span id="surprise_removal_of_secondary_adapter"></span><span id="SURPRISE_REMOVAL_OF_SECONDARY_ADAPTER"></span>意外删除了辅助适配器

-   [*DxgkDdiNotifySurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_notify_surprise_removal)
-   [**DXGK\_SURPRISE\_REMOVAL\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ne-dispmprt-_dxgk_surprise_removal_type)
-   [**DXGK\_DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**D3DKMT\_WDDM\_1\_2\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/display/d3dkmt-wddm-1-2-caps)

[**系统固件表接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_firmware_table_interface)

允许显示微型端口驱动程序枚举和读取系统固件表。

[**亮度控制接口 V。2 （自适应和平滑的亮度控制）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

允许显示微型端口驱动程序到显示背景光降低功率和仍顺利适应环境光线和更改亮度的用户请求中的更改。

另请参阅[Windows 8 集成显示器的亮度控制](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614018(v=vs.85))。

### <a name="span-idmicrosoftdirectxgraphicsinfrastructureddidxgispanspan-idmicrosoftdirectxgraphicsinfrastructureddidxgispanspan-idmicrosoftdirectxgraphicsinfrastructureddidxgispanmicrosoft-directx-graphics-infrastructure-ddi-dxgi"></a><span id="Microsoft_DirectX_Graphics_Infrastructure_DDI__DXGI_"></span><span id="microsoft_directx_graphics_infrastructure_ddi__dxgi_"></span><span id="MICROSOFT_DIRECTX_GRAPHICS_INFRASTRUCTURE_DDI__DXGI_"></span>Microsoft DirectX 图形基础结构 (DXGI) DDI

-   [*Blt1DXGI*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)
-   [**DXGI\_DDI\_ARG\_BLT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_blt1)
-   [**DXGI\_DDI\_BASE\_ARGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args)
-   [**DXGI1\_2\_DDI\_BASE\_FUNCTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_2_ddi_base_functions)

### <a name="span-idallocationsharingenqueinggpueventsspanspan-idallocationsharingenqueinggpueventsspanspan-idallocationsharingenqueinggpueventsspanallocation-sharing--enqueing-gpu-events"></a><span id="Allocation_sharing___enqueing_GPU_events"></span><span id="allocation_sharing___enqueing_gpu_events"></span><span id="ALLOCATION_SHARING___ENQUEING_GPU_EVENTS"></span>分配共享与加入 GPU 事件

-   [*pfnCreateSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createsynchronizationobject2cb)
-   [*pfnSignalSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_signalsynchronizationobject2cb)
-   [*pfnWaitForSynchronizationObject2Cb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_waitforsynchronizationobject2cb)
-   [**D3DDDI\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicecallbacks)
-   [**D3DDDI\_SYNCHRONIZATIONOBJECT\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_synchronizationobject_flags)
-   [**D3DDDICB\_CREATESYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_createsynchronizationobject2)
-   [**D3DDDICB\_SIGNALFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_signalflags)
-   [**D3DDDICB\_SIGNALSYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_signalsynchronizationobject2)
-   [**D3DDDICB\_WAITFORSYNCHRONIZATIONOBJECT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_waitforsynchronizationobject2)
-   [**D3DKMT\_CREATEALLOCATIONFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_createallocationflags)
-   [**D3DKMT\_CREATEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2)
-   [**D3DKMT\_CREATEKEYEDMUTEX2\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_createkeyedmutex2_flags)
-   [**D3DKMT\_RELEASEKEYEDMUTEX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_releasekeyedmutex2)
-   [**D3DKMTShareObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtshareobjects)

### <a name="span-idcancelcommandinterfacespanspan-idcancelcommandinterfacespanspan-idcancelcommandinterfacespancancel-command-interface"></a><span id="Cancel_command_interface"></span><span id="cancel_command_interface"></span><span id="CANCEL_COMMAND_INTERFACE"></span>取消命令界面

-   [*DxgkDdiCancelCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_cancelcommand)
-   [**DXGKARG\_CANCELCOMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_cancelcommand)
-   [**DXGK\_VIDSCHCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidschcaps)

### <a name="span-idoutputduplicationspanspan-idoutputduplicationspanspan-idoutputduplicationspanoutput-duplication"></a><span id="Output_duplication"></span><span id="output_duplication"></span><span id="OUTPUT_DUPLICATION"></span>输出重复

-   [**D3DKMTOutputDuplPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtoutputduplpresent)
-   [**D3DKMTOutputDuplReleaseFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtoutputduplreleaseframe)
-   [**D3DKMT\_OUTPUTDUPL\_RELEASE\_FRAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputdupl_release_frame)
-   [**D3DKMT\_OUTPUTDUPL\_SNAPSHOT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputdupl_snapshot)
-   [**D3DKMT\_OUTPUTDUPLCONTEXTSCOUNT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplcontextscount)
-   [**D3DKMT\_OUTPUTDUPLPRESENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplpresent)
-   [**D3DKMT\_OUTPUTDUPLPRESENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_outputduplpresentflags)
-   [**D3DKMT\_PRESENT\_RGNS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ns-d3dkmthk-_d3dkmt_present_rgns)

[**Windows 8 OpenGL 增强功能**](supporting-opengl-enhancements.md)

OpenGL 可安装的客户端驱动程序 (ICDs) 可以调用新函数来控制对资源的访问和对象与标识符之间进行映射。

 

 





