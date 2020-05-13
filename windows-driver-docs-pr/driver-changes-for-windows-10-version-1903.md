---
title: Windows 10 版本1903的驱动程序开发更改
description: 本部分介绍 Windows 10 中驱动程序开发的新增功能。
ms.assetid: 90f7754d-be7a-408d-8b89-b173a86c4fa3
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2bf812f56225743325a273081add70758b784adf
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270418"
---
# <a name="whats-new-in-windows-10-version-1903"></a>Windows 10 版本1903中的新增功能

本部分介绍 Windows 10 版本 1903（Windows 10 2019 年 4 月更新）中驱动程序开发的新增功能和更新。

## <a name="audio"></a><a name="audio-1903"></a>音频

下面是 Windows 10 版本 1903 中新的和更新的音频功能列表：

* 有关在新的 [eventdetectoroemadapter.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/) 标头中用于语音激活的音频 OEM 适配器的新参考主题。
* 新的远场音频信息： 
    * [PKEY_Devices_AudioDevice_Microphone_IsFarField](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-devices-audiodevice-microphone-isfarfield)
    * [KSPROPSETID_InterleavedAudio](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-interleavedaudio)
    * [KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION](https://review.docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-interleavedaudio-formatinformation)
    
* [USB 音频 2.0 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/usb-2-0-audio-drivers)中的新插孔说明信息。

## <a name="camera"></a><a name="camera-1903"></a>相机

在 Windows 10 版本 1903 中添加的新相机驱动程序文档和功能包括：

* 新的[红外闪光灯](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-irtorchmode)扩展属性控件，可以设置红外相机的红外闪光灯功率级和占空比。
* 新的 [KSCATEGORY_NETWORK_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-network-camera) 设备。
* 为以下控件选择器新编和更新了 [USB 视频类 (UVC) 1.5 扩展](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)文档：
  * MSXU_CONTROL_FACE_AUTHENTICATION
  * MSXU_CONTROL_METADATA
  * MSUX_CONTROL_IR_TORCH


## <a name="debugging"></a>调试

对 Windows 10 版本1903的调试器进行的更改包括：

* 添加了新的停止代码，以便更好地跟踪 Windows 操作系统中的独特故障类型。 此外，还补充并更新了大量现有的 bug 检查主题。 有关详细信息，请参阅 [Bug 检查代码参考](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)。

* 更新了 KDNET 主题（例如，在新文章[自动设置 KDNET 网络内核调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)中）以提高易用性

* 更新了 IP V6 KDNET 支持。

* 新的 [JavaScript 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting)主题

## <a name="display"></a><a name="display-1903"></a>显示

Windows 10 版本 1903 中的显示驱动程序开发的更新包括：

* **超级湿墨**：添加了新的 DDI 以实现前端缓冲渲染。 请参阅 [D3DWDDM2_6DDI_SCANOUT_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm2_6ddi_scanout_flags) 和 [PFND3DWDDM2_6DDI_PREPARE_SCANOUT_TRANSFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_6ddi_prepare_scanout_transformation)。

* **可变速率着色**：在不同的渲染图像中以不同的速率分配渲染性能/算力。 请参阅 [PFND3D12DDI_RS_SET_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_rs_set_shading_rate_0062) 和 [D3D12DDI_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_shading_rate_0062)。

* **收集诊断信息**：允许 OS 从包括渲染和显示功能的图形适配器的驱动程序中收集专用数据。 请参阅 [DXGKDDI_COLLECTDIAGNOSTICINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_collectdiagnosticinfo)。

* **后台处理**：允许用户模式驱动程序表达所需的线程行为，并允许运行时控制/监视此行为。 用户模式驱动程序将运转后台线程，为线程分配尽量低的优先级，并依赖于 NT 计划程序来确保这些线程不会干扰关键路径线程（一般会成功）。 请参阅 [PFND3D12DDI_QUEUEPROCESSINGWORK_CB_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_queueprocessingwork_cb_0062)。

* **驱动程序热更新**：需要更新 OS 组件时，尽量减少服务器停机时间。 请参阅 [DXGKDDI_SAVEMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_savememoryforhotupdate) 和 [DXGKDDI_RESTOREMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restorememoryforhotupdate)。

## <a name="networking"></a><a name="networking-1903"></a>网络

## <a name="netadaptercx"></a>NetAdapterCx

在 NetAdapter WDF 类扩展 (NetAdapterCx) 中，网环缓冲区已由网环取代，后者提供新的接口用于通过网环迭代器发送和接收网络数据。 下面是新主题的列表：

* [网环简介](https://docs.microsoft.com/windows-hardware/drivers/netcx/introduction-to-net-rings)
* [使用网环发送网络数据](https://docs.microsoft.com/windows-hardware/drivers/netcx/sending-network-data-with-net-rings)，其中提供了演示如何发送数据的新动画
* [使用网环接收网络数据](https://docs.microsoft.com/windows-hardware/drivers/netcx/receiving-network-data-with-net-rings)，其中提供了演示如何接收数据的新动画
* [使用网环取消网络数据](https://docs.microsoft.com/windows-hardware/drivers/netcx/canceling-network-data-with-net-rings)

支持此功能的新标头包括：

* [Ring.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/index)
* [Ringcollection.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/ringcollection/index)
* [Netringiterator.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/index)

下面是 NetAdapterCx 内容更新的列表：

* 已删除默认的适配器对象，改用单个适配器对象类型。 已相应地更新了以下主题：

  * [NetAdapterCx 对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-netadaptercx-objects)
  * [设备和适配器初始化](https://docs.microsoft.com/windows-hardware/drivers/netcx/device-and-adapter-initialization)

* 硬件卸载和数据包扩展 DDI 已重新组织为新标头：

  * [Checksum.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksum/index)
  * [Checksumtypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksumtypes/index)
  * [Extension.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/extension/index)
  * [Lso.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/lso/index)
  * [Lsotypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/lsotypes/index)
  * [Rsc.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/rsc/index)
  * [Rsctypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/rsctypes/index)

* 基本网络数据结构、数据包和段已更新，并已放入新标头：

  * [Packet.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/packet/index)
  * [Fragment.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/fragment/index)

* 大幅修改了[传输和接收队列](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues)主题，以包含回调示例和数据包队列的主要操作。

## <a name="mobile-operator-scenarios"></a>移动运营商方案

编写了新的移动套餐内容，以方便移动运营商通过移动套餐应用直接在 Windows 10 设备上向客户销售套餐：

* [移动套餐](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/mobile-plans)

## <a name="mobile-broadband"></a><a name="mobilebroadband-1903"></a>移动宽带

以下功能已添加到 Windows 10 版本 1903 中的移动宽带：

* 新的 [SIM 卡 (UICC) 文件/应用程序系统访问](https://docs.microsoft.com/windows-hardware/drivers/network/mb-uicc-application-and-file-system-access)功能
* 新的[手机网络时间信息 (NITZ)](https://docs.microsoft.com/windows-hardware/drivers/network/mb-nitz-support) 功能。
* 新的[使用 DSS 进行调制解调器日志记录](https://docs.microsoft.com/windows-hardware/drivers/network/mb-modem-logging-with-dss)功能。
* 新的 [5G 数据类支持](https://docs.microsoft.com/windows-hardware/drivers/network/mb-5g-data-class-support)功能。

## <a name="power-management-framework"></a>电源管理框架

电源管理框架 (PoFx) 可让驱动程序为设备中的各个组件单独定义一个或多个可调整的性能状态集。 驱动程序可以使用性能状态来限制组件的工作负荷，以提供刚好足够的性能来满足工作负荷的当前需求。 有关详细信息，请参阅[组件级性能状态管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-performance-management)。

Windows 10 版本 1903 支持[定向电源管理框架 (DFx)](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-the-directed-power-management-framework)。  相关的参考文档包括：

* [PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-po_fx_device_v3)
* [PO_FX_DIRECTED_POWER_DOWN_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_down_callback)
* [PO_FX_DIRECTED_POWER_UP_CALLBACK 回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_directed_power_up_callback)
* [PoFxCompleteDirectedPowerDown](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxcompletedirectedpowerdown) 函数

有关 DFx 测试的信息，请参阅以下页：

* [定向 FX 单一设备测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
* [定向 FX 系统验证测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
* [PwrTest DirectedFx 方案](devtest/pwrtest-directedfx-scenario.md)

## <a name="print"></a><a name="print-1903"></a>打印

在 Windows 10 版本 1903 中添加的新打印驱动程序文档和功能包括：

* 新的 USB 打印 IOCTL：

  * [IOCTL_USBPRINT_GET_INTERFACE_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_get_interface_type)
  * [IOCTL_USBPRINT_GET_PROTOCOL](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_get_protocol)
  * [IOCTL_USBPRINT_SET_PROTOCOL](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_set_protocol)

* 新的 **fpRegeneratePrintDeviceCapabilities** [PRINTPROVIDER](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_printprovidor) 结构成员和更新的文档。

## <a name="sensors"></a><a name="sensors-1903"></a>传感器

Windows 10 版本 1903 中传感器驱动程序开发的新功能包括用于测试和校准屏幕亮度的 [MALT（Microsoft 环境光照度工具）](https://docs.microsoft.com/windows-hardware/drivers/sensors/testing-malt-building-a-light-testing-tool)。

此外，还更新了环境色 OEM 白皮书。

## <a name="storage"></a><a name="storage-1903"></a>存储

Windows 10 版本 1903 中添加了以下存储功能：

* 添加了新的 Storport API，用于在 ETW 事件中记录设备故障和硬件协议错误，以及查询平台 D3 所需的行为
* 添加了新的 API 用于设置存储设备或适配器的属性
* 对于文件系统，已添加新的 DDI 用于支持在创建完成时检索扩展属性 (EA) 信息，使微型筛选器能够改变 ECP 有效负载来更改更高级别的筛选器看到的结果

## <a name="windows-driver-frameworks-wdf"></a>Windows 驱动程序框架 (WDF)

在 Windows 10 版本 1903 中，Windows 驱动程序框架 (WDF) 包括内核模式驱动程序框架 (KMDF) 版本 1.29 和用户模式驱动程序框架 (UMDF) 版本 2.29。

有关这些框架版本的功能的信息，请参阅 [Windows 10 中 WDF 驱动程序的新增功能](https://docs.microsoft.com/windows-hardware/drivers/wdf/)。
若要了解在旧版 WDF 中添加了哪些功能，请参阅 [KMDF 版本历史记录](https://docs.microsoft.com/windows-hardware/drivers/wdf/kmdf-version-history)和 [UMDF 版本历史记录](https://docs.microsoft.com/windows-hardware/drivers/wdf/umdf-version-history)。

## <a name="windows-hardware-error-architecture-whea"></a>Windows 硬件错误体系结构 (WHEA)

Windows 10 版本 1903 包含 WHEA 的简化界面。  有关详细信息，请参阅以下页：

* [**WheaAddErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)
* [**WheaReportHwErrorDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheareporthwerrordevicedriver)
* [**WheaRemoveErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)
* [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)
* [*WHEA_ERROR_SOURCE_READY_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_ready_device_driver)
* [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)
* [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)

## <a name="wi-fi"></a><a name="wifi-1903"></a>Wi-Fi

新的 Wi-Fi 驱动程序开发文档和功能包括：

* 新的精准时序测量(FTM) 功能
* 新的 [WPA3-SAE 身份验证](https://docs.microsoft.com/windows-hardware/drivers/network/wpa3-sae-authentication)功能
* 新的多频段操作 (MBO) 支持，可提高企业方案的漫游性能
* 新的信标报告卸载支持
* 有关这些新功能的 OID 命令、NDIS 状态指示和 TLV，请参阅 [WDI 文档更改历史记录](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-doc-change-history)

已更新 Windows 10 版本 1903 的以下主题：

* [WDI_AUTH_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm) - 添加了对 WPA3-SAE 身份验证的支持
* [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-request-action-frame) 和 [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-response-action-frame) - 对传出的点对点 (P2P) 动作帧添加了更多验证