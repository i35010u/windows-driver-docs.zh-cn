---
title: Windows 10 版本 1809 的驱动程序开发变更
description: 本部分介绍 Windows 10 中驱动程序开发的新增功能。
ms.assetid: 764bcd98-c123-45e2-9dd1-44d54bb1addc
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 470b8084c484b72418621dac3431d900341b678e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066550"
---
# <a name="whats-new-in-windows-10-version-1809"></a>Windows 10 版本 1809 中的新增功能

本部分介绍 Windows 10 版本 1809（Windows 10 2018 年 10 月更新）中驱动程序开发的新增功能和更新。

## <a name="audio"></a><a name="audio-1809"></a>音频

现已发布有关新的 [sidebandaudio](/windows-hardware/drivers/ddi/sidebandaudio/) 和 [usbsidebandaudio](/windows-hardware/drivers/ddi/usbsidebandaudio/) 标头的文档。

## <a name="bluetooth"></a><a name="bluetooth-1809"></a>蓝牙

* HCI_VS_MSFT_Read_Supported_Features 已更新，包含用于安全简单配对过程的新标志。 请参阅 [Microsoft 定义的蓝牙 HCI 命令和事件](./bluetooth/microsoft-defined-bluetooth-hci-commands-and-events.md#hci_vs_msft_read_supported_features)。

* 以下网页提供了 Windows 10 版本 1809 的新 QDID：[108589](https://launchstudio.bluetooth.com/ListingDetails/55701)。 有关所有版本的 QD ID 完整列表，请参阅[蓝牙](/windows-hardware/design/component-guidelines/bluetooth)。

## <a name="windows-hardware-dev-center-dashboard"></a>Windows 硬件开发人员中心仪表板

在 Windows 10 版本 1809 中，在[硬件 API](./dashboard/dashboard-api.md) 方面，我们为开发人员、IHV 和 OEM 添加了新的和改进的功能，用于跟踪驱动程序包以及将其提交到 Windows 硬件仪表板。

使用发货标签 REST API 可以像分发驱动程序一样创建和管理发货标签。

* [管理发货标签](./dashboard/manage-shipping-labels.md)
* [获取发货标签数据](./dashboard/get-shipping-labels.md)

使用异步自定义报告方法可以访问驱动程序错误和 OEM 硬件错误的报告数据。 可根据需要定义报告模板、设置计划，系统会定期向你传送数据。

* [计划自定义报告以获取驱动程序故障详细信息](./dashboard/dashboard-api.md)

## <a name="debugging"></a>调试

对 Windows 10 版本1809的调试器进行的更改包括：

* **新的调试器数据模型 API** – 现已推出一个新的面向对象的调试器数据模型接口，该接口可使用 dbgmodel.h 标头支持调试器自动化。 调试器数据模型是一种可扩展的对象模型，它能够让新调试器扩展（包括 JavaScript、NatVis 和 C++ 中的扩展）使用来自调试器的信息并生成可从调试器及其他扩展访问的信息。 可以在调试器的 dx 表达式计算器中以及从 JavaScript 扩展或 C++ 扩展访问写入到数据模型 API 的构造。 文档位置：[调试器数据模型 C++ 接口概述](debugger/data-model-cpp-overview.md)和 [dbgmodel.h](/windows-hardware/drivers/ddi/dbgmodel/) 标头参考主题。

* **IPv6** - 我们将在 KDNET 中添加对 IPv6 的支持。 为了给 IPv6 所需的较大标头留出空间，我们减少了数据包的有效负载大小。 因此，我们将会声明 KDNET 协议的新版本，使运行最新版调试器的主机电脑可用于调试仅支持 IPv4 的目标电脑。 [https://aka.ms/windbgpreview](https://aka.ms/windbgpreview) 上提供了支持 IPv6 的 WinDbg 预览版。 请关注“Windows 调试工具”博客来了解有关 KDNET IPv6 支持的最新信息，并参阅[手动设置 KDNET 网络内核调试](./debugger/setting-up-a-network-debugging-connection.md)了解更多详细信息。

## <a name="device-and-driver-installation"></a>设备和驱动程序安装

在 Windows 10 版本 1809 中添加了以下内容：

* [INF AddEventProvider 指令](./install/inf-addeventprovider-directive.md)
* [INF DDInstall.Events 节](./install/inf-ddinstall-events-section.md)

更新了以下内容：

* [提前启动反恶意软件的要求](./install/elam-driver-requirements.md)
* [内核模式代码签名要求](./install/kernel-mode-code-signing-requirements--windows-vista-and-later-.md)

## <a name="display"></a><a name="display-1809"></a>显示

Windows 10 版本 1809 中的“显示”驱动程序开发的更新包括：

* **光线跟踪**：为了支持硬件加速的光线跟踪，我们在开发 Direct3D API 的同时开发了新的 Direct3D DDI。 示例 DDI 包括：[PFND3D12DDI_BUILD_RAYTRACING_ACCELERATION_STRUCTURE_0054](/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_build_raytracing_acceleration_structure_0054)、[PFND3D12DDI_COPY_RAYTRACING_ACCELERATION_STRUCTURE_0054](/windows-hardware/drivers/ddi/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_copy_raytracing_acceleration_structure_0054)。 有关光线跟踪的详细信息，请参阅[宣布推出 Microsoft DirectX 光线跟踪](https://devblogs.microsoft.com/directx/announcing-microsoft-directx-raytracing/)。

* **通用驱动程序要求**：WDDM 2.5 驱动程序需要确保其 DirectX11 UMD、DirectX12 UMD、KMD 以及这些组件加载的其他任何 DLL 遵守通用 API。

* **仅限 SRV 的平铺资源层 3**：在 Windows 10 版本 1809 中，GPU 能够更以更低的正交性支持平铺资源层 3 功能。 Direct3D12 现在支持稀疏体积纹理，而无需进行无序访问和渲染器目标操作。 仅限 SRV 的平铺资源层 3 是适合在第 2 层和第 3 层之间部署的概念层。 与当前的正交平铺资源层 3 一样，硬件支持是可选的。 但是，仅限 SRV 的平铺资源层 3 支持是一个超集层，需要平铺资源层 2 的支持。

   已播发正交平铺资源层 3 支持的驱动程序只需更新其驱动程序即可支持最新的“选项上限”DDI 结构版本。 对于已能支持正交平铺资源层 3 的任何硬件，运行时会将仅限 SRV 的平铺资源层 3 支持播发到应用程序。

* **渲染通道**：已添加渲染通道功能来实现以下目的：

  * 在现有的驱动程序上运行新的 API。
  * 使用户模式驱动程序能够选择最佳的渲染路径，且不会严重降低 CPU 的性能。

* **元命令**：元命令是代表 IHV 加速算法的 Direct3D12 对象。 它是对驱动程序实现的命令生成器的不透明引用。 元命令的更新包括描述符表绑定和纹理绑定。 请参阅 [D3D12DDI_META_COMMAND_PARAMETER_TYPE](/windows-hardware/drivers/ddi/d3d12umddi/ne-d3d12umddi-d3d12ddi_meta_command_parameter_type) 和 [D3D12DDIARG_META_COMMAND_PARAMETER_DESC](/windows-hardware/drivers/ddi/d3d12umddi/ns-d3d12umddi-d3d12ddiarg_meta_command_parameter_desc)。

  启用计算算法以使用纹理资源（重排内存）
  * 启用图形管道算法

* **HDR 亮度补偿**：引入了新的 SDR 亮度提升技术，以将 SDR 内容的参考白色部分提高到用户所需的值，这样就能够以 200-240 典型尼特值再现 SDR 内容，相当于用户预期的 SDR 显示效果。 SDR 亮度提升在两个方面会影响总体 Brightness3 行为：

  1. 只能在预先混合的前提下，针对 SDR 内容应用此提升。 HDR 内容不受影响。 同时，对于大多数笔记本电脑/brightness3 方案，用户预期所有内容（SDR 和 HDR）可调整。
  2. 当 OS 中的 Brightness3 堆栈确定所需的尼特值时，并不知道已经应用了 SDR 提升。

     驱动程序必须对来自 HDR Brightness3 DDI 的所需尼特值应用补偿。 由于图形驱动程序（和下游的 TCON 等）将会修改内容的像素值以获取所需的尼特值，因此，还应该对应用程序通过 [D3DDDI_HDR_METADATA_HDR10](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_hdr_metadata_hdr10) 提供的 HDR 内容元数据或者通过 [DxgkDdiSetTargetAdjustedColorimetry](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry) 提供的 OS 默认值应用补偿。 由于图形驱动程序 (TCON) 负责修改像素数据，因此驱动程序需负责补偿 HDR 内容元数据。

* **HDR 像素格式支持**：此内核模式设备驱动程序接口 (DDI) 更改包含在 WDDM 2.5 中，公开了驱动程序/设备报告的新功能，提供有关驱动程序/设备支持的 HDR 功能的信息。

   目前，OS 根据从 [DdiUpdateMonitorLinkInfo](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_updatemonitorlinkinfo) 读取的 [DXGK_MONITORLINKINFO_CAPABILITIES](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_monitorlinkinfo_capabilities) 结构的 *HighColorSpace* 位确定驱动程序/设备是否支持 HDR。 *HighColorSpace* 位提供以 HDR 模式运行的驱动程序/链接/监视功能的组合。

    驱动程序报告的 HDR 功能现在包括驱动程序/设备级功能，可让 OS 知道驱动程序/设备是支持真正的 HDR（即 FP16HDR），还是仅支持受限形式的 HDR（即 ARGB10HDR），相关定义如下：

  * FP16HDR：驱动程序/设备可将 FP16 像素格式图面与 scRGB/CCCS 色彩空间结合使用，并在运行扫描输出管道期间应用 PQ/2084 编码和 BT.2020 原色，以将输出信号转换为 HDR10。
  * ARGB10HDR：驱动程序/设备可以采用已经过 PQ/2084 编码的 ARGB10 像素格式图面，并扫描输出 HDR10 信号。 驱动程序/设备无法处理上面定义的 FP16HDR，也无法处理 scRGB FP16 的扩展数值范围。

    图形驱动程序只能报告 FP16HDR 或 ARGB10HDR 的支持，因为它们并不真正采用超集/子集配置；如果同时报告支持 FP16HDR 和 ARGB10HDR，则 OS 会使启动适配器失败。 请参阅 [DXGK_MONITORLINKINFO_CAPABILITIES](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_monitorlinkinfo_capabilities) 和 [_DXGK_DISPLAY_DRIVERCAPS_EXTENSION](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_display_drivercaps_extension)。

* **SDR 白水平**：内核模式设备驱动程序接口的更改包括将新的参数添加到现有的 DDI，使图形驱动程序知道 OS 复合器对所有在 HDR 模式下显示的 SDR 内容应用的“SDR 白水平”值。 请参阅“_DXGK_COLORIMETRY”。

## <a name="windows-kernel"></a><a name="kernel-1809"></a>Windows 内核

核心内核中添加了几个新的 API：

* [RtlQueryRegistryValueWithFallback 函数](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-rtlqueryregistryvaluewithfallback)：在缺少主句柄的情况下使用回退句柄查询注册表值项。
* [PsGetSiloContainerId 函数](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetsilocontainerid)和 [PsGetThreadServerSilo 函数](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psgetthreadserversilo)
* 已将新的信息类添加到 [_FILE_INFORMATION_CLASS](/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)
  * FileLinkInformationExBypassAccessCheck
  * FileCaseSensitiveInformationForceAccessCheck
  * FileStorageReserveIdInformation
    * FileLinkInformationEx
* 已将扩展的 NtCreateSection 版本添加到 [NtCreateSectionEx 函数](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatesectionex)，以指示这实际上是一个 AWE 节。
* 新的 Ex 宏授予对 Ntoskernel 导出的实际推送锁 API 的直接访问权限。
  * [ExAcquirePushLockExclusive 宏](/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirepushlockexclusive)
  * [ExAcquirePushLockShared 宏](/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirepushlockshared)
  * [ExInitializePushLock 函数](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepushlock)
  * [ExReleasePushLockExclusive 宏](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleasepushlockexclusive)
  * [ExReleasePushLockShared 宏](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleasepushlockshared)
* [KzLowerIrql](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kzlowerirql) 和 [KzRaiseIrql](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kzraiseirql) 已移到面向 Windows 8 和更高版本的内核组件的受支持外部 forceinline，而不依赖于转发器来实例化内联函数的特殊用例。
* 平展 PCI 的门户桥 (FPB) 现在受支持。 有关详细信息，请参阅[官方规范](https://pcisig.com/sites/default/files/specification_documents/ECN_FPB_9_Feb_2017.pdf)。 在 [Ntddk.h](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/) 中声明了新的 API (_PCI_FPB_*)。

## <a name="networking"></a><a name="networking-1809"></a>网络

## <a name="netadaptercx"></a>NetAdapterCx

* 新的 [NetAdapterCx 客户端驱动程序的 INF 文件](./netcx/inf-files-for-netadaptercx-client-drivers.md)主题。
* 传输和接收队列已合并成名为“数据包队列”的单个对象类型，以简化 API 图面。 已将标题为[轮询模型](./netcx/transmit-and-receive-queues.md#polling-model)的新部分添加到[传输和接收队列](./netcx/transmit-and-receive-queues.md)主题。
* 已将[硬件卸载](./netcx/netadaptercx-hardware-offloads.md)添加到 NetAdapterCx，该功能还可以自动注册客户端驱动程序的关联数据包扩展。
* 网络接口现在与驱动程序的 WDF 设备对象分离。 为了支持此功能，现已删除 *EvtNetAdapterSetCapabilities* 回调函数。 NetAdapterCx 客户端驱动程序现在可以包含多个网络接口，其中包括一个默认接口。

   更新的有关支持网络接口/设备对象分离的主题包括：

  * [NetAdapterCx 对象的摘要](./netcx/summary-of-netadaptercx-objects.md)
  * [设备和适配器初始化](./netcx/device-and-adapter-initialization.md)
  * [NetAdapterCx 客户端驱动程序的通电顺序](./netcx/power-up-sequence-for-a-netadaptercx-client-driver.md)
  * [NetAdapterCx 客户端驱动程序的断电顺序](./netcx/power-down-sequence-for-a-netadaptercx-client-driver.md)

* 支持 [NetAdapterCx 接收端缩放 (RSS)](./netcx/netadaptercx-receive-side-scaling-rss-.md) 的 DDI 已简化。
* 已删除数据包上下文标记帮助器宏。

## <a name="ndis"></a>NDIS

[接收端缩放版本 2 (RSSv2)](./network/receive-side-scaling-version-2-rssv2-.md) 已更新为版本 1.01。

## <a name="mobile-broadband"></a><a name="mobilebroadband-1809"></a>移动宽带

* 新的 [OID](./network/oid-wwan-mpdp.md) 和 DDI 可以支持 MBB 设备的多个数据包数据协议 (MPDP) 接口。
* 新的[基于设备的重置和恢复](./network/mb-device-based-reset-and-recovery.md)能够以更可靠的方式重置和恢复 MBB 设备与驱动程序。

## <a name="mobile-broadband-wdf-class-extension-mbbcx"></a>移动宽带 WDF 类扩展 (MBBCx)

MBBCx 电源管理方法已简化。

尽管 Windows 10 版本 1803 中提供 MBBCx 的预览内容，但 Windows 10 版本 1809 的 WDK 版本中随附了 MBBCx。

## <a name="mobile-operators"></a>移动运营商

现在，桌面版 COSA 支持 [AutoConnectOrder 设置](./mobilebroadband/desktop-cosa-apn-database-settings.md#apn-database-and-desktop-cosa-settings)。

## <a name="sensors"></a><a name="sensors-1809"></a>传感器

自动亮度调节功能支持：

已添加 PKEY_SensorData_IsValid 数据字段以支持传感器中的自动亮度调节。

有关详细信息，请参阅[光传感器数据字段](./sensors/light-sensor-data-fields.md)。

## <a name="universal-drivers-in-windows-10-version-1809"></a>Windows 10 版本 1809 中的通用驱动程序

从 Windows 10 版本 1809 开始，Windows 支持灵活链接，可让你使用单个二进制文件来以 OneCore 和桌面 SKU 为目标。
若要启用灵活链接，请使用以下新的 SDK API：

* [IsApiSetImplemented](/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented)

此现有主题已得到增强，其中介绍了如何使用灵活链接来满足 [DCHU 驱动程序设计原则](./develop/dch-principles-best-practices.md)的 U 要求：

* [针对 OneCore 生成](./develop/building-for-onecore.md)


## <a name="usb"></a><a name="usb-1809"></a>USB

**面向 USB 类型 C 驱动程序开发人员的新功能：**

如果硬件符合 UCSI 规范并且需要通过非 ACPI 传输进行通信，则你可以利用新的类扩展 &mdash; (UcmUcsiCx.sys)。 此扩展以传输无关的方式实现 UCSI 规范。 只需编写极少量的代码，驱动程序（即 UcmUcsiCx 的客户端）即可通过非 ACPI 传输来与 USB 类型 C 硬件通信。 本主题介绍 UCSI 类扩展提供的服务，以及客户端驱动程序的预期行为。

* [编写 UCSI 客户端驱动程序](./usbcon/write-a-ucsi-driver.md)
* [UcmUcsiCx 类扩展参考](/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)
* [UcmUcsiCx 客户端驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmUcsiAcpiSample)

**使用面向 USB 类型 C 驱动程序开发人员的新功能可以监视 USB 类型 C 连接器的活动和/或参与 USB 类型 C 连接器的策略决策。**

例如，根据热量状况控制设备的充电，使设备不会过热。

* [编写 USB 类型 C 策略管理器客户端驱动程序](https://www.microsoft.com/windows-hardware/drivers/usbcon/policy-manager-client)
* [Usbpmapi.h](/windows-hardware/drivers/ddi/usbpmapi/) 中提供了新的 API

**适用于模拟 USB 设备 (UDE) - 1.1 和 USB 主控制器 (Ucx) 1.5 的新版类扩展：**

模拟设备现在可通过功能 (FLDR) 和平台 (PLDR) 重置来支持更好的重置和恢复。 客户端驱动程序现在可让系统知道设备需要重置以及重置的类型：功能或平台。

* [UdecxWdfDeviceNeedsReset 函数](/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

主控制器还可通过以下方式选择 FLDR 和 PLDR 重置：

* [EVT_UCX_USBDEVICE_DISABLE](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)

## <a name="wi-fi"></a><a name="wifi-1809"></a>Wi-Fi

WLAN 设备驱动程序接口 (WDI) 规范已更新为版本 1.1.7。

* 添加了 WDI 驱动程序的最新 802.11ax PHY 类型的支持。
* 添加了未经请求的设备服务指示的支持。