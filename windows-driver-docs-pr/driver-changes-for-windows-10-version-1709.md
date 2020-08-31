---
title: Windows 10 版本 1709 的驱动程序开发变更
description: 本部分介绍 Windows 10 中驱动程序开发的新增功能。
ms.assetid: 68a5a513-0dab-40f7-b67f-29b76061e1ab
ms.date: 04/14/2020
author: EliotSeattle
ms.localizationpriority: medium
ms.openlocfilehash: 3222a10b91c349f55a98501fe4111b83d1fbd4b9
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066554"
---
# <a name="driver-development-additions-for-windows-10-version-1709"></a>适用于 Windows 10 的驱动程序开发添加版本1709

本主题提供有关 Windows 10 版本1709中的 Windows 驱动程序开发功能和更新的信息。

## <a name="feature-areas-updated-in-windows-10-version-1709"></a>Windows 10 版本1709中更新的功能区域

以下功能在 Windows 10 版本1709中记录了更新。

- [音频](#audio)
- [ACPI](#acpi)
- [生物识别](#biometric)
- [Windows 调试器](#windows-debugger)
- [显示器](#display)
- [驱动程序验证程序](#driver-verifier)
- [硬件通知](#hardware-notifications)
- [Windows 内核](#windows-kernel)
- [移动宽带](#mobile-broadband)
- [网络](#networking)
- [虚拟化 PCI](#virtualized-pci)
- [脉宽调制](#pulse-width-modulation-controllers)
- [& 存储的文件系统](#file-systems-and-storage)
- [USB](#usb)
- [通用 Windows 驱动程序](#universal-windows-drivers)
- [WPP 软件跟踪](#wpp-software-tracing)

### <a name="windows-debugger"></a>Windows 调试器

下面是 Windows 10 版本 1709 中调试器的新内容集列表：

- [使用 WinDbg 预览版进行调试](./debugger/debugging-using-windbg-preview.md) - 预览下一代调试器。
- [时光穿越调试 - 概述](./debugger/time-travel-debugging-overview.md) - 记录和重放过程的执行。

### <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证程序包含以下技术的新驱动程序验证规则：

- 新的[音频驱动程序规则](./devtest/rules-for-audio-drivers.md)
- 新的 [AVStream 驱动程序规则](./devtest/rules-for-avstream-drivers.md)
- 四个新的 [KMDF 驱动程序规则](./devtest/sdv-rules-for-kmdf-drivers.md)
- 三个新的 [NDIS 驱动程序规则](./devtest/sdv-rules-for-ndis-drivers.md)
- 版本 1703 中添加了新的 [Nullcheck 规则](./devtest/nullcheck.md) 

### <a name="universal-windows-drivers"></a>通用 Windows 驱动程序

下面是 Windows 10 版本 1709 中通用驱动程序的新增功能列表：

- [使用 Windows 更新来更新设备固件](./install/updating-device-firmware-using-windows-update.md) - 介绍如何使用 Windows 更新 (WU) 服务更新可移动设备或机箱内部设备的固件。
- [Reg2inf](./devtest/reg2inf.md) - 驱动程序包 INF 注册表转换工具 (reg2inf.exe) 可将注册表项及其值或者用于实现 DLL RegisterServer 例程的 COM.dll 转换成一组 INF AddReg 指令。 这些指令包含在驱动程序包 INF 文件中。

下面是 Windows 10 版本 1709 中通用驱动程序的更新列表：

- [通用驱动程序方案](./develop/dch-example.md)包含新的 COM 组件示例
- [INF AddComponent 指令](./install/inf-addcomponent-directive.md)
- [使用扩展 INF 文件](./install/using-an-extension-inf-file.md)
- [使用组件 INF 文件](./install/using-a-component-inf-file.md)

### <a name="wpp-software-tracing"></a>WPP 软件跟踪

[WPP 软件跟踪](./devtest/wpp-software-tracing.md) 引入了一项新功能： *即时 Trace 记录器*，在 Windows 10 中，版本1709。 如果驱动程序启用了 WPP 跟踪和 WPP 记录器，则会自动启用跟踪日志记录，你无需启动或停止跟踪会话即可轻松查看消息。 若要对日志进行更细微的控制，WPP 记录器允许 KMDF 驱动程序创建和管理自定义缓冲区。

- [用于日志跟踪的 WPP 记录器](./devtest/using-wpp-recorder.md)
- [WppRecorderLogGetDefault](/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-imp_wpprecorderloggetdefault)
- [WppRecorderLogCreate](/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)（仅限 KMDF）
- [WppRecorderDumpLiveDriverData](/windows-hardware/drivers/ddi/wpprecorder/nf-wpprecorder-wpprecorderdumplivedriverdata)

### <a name="audio"></a>音频

下面是 Windows 10 版本 1709 中 Windows 音频驱动程序开发的更新列表：

- 新的[配置和查询音频设备模块](./audio/configure-and-query-audiodevicemodules.md)
- 对[语音激活](./audio/voice-activation.md)做了大量更新
  - 有关仅限链接和关键字激活的更多详细信息
  - 新的词汇表
  - 有关训练和识别的更多信息，例如引脚和音频格式信息
  - 更新的关键字系统概述
  - 有关语音唤醒的更新信息

### <a name="acpi"></a>ACPI

下面列出了新的高级配置和电源接口 (ACPI) DDIs，支持 Windows 10 1709 版中的输入/输出缓冲区。

- [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V1](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)
- [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V1_EX](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)
- [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V2](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v2)
- [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V2_EX](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v2_ex)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V1](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V2](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v2)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V2_EX](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v2_ex)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V1](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V1_EX](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V2](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v2)
- [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V2_EX](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v2_ex)
- [ACPI_EVAL_INPUT_BUFFER_V1](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)
- [ACPI_EVAL_INPUT_BUFFER_V1_EX](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)
- [ACPI_EVAL_INPUT_BUFFER_V2](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v2)
- [ACPI_EVAL_INPUT_BUFFER_V2_EX](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v2_ex)
- [ACPI_EVAL_OUTPUT_BUFFER_V1](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)
- [ACPI_EVAL_OUTPUT_BUFFER_V2](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v2)
- [ACPI_METHOD_ARGUMENT_V1](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v1)
- [ACPI_METHOD_ARGUMENT_V2](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_method_argument_v2)
- [GIC_ITS](/windows-hardware/drivers/ddi/acpitabl/ns-acpitabl-_gic_its)

### <a name="biometric"></a>生物识别

Windows 10 版本1709中引入的 Windows 生物识别驱动程序有新的签名要求。 有关详细信息，请参阅[为 WBDI 驱动程序签名](./biometric/signing-wbdi-drivers.md)。

### <a name="display"></a>显示

Windows 10 版本1709中的 Windows 显示器驱动程序开发中引入了以下新功能。

- 显示色彩空间转换 DDI 针对合成后显示管道中应用的色彩空间转换提供更高的控制度。
- D3D12 复制队列时间戳查询功能可让应用程序针对 COPY 命令列表/队列发出时间戳查询。 这些时间戳的指定运行方式与其他引擎中的时间戳相同。
- 通过以下方式增强了视频与 Direct3D12 运行时的集成：
    1. 硬件加速的视频解码
    2. 内容保护
    3. 视频处理

### <a name="hardware-notifications"></a>硬件通知

Windows 10 版本1709添加了对硬件无关通知组件（例如 Led 和振动机制）的支持。 有关更多信息，请参阅：

- [硬件通知支持](./gpiobtn/hardware-notifications-support.md)
- [硬件通知参考](/windows-hardware/drivers/ddi/_gpiobtn/)

### <a name="windows-kernel"></a>Windows 内核

在 Windows 10 版本 1709 中，为驱动程序的 Windows 内核添加了多个新例程。

- ExGetFirmwareType 和 ExIsSoftBoot &ndash; 执行库支持例程。
- [PsSetLoadImageNotifyRoutineEx](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutineex) &ndash; 针对所有可执行映像的扩展映像通知例程，包括其体系结构与操作系统本机体系结构不同的映像。
- [MmMapMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapmdl) &ndash;[内存管理器](./kernel/windows-kernel-mode-memory-manager.md)例程，用于将内存描述符列表 (MDL) 描述的物理页面映射到系统虚拟地址空间。
- [PoFxSetTargetDripsDevicePowerState ](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxsettargetdripsdevicepowerstate) &ndash; 一个 PoFx 例程，用于向电源管理器告知 DRIPS 的设备目标电源状态。
- 为 [ZwSetInformationThread](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwsetinformationthread) 例程添加了以下与进程策略相关的选项：

  - [PROCESS_MITIGATION_CHILD_PROCESS_POLICY](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_process_mitigation_child_process_policy)
  - [PROCESS_MITIGATION_PAYLOAD_RESTRICTION_POLICY](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_process_mitigation_payload_restriction_policy)
  - PROCESS_READWRITEVM_LOGGING_INFORMATION

- [PsGetServerSiloActiveConsoleId](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetserversiloactiveconsoleid) 和 [PsGetParentSilo](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetparentsilo) &ndash; 接收器 api，用于获取在计算机上创建和销毁的服务器接收器的相关信息。
- 下面是新的 RTL 函数列表，通过这些函数可以使用关联矢量来引用事件和生成的日志，以进行诊断。
  - [CORRELATION_VECTOR](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-correlation_vector)
  - [RtlExtendCorrelationVector](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlextendcorrelationvector)
  - [RtlIncrementCorrelationVector](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlincrementcorrelationvector)
  - [RtlInitializeCorrelationVector](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlinitializecorrelationvector)
  - [RtlValidateCorrelationVector](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlvalidatecorrelationvector)

### <a name="mobile-broadband"></a>移动宽带

对于 windows 10 版本1709中的驱动程序开发，为 Windows Mobile 宽带和移动运营商方案添加了以下功能：

- [UICC 重置](./network/mb-low-level-uicc-access.md)和[调制解调器重置](./network/mb-modem-reset-operations.md)
- [协议配置操作 (PCO)](./network/mb-protocol-configuration-options-pco-operations.md)
- [基站信息查询](./network/mb-base-stations-information-query-support.md)
- [eSIM 卡和 MBIM ReadyState 指南](./network/mb-esim-mbim-ready-state-guidance.md)

在 Windows 10 版本 1709 中，[桌面版 COSA 文档](./mobilebroadband/planning-your-desktop-cosa-apn-database-submission.md)已更新，包括新的品牌相关字段。
有关对移动运营商方案所做的其他更改，请参阅[已弃用的功能](what-s-new-in-driver-development.md#deprecated-features)列表。

### <a name="networking"></a>网络

Windows 10 版本1709中添加了 Windows 网络驱动程序开发的这些新功能和改进。

下面是 NDIS 的新增功能和已更新功能列表：

- NetAdapterCx 1.1 简介，其中包括新的 NewAdapterCx 功能：
  - 更多的数据包上下文选项
  - 更精细的链接状态控制
  - 改进了接收缓冲区管理和性能
  - 一般性能改进
- NDIS 6.80 中新的[同步 OID 请求接口](./network/synchronous-oid-request-interface-in-ndis-6-80.md)
- NDIS 6.80 中新的[接收端缩放版本 2 (RSSv2)](./network/receive-side-scaling-version-2-rssv2-in-ndis-6-80.md)
- [NDIS 6.80 简介](./network/introduction-to-ndis-6-80.md)
- [将 NDIS 6.x 驱动程序移植到 NDIS 6.80](./network/porting-ndis-6-x-drivers-to-ndis-6-80.md)

### <a name="virtualized-pci"></a>虚拟化 PCI

在 Windows 10 1709 版中，添加了新的编程接口，用于写入符合 PCI Express 单根 i/o 虚拟化的设备的物理功能驱动程序 (SR-IOV) 规范。 接口在 Pcivirt.h 中声明。 有关详细信息，请参阅 [PCI 虚拟化](/windows-hardware/drivers/ddi/pcivirt/)。

### <a name="pulse-width-modulation-controllers"></a>脉冲宽度调制控制器

在 Windows 10 版本 1709 中，若要提供对已映射到 SoC 地址空间的 SoC 和内存中的脉宽调制 (PWM) 控制器的访问，需要编写一个内核模式驱动程序。 有关详细信息，请参阅 [SoC 中 PWM 模块的 PWM 驱动程序](/windows-hardware/drivers/spb/pulse-width-controller driver?branch=spb)。

若要分析和验证引脚路径和提取引脚编号，内核模型驱动程序应使用 [PwmParsePinPath](/windows-hardware/drivers/ddi/pwmutil/nf-pwmutil-pwmparsepinpath)。

应用可以通过发送 [PWM IOCTL](/windows-hardware/drivers/spb/pulse-width-controller driver#pwm-ioctl-requests) 请求，将请求发送到控制器驱动程序。

### <a name="file-systems-and-storage"></a>文件系统和存储

Windows 10 版本 1709 的文件系统和存储中添加了 ufs.h 标头，以提供对通用闪存存储的额外支持。

Posix 更新包括新的 **delete** 和 **rename** 函数。

下面是 Windows 10 版本 1709 中已更新的标头列表：

- ata.h
- fltKernel.h
- minitape.h
- ntddscsi.h
- ntddstor.h
- ntddvol.h
- ntifs.h
- scsi.h
- storport.h

### <a name="usb"></a>USB

在 Windows 10 版本1709中添加了这些新的 USB 功能。

#### <a name="media-agnostic-usb-ma-usb-protocol"></a>不区分媒体的 USB (MA-USB) 协议

USB 驱动程序堆栈可以使用不区分媒体的 USB (MA-USB) 协议，通过非 USB 物理媒体（例如 Wi-Fi）发送 USB 数据包。 为了实现此功能，我们已发布新的编程接口。 新的 DDI 可让驱动程序确定与 [_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_get_isoch_pipe_transfer_path_delays) 关联的延迟。 可以通过生成新的 URB 请求来检索该信息。
有关此新增功能的信息，请参阅以下主题：

- [不区分媒体的 (MA-USB) 协议的客户端驱动程序](./usbcon/usb-client-drivers-for-ma-usb.md)
- [_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS](/windows-hardware/drivers/ddi/usb/ns-usb-_urb_get_isoch_pipe_transfer_path_delays)
- [USB 请求块 (URB)](./usbcon/communicating-with-a-usb-device.md)

若要支持 MA-USB，主控制器驱动程序必须通过实现特定的回调函数来提供传输特征。 下表显示了支持 MA-USB 的回调函数和结构。

| 回调函数 | 结构 |
| ----- | ----- |
| [EVT_UCX_USBDEVICE_GET_CHARACTERISTIC](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_get_characteristic) | [UCX_ENDPOINT_ISOCH_TRANSFER_PATH_DELAYS](/windows-hardware/drivers/ddi/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_isoch_transfer_path_delays) |
| [EVT_UCX_USBDEVICE_RESUME](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_resume) | [UCX_CONTROLLER_ENDPOINT_CHARACTERISTIC_PRIORITY](/windows-hardware/drivers/ddi/ucxendpoint/ne-ucxendpoint-_ucx_endpoint_characteristic_priority) |
| [EVT_UCX_USBDEVICE_SUSPEND](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_suspend) | [UCX_ENDPOINT_CHARACTERISTIC](/windows-hardware/drivers/ddi/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_characteristic) |
| [EVT_UCX_ENDPOINT_GET_ISOCH_TRANSFER_PATH_DELAYS](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_get_isoch_transfer_path_delays) | [UCX_ENDPOINT_CHARACTERISTIC_TYPE](/windows-hardware/drivers/ddi/ucxendpoint/ne-ucxendpoint-_ucx_endpoint_characteristic_type) |
| [EVT_UCX_ENDPOINT_SET_CHARACTERISTIC](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_set_characteristic) | [UCX_ENDPOINT_ISOCH_TRANSFER_PATH_DELAYS](/windows-hardware/drivers/ddi/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_isoch_transfer_path_delays) |

#### <a name="synchronized-system-qpc-with-usb-frame-and-microframes"></a>系统 QPC 与 USB 帧和微帧同步

添加了新的编程接口，可检索系统查询性能计数器， (QPC) 值与帧和 microframe 同步。

仅当调用方在主控制器中启用了该功能时，才可以检索此信息。 若要启用此功能，主控制器驱动程序必须实现以下回调函数。

- [EVT_UCX_CONTROLLER_GET_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC](/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_get_frame_number_and_qpc_for_time_sync)
- [EVT_UCX_CONTROLLER_START_TRACKING_FOR_TIME_SYNC](/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_start_tracking_for_time_sync)
- [EVT_UCX_CONTROLLER_STOP_TRACKING_FOR_TIME_SYNC](/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_stop_tracking_for_time_sync)

应用程序可以使用以下 API 来启用/禁用该功能以及检索信息：

- [WinUsb_GetCurrentFrameNumberAndQpc](/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumberandqpc)
- [WinUsb_StartTrackingForTimeSync](/windows/desktop/api/winusb/nf-winusb-winusb_starttrackingfortimesync)
- [WinUsb_StopTrackingForTimeSync](/windows/desktop/api/winusb/nf-winusb-winusb_stoptrackingfortimesync)

其他驱动程序可以发送以下 IOCTL 请求来启用/禁用该功能以及检索信息：

- [IOCTL_USB_GET_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_frame_number_and_qpc_for_time_sync)
- [IOCTL_USB_START_TRACKING_FOR_TIME_SYNC](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_start_tracking_for_time_sync)
- [IOCTL_USB_STOP_TRACKING_FOR_TIME_SYNC](/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_stop_tracking_for_time_sync)

这些支持结构适用于带有 USB 帧和 microframes 的同步系统 OPC：

- [USB_START_TRACKING_FOR_TIME_SYNC_INFORMATION](/windows-hardware/drivers/ddi/usbioctl/ns-usbioctl-_usb_start_tracking_for_time_sync_information)
- [USB_STOP_TRACKING_FOR_TIME_SYNC_INFORMATION](/windows-hardware/drivers/ddi/usbioctl/ns-usbioctl-_usb_stop_tracking_for_time_sync_information)
- [USB_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC_INFORMATION](/windows-hardware/drivers/ddi/usbioctl/ns-usbioctl-_usb_frame_number_and_qpc_for_time_sync_information)

#### <a name="ioctl_ucmtcpci_port_controller_displayport_display_out_status_changed"></a>IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED

[IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED](/windows-hardware/drivers/ddi/ucmtcpciportcontrollerrequests/ni-ucmtcpciportcontrollerrequests-ioctl_ucmtcpci_port_controller_displayport_display_out_status_changed) 请求是 USB 类型 C 端口控制器接口框架扩展中的新请求。 此请求向客户端驱动程序告知 DisplayPort 连接的显示输出状态已更改。

这些结构支持 IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED 请求：

- [UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED_IN_PARAMS](/windows-hardware/drivers/ddi/ucmtcpciportcontrollerrequests/ns-ucmtcpciportcontrollerrequests-_ucmtcpci_port_controller_displayport_display_out_status_changed_in_params)
- [UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS](/windows-hardware/drivers/ddi/ucmtcpciportcontrollerrequests/ne-ucmtcpciportcontrollerrequests-_ucmtcpci_port_controller_displayport_display_out_status)