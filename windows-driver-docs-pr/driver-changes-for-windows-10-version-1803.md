---
title: Windows 10 版本 1803 的驱动程序开发变更
description: 本部分介绍 Windows 10 中驱动程序开发的新增功能。
ms.assetid: 73ba8c40-d605-4dba-a965-0a87d80b9126
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: fa3811172b72c28bd696a41d11be1fd2cef3a999
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066552"
---
# <a name="whats-new-in-windows-10-version-1803"></a>Windows 10 版本 1803 中的新增功能

本部分介绍 Windows 10 版本 1803（Windows 10 2018 年 4 月更新）中驱动程序开发的新增功能和更新。

## <a name="acpi"></a><a name="acpi-1803"></a>ACPI

Windows 10 版本 1803 包含 ACPI DDI 的更新，支持平台功能和物理设备定位。

## <a name="audio"></a><a name="audio-1803"></a>音频

[语音激活](./audio/voice-activation.md)主题已更新，包括有关 APO 要求的附加信息。

## <a name="bluetooth"></a><a name="bluetooth-1803"></a>蓝牙

Windows 10 版本 1803 引入了迅速配对的支持。 用户不再需要在设置应用中导航并查找外设即可配对。 Windows 可以自动为用户完成配对。当附近出现新的外设并且该设备准备就绪时，Windows 会弹出一条通知。 确保外设进行迅速配对需要满足两套要求。 一套要求与外设的行为相关，另一套要求与 Microsoft 定义的供应商播发部分中的结构和值相关。 有关更多信息，请参阅：

* [蓝牙迅速配对](/windows-hardware/design/component-guidelines/bluetooth-swift-pair)
* [蓝牙功能和建议](/windows-hardware/design/component-guidelines/bluetooth)

Windows 10 版本 1803 支持蓝牙版本 5.0。 有关配置文件支持的信息，请参阅 [Windows 10 中的蓝牙版本和配置文件支持](./bluetooth/general-bluetooth-support-in-windows.md)。

## <a name="camera"></a><a name="camera-1803"></a>相机

对相机驱动程序开发的更新包括：

* [适用于 UVC 设备的 DShow (DirectShow) 桥实施指南](./stream/dshow-bridge-implementation-guidance-for-usb-video-class-devices.md) - 有关配置符合 USB 视频类 (UVC) 规范的相机和设备的 DShow 桥的实施指南。 平台使用 USB 总线标准中的 Microsoft OS 描述符来配置 DShow 桥。 扩展属性 OS 描述符是 USB 标准描述符的扩展，USB 设备使用它来返回尚未通过标准规范启用的 Windows 特定设备属性。
* [全景相机视频捕获](./stream/360-camera-video-capture.md) - 使用现有的 MediaCapture API 提供全景相机预览、捕获和记录支持。 平台可以使用此功能来公开球形帧源（例如 equirectangular 帧），使应用能够检测和处理全景视频相机流，以及提供全景拍摄体验。

## <a name="debugging"></a>调试

对 Windows 10 版本1803的调试器进行的更改包括：

[WinDbg 预览版时光穿越调试 (TTD) 动手实验](./debugger/time-travel-debugging-walkthrough.md) - 此实验使用一个存在代码缺陷的示例小程序介绍时光穿越调试 (TTD)。 TTD 用于调试、识别问题及分析其根本原因。

## <a name="display"></a><a name="display-1803"></a>显示

下面是对 Windows 10 版本 1803 中的“显示”驱动程序开发的更新：

* **间接显示 UMDF 类扩展** - 间接显示驱动程序可将 SRM 传递给渲染 GPU，并提供一种机制用于查询所用的 SRM 版本。

* **基于 IOMMU 硬件的 GPU 隔离支持** - 通过限制 GPU 访问系统内存来提高安全性。

* **GPU 半虚拟化支持** - 可让显示驱动程序在 Hyper-V 虚拟化环境中提供渲染功能。

* **亮度** - 提供新的亮度接口来支持多个显示器，这些显示器可设置为基于校准尼特值的亮度水平。

* **D3D11 位流加密** - 在 D3D11 中提供更多的 GUID 和参数来支持公开包含 8 或 16 字节初始化矢量的 CENC、CENS、CBC1 和 CBCS。

* **D3D11 和 D3D12 视频解码直方图** - 借助照度直方图，媒体团队可以利用直方图的固定功能硬件来改善 HDR/EDR 方案的音调映射质量。 当这些方案已经饱和使用了 GPU 或者想要启用并行处理时，固定功能硬件非常有用。 此功能是可选的。仅当固定功能硬件可用时，才应该实现此功能。 不应配合 3D 或计算方案实现此功能。

* **D3D12 视频解码**现在支持解码层 II，指示驱动程序支持纹理阵列，可在分辨率发生更改时，让应用程序分摊分配成本并减少峰值内存使用量。 

* **平铺资源层和 LDA 原子性** - 提供新的跨节点共享层，以添加对跨链接适配器 (LDA) 节点工作的原子着色器指令的支持。 这提高了 ISV 实现多种 GPU 渲染技术（例如分割帧渲染 (SFR)）的能力，并且与 D3D11 相比，将功能提高到了新的层次。

* **GPU 递色支持** - 驱动程序可以报告给定计时模式下针对网络信号执行递色的能力。 这样，当所需的位深度效率高于监视链路实际所能提供的效率时（例如需要 HDR10 而不是 HDMI 2.0），OS 可以显式请求递色。

* **后处理颜色增强覆盖** - 可让 OS 请求驱动程序暂时禁用任何增强或更改显示颜色的后处理功能。 这可以支持如下所述的方案：特定的应用程序能够以比色方式在显示器上实施准确的色彩行为，并安全地与 OEM 或 IHV 专属显示颜色增强功能共存。

* **Direct3D12 和视频** - 新的 API 和 DDI 提供对以下功能的访问：
  * 硬件加速的视频解码
  * 内容保护
  * 视频处理

* **DisplayID** - 一个新的 DDI，旨在通过受图形适配器控制的，并且应该支持 DisplayID v1.3 和 DisplayID v2.0 的显示器查询 VESA 的 DisplayID 描述符。 DDI 是现有 DxgkDdiQueryAdapterInfo DDI 的扩展，应受 DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM2_3 的所有驱动程序的支持，包括仅限内核模式显示的驱动程序和间接显示驱动程序。

* **GPU 性能数据** - DdiQueryAdapterInfo 的扩展将公开温度、风扇速度、引擎和内存时钟速度、内存带宽、功耗和电压等信息

* 杂项 - 新的 SupportContextlessPresent 驱动程序上限可帮助 IHV 载入新驱动程序。

* 改进了 OS 中的外部/可移动 GPU 支持。 作为改进支持的第一步，Dxgkrnl 需要确定 GPU 是否“可分离”，即可热插拔。 对于 RS4，我们希望利用此方面的驱动程序信息，而不是生成自己的基础结构。 为此，我们将在 DXGK_ DRIVERCAPS 结构中添加“Detachable”位。 如果适配器可热插拔，则在适配器初始化期间，驱动程序会设置此位。

* **显示诊断** - 内核模式设备驱动程序接口 (DDI) 已发生更改，允许显示控制器的驱动程序向 OS 报告诊断事件。  这就提供了一个通道来让驱动程序记录事件，否则 OS 看不到这些事件，因为事件不是 OS 请求的响应，也不是 OS 需要应对的对象。

* **共享图形电源组件** - 使非图形驱动程序能够参与图形设备的电源管理。  非图形驱动程序将配合图形驱动程序，使用某个驱动程序接口来管理其中一个或多个共享的电源组件。

* **共享纹理改进** - 包括增加了可在进程和 D3D 设备之间共享的纹理类型。 此设计使得帧服务器 OS 组件能够以极少量的内存复制来支持单色。

## <a name="driver-security"></a><a name="security-1803"></a>驱动程序安全性

对 [Windows 驱动程序安全指南](./driversecurity/index.md)和[驱动程序安全清单](./driversecurity/driver-security-checklist.md)做了更新，为驱动程序开发人员提供驱动程序安全清单。

## <a name="windows-kernel"></a><a name="kernel-1803"></a>Windows 内核

本部分介绍 Windows 10 版本 1803 中的 Windows 内核驱动程序开发的新增功能和已更新的功能。

已将一组新 API 添加到工具包，使第三方能够创建其自己的 KDNET 扩展模块或 KdSerial 传输层。 有关示例代码，请参阅 Debuggers 文件夹中的“内核传输示例”(ddk\samples\kdserial and ddk\samples\kdnet)。

添加了相应的支持，为驱动程序提供一个可以存储文件状态的批准位置（操作系统知道该位置）。  使用此方法时，系统可将该位置中的文件与某个设备或驱动程序相关联。

有不同的位置用于存储特定于驱动程序内部组件或特定于设备的文件状态。 对于包含文件状态的驱动程序，可以确定写入到磁盘的状态是：

* 驱动程序状态 ([IoGetDriverDirectory](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdriverdirectory))：可能正在控制多个设备的驱动程序的全局状态，还是

* 设备状态 ([IoGetDeviceDirectory](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicedirectory))：特定于驱动程序控制的单个设备，其他设备可能对类似的状态使用不同的值。

现在，当功能驱动程序 (FDO) 的相应 PCIe 设备处于 D3Cold 状态时，可与其他电源协商。 这包括：

* 辅助电源要求 [D3COLD_REQUEST_AUX_POWER](/windows-hardware/drivers/ddi/wdm/nc-wdm-d3cold_request_aux_power)。
* 核心电源导轨 [D3COLD_REQUEST_CORE_POWER_RAIL](/windows-hardware/drivers/ddi/wdm/nc-wdm-d3cold_request_core_power_rail)。
* 在从 PCI Express 下游端口收到消息，到相应终结点或 PCI Express 下游端口在系统处于 ACPI 工作状态时转换为 D3cold 期间平台将 PERST# 断言到插槽的固定延迟时间要求。 请参阅 [D3COLD_REQUEST_PERST_DELAY](/windows-hardware/drivers/ddi/wdm/nc-wdm-d3cold_request_perst_delay)。

NT 服务以及内核模式和用户模式驱动程序可以使用 [RtlRaiseCustomSystemEventTrigger](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlraisecustomsystemeventtrigger) 函数针对设备引发自定义触发器。 驱动程序开发人员拥有的自定义触发器通知系统事件代理使用自定义触发器标识符标识的触发器启动关联的后台任务。

现在，可以在激发通知时注册活动会话更改通知并获取回调。 作为此通知的一部分，某些数据还会与调用方共享。 这些关联的数据通过 [PO_SPR_ACTIVE_SESSION_DATA 结构](/windows-hardware/drivers/ddi/ntpoapi/ns-ntpoapi-_po_spr_active_session_data)传送。

## <a name="networking"></a><a name="networking-1803"></a>网络

本部分概述 Windows 10 版本 1803 中 Windows 网络驱动程序开发的新增功能和改进。

## <a name="ndis-and-netadaptercx"></a>NDIS 和 NetAdapterCx

NDIS 的更新包括：

* [接收端缩放 V2](./network/receive-side-scaling-version-2-rssv2-in-ndis-6-80.md) 已更新，包括有关操纵参数的更多详细信息
* [同步 OID 接口](./network/synchronous-oid-request-interface-in-ndis-6-80.md)现在支持 NDIS 轻型筛选器驱动程序

下面是网络适配器 WDF 类扩展 (NetAdapterCx) 的新主题：

* [NetAdapterCx 1.2 简介](./netcx/index.md)
* [数据包描述符和扩展](./netcx/packet-descriptors-and-extensions.md)
* [网络数据缓冲区管理](./netcx/network-data-buffer-management.md)
* [NetAdapterCx 接收端缩放 (RSS)](./netcx/netadaptercx-receive-side-scaling-rss-.md)

此外，为仅限预览的功能 - 移动宽带类扩展 (MBBCx) 提供了新的主题。该功能使用 NetAdapterCx 模型建立移动宽带连接。

* [移动宽带类扩展 (MBBCx)](./netcx/mobile-broadband-mbb-wdf-class-extension-mbbcx.md)
  * [编写 MBBCx 客户端驱动程序](./netcx/writing-an-mbbcx-client-driver.md)
  * [MBBCx API 参考](/windows-hardware/drivers/ddi/_netvista/)

## <a name="mobile-broadband"></a><a name="mobilebroadband-1803"></a>移动宽带

在移动宽带中，提供了详细介绍 [MB 低级别 UICC 访问](./network/mb-low-level-uicc-access.md)的新主题。

## <a name="mobile-operators"></a>移动运营商

[桌面版 COSA](./mobilebroadband/desktop-cosa-apn-database-settings.md#desktop-cosa-only-settings) 现在包括新的热点和 AppID 设置。 强烈建议移动运营商从使用 [Sysdev 元数据包](./mobilebroadband/service-metadata.md)的宽带应用体验过渡到 [MO UWP 应用](./mobilebroadband/uwp-mobile-broadband-apps.md)和 [COSA 数据库](./mobilebroadband/desktop-cosa-apn-database-settings.md)。

## <a name="pcie"></a><a name="pci-1803"></a>PCIe

添加了新的 ACPI _DSD 方法用于支持以下新式待机和 PCI 热插拔方案：

* PCIe 根端口上的定向最深运行时空闲电源状态 (DDRIPS) 支持
* 在 D3 中识别支持热插拔的 PCIe 根端口
* 识别外部公开的 PCIe 根端口

有关信息，请参阅 [ACPI 接口：PCIe 根端口的设备特定数据 (_DSD)](./pci/dsd-for-pcie-root-ports.md)。

## <a name="sensors"></a><a name="sensors-1803"></a>传感器

添加了 [SENSOR_CONNECTION_TYPES 枚举](/windows-hardware/drivers/ddi/sensorsdef/ne-sensorsdef-sensor_connection_types)用于澄清连接类型属性。

## <a name="usb"></a><a name="usb-1803"></a>USB

添加了新的 API 用于模拟共享连接器的分离。 如果 USB 设备已附加到主机，或者在删除堆栈时包含共享连接器，则你可以模拟分离事件。 此时已禁用所有附加/分离通知机制。 有关详细信息，请参阅 [UfxDeviceNotifyFinalExit 函数](/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyfinalexit)。

## <a name="wi-fi"></a><a name="wifi-1803"></a>Wi-Fi

Wi-Fi 驱动程序开发的更新包括添加了新的[用于 NIC 自动电源保护程序 (NAPS) 高级电源管理的 TLV 功能](./network/wdi-tlv-os-power-management-features.md)，以及对平台级设备恢复服务 (PLDR) 的更新。