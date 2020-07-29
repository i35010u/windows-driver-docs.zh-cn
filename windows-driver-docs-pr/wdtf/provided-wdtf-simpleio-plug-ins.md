---
title: 提供的 WDTF 简单 I/O 插件
description: 简单 i/o 插件是 Windows 驱动程序测试框架（WDTF）的扩展，用于实现特定于设备的特定 i/o 功能。
ms.assetid: 948E8CF5-24A1-4A7C-BD18-374F989AD053
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ace73923487e0e97601732548056aa2cbdabf0b
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264458"
---
# <a name="provided-wdtf-simple-io-plug-ins"></a>提供的 WDTF 简单 I/O 插件

简单 i/o 插件是 Windows 驱动程序测试框架（WDTF）的扩展，用于实现特定于设备的特定 i/o 功能。 如果为要测试的设备类型提供了插件，则[设备基本测试](https://docs.microsoft.com/windows-hardware/drivers)将使用 WDTF 简单 i/o 接口测试 i/o。

下表显示了具有简单 i/o 插件的设备类型。该表还指明了在测试设备时是否有特定要求。 使用[Windows 硬件认证工具包（HCK）](https://go.microsoft.com/fwlink/p/?linkid=254893)时，需要遵循这些要求。

如果未列出你的设备类型，则可以创建一个，请参阅[如何使用 WDTF Simple I/o 操作插件为设备自定义 i/o](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)

## <a name="provided-simple-io-plugins-and-device-requirements-for-testing-and-tips-for-troubleshooting"></a>为测试提供了简单的 i/o 插件和设备要求，并提供了故障排除提示

以下部分列出了具有简单 i/o 插件的设备类型。此部分还指示测试设备是否有特定要求。 使用[Windows 硬件认证工具包（HCK）](https://go.microsoft.com/fwlink/p/?linkid=254893)时，需要遵循这些要求。 本部分还介绍了可用于对测试失败进行故障排除和会审的提示。

* [音频设备](#audio)
* [蓝牙设备](#bluetooth)
* [CDROM 设备](#cdrom)
* [磁盘设备](#disk)
* [显示设备](#display)
* [GPS 设备](#gps-devices-and-gps-devices-in-systems)
* [LAN 设备](#lan)
* [移动宽带设备](#mobile-broadband)
* [便携设备](#portable-devices)
* [智能卡读卡器](#smart-card-readers)
* [传感器设备](#sensors)
* [数据量(Volume)](#volume)
* [网络摄像头](#webcam)
* [WLAN](#wlan)
* [USB 控制器和集线器与 Mutt](#usb-controller-and-hub-with-mutt)

有关具有特定要求的设备基础测试的列表，请参阅[具有特定设备配置要求的设备基础测试](#device-fundamental-tests-that-have-specific-device-configuration-requirements)

### <a name="audio"></a>音频

#### <a name="requirements"></a>要求

* 设备必须连接至少一个呈现类型终结点（扬声器、耳机等）。

* 如果目标音频设备具有 HDMI 视频和音频输出功能，若要执行音频测试，设备必须连接到 HDMI 音频功能设备，如 HDMI 监视器或 A/V 接收器。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 在呈现类型终结点上播放正弦微调。 捕获捕获类型终结点上的音频。

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

* 查看失败的 HRESULT 以执行初始会审。
* 如果测试未响应，请使用目标计算机上的内核调试器来缩小根本原因。
* 运行跟踪：
  * 启动内核跟踪：

```syntax
xperf.exe -on LOADER+PROC_THREAD+CSWITCH+DISK_IO+HARD_FAULTS+PROFILE+INTERRUPT+NETWORKTRACE+DPC+Latency+POWER -stackwalk ProcessCreate+ProcessDelete+ImageLoad+ImageUnload+ThreadCreate+ThreadDelete+CSwitch+ReadyThread+Profile+DiskFlushInit+FileFlush+RegFlush+HardFault+VirtualAlloc+VirtualFree -BufferSize 1024 -MinBuffers 512 -MaxBuffers 1024 -f Audio_SimpleIo_Kernel.etl
```

  * 启动音频跟踪：

```syntax
xperf.exe -start AudioSimpleIo -on Microsoft-Windows-Audio+a6a00efd-21f2-4a99-807e-9b3bf1d90285:0xffff:0x3 -BufferSize 1024 -MinBuffers 512 -MaxBuffers 1024 -f Audio_SimpleIo.etl
```

  * 运行测试。
  * 停止跟踪：

```syntax
xperf.exe -stop "NT Kernel Logger" Audio_SimpleIo
```

  * 合并跟踪：

```syntax
xperf.exe -merge Audio_SimpleIo_Kernel.etl Audio_SimpleIo.etl Audio_SimpleIo _Merged.etl
```

  * 查看包含 Xperf 的合并跟踪文件（**xperfview**）。

### <a name="bluetooth"></a>Bluetooth

#### <a name="requirements"></a>要求

* 无特殊要求。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 使用[**BluetoothFindFirstDevice 函数**](https://docs.microsoft.com/windows/desktop/api/bluetoothapis/nf-bluetoothapis-bluetoothfindfirstdevice)查找蓝牙设备。

### <a name="cdrom"></a>CDROM

#### <a name="requirements"></a>要求

* 已分配驱动器号。
* 媒体存在于设备中。
* 文件存在于插入的介质上。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 在 cd-rom 上查找文件，并使用 Win32 [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile) API 执行读取操作。

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

* 在测试计算机上，导航到相关的 CD/DVD 驱动器并确认你可以访问驱动器的内容。
* Cd-rom 简单 i/o 插件在 CD/DVD 上搜索要用于执行读取的 CD/DVD 上的文件。 确保 CD/DVD 中的文件在磁盘上进行了编码。
* 这个简单的 i/o 插件使用 Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)， [**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)， [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)函数。 返回的错误很可能是这些 Api 中的 Win32 错误代码。

### <a name="disk"></a>磁盘

#### <a name="requirements"></a>要求

* 磁盘至少分配有一个关联的卷驱动器号。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 使用简单的[卷](#volume)i/o 插件。

### <a name="display"></a>显示

#### <a name="requirements"></a>要求

* 没有特殊的测试要求。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 使用 D3DX Api 来运动图形适配器。

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

* 查看测试日志，该日志报告所使用的 Api 失败。

### <a name="gps-devices-and-gps-devices-in-systems"></a>GPS 设备（和系统中的 GPS 设备）

#### <a name="requirements"></a>要求

* 设备必须在具有适当 GPS 信号的位置进行测试。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 对[传感器](#sensors)使用 i/o 插件。

### <a name="lan"></a>LAN

#### <a name="requirements"></a>要求

* 设备有一个 IPv6 地址。

* 设备具有 IPv6 网关地址（否则，应将 WDTFREMOTESYSTEM 参数传递给测试，其中包含一个测试 NIC 能 ping 的 IPv6 地址）。

* 设备的网络操作状态为 "IfOperStatusUp"。

* 网络设备不是 WWAN 或 WLAN 设备。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* Ping IPv6 网络网关地址。

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

* 确认有一个现有的 IP 地址。
* 确认存在网关 IPv6 IP 地址。
* 手动确认 IP 网关地址（使用 ping.exe）。

### <a name="mobile-broadband"></a>移动宽带

#### <a name="requirements"></a>要求

* 没有特殊的测试要求。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 使用[**IMbnInterface 接口**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)并调用 GetHomeProvider、 [**IMbnInterface：： GetInterfaceCapability 方法**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterface-getinterfacecapability)和[**IMbnInterface：： GetReadyState 方法**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterface-getreadystate)api 来试验设备。

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

* MobileBroadbandPlugin 的区域可能会失败。

  * "MobileBroadbandPlugin：获取所有移动宽带接口时返回故障。"
  * "MobileBroadbandPlugin：获取接口时返回了失败。"
  * "MobileBroadbandPlugin：获取 DeviceId 返回的。"
  * "MobileBroadbandPlugin：获取接口功能返回失败"
  * "MobileBroadbandPlugin：获取 ReadyState 返回的失败。"

* 调查故障的最佳位置是从设备开始，并确定它是否无法指示就绪信息或设备功能。 若要调试更进一步的操作系统跟踪文件，需要收集。

  * 运行命令： **netsh trace start wwan \_ dbg**
  * 重现问题。
  * 运行命令： **netsh trace stop**

### <a name="portable-devices"></a>便携设备

#### <a name="requirements"></a>要求

* 设备具有可在其中创建文件夹和文件的存储组件。

**I/o 插件的类型执行：**

* 使用 WPD Api 读取文件并将其写入 WPD 设备上的存储组件。

### <a name="smart-card-readers"></a>智能卡读卡器

#### <a name="requirements"></a>要求

* 设备已插入 Athena T0 测试卡。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 读取数据并将数据写入读卡器中插入的 Athena T0 卡。

### <a name="sensors"></a>Sensors

#### <a name="requirements"></a>要求

* GPS 设备必须在具有适当 GPS 信号的位置进行测试。

### <a name="volume"></a>数据量(Volume)

#### <a name="requirements"></a>要求

* 已为卷分配驱动器号。
* 卷的可用空间为5MB。
* 卷不是写保护的。
* 媒体存在于设备中。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 创建名为 WDTF 的 \_ 目录 \_ ，并创建一个名为 SimpleIO 的文件。 I/o 是通过调用[**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)和[**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile) api 来执行的。

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

* 在测试计算机上，导航到相关驱动器并确认你可以访问驱动器的内容。
* 尝试将文件保存到驱动器。 确保可以轻松保存和访问。
* 这个简单的 i/o 插件使用 Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)， [**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)， [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)函数。 返回的错误很可能是这些 Api 中的 Win32 错误代码。

### <a name="webcam"></a>摄像头

#### <a name="requirements"></a>要求

* 没有特殊的测试要求。

    > [!NOTE]
    > 用于网络摄像机设备的简单 i/o 插件依赖于 MFPlat.dll 文件，该文件在不包括 Media Player 和相关技术的 Windows 版本（例如，Windows 7 N 或 Windows 7 KN）上不可用。 在这些版本的 Windows 上，必须安装媒体功能包。 媒体功能包可供下载。 有关详细信息，请参阅[知识库文章 968211](https://go.microsoft.com/fwlink/p/?linkid=266437)。

**I/o 插件的类型执行：**

* 使用媒体基础接口来捕获视频。

### <a name="wlan"></a>WLAN

#### <a name="requirements"></a>要求

* 请参阅 HCK 文档中[由设备基础测试记录的 WLAN SimpleIO 插件故障疑难解答](https://go.microsoft.com/fwlink/p/?linkid=309556)。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 请参阅 HCK 文档中[由设备基础测试记录的 WLAN SimpleIO 插件故障疑难解答](https://go.microsoft.com/fwlink/p/?linkid=309556)。

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

* 请参阅 HCK 文档中[由设备基础测试记录的 WLAN SimpleIO 插件故障疑难解答](https://go.microsoft.com/fwlink/p/?linkid=309556)。

### <a name="usb-controller-and-hub-with-mutt"></a>USB 控制器和集线器与 Mutt

#### <a name="requirements"></a>要求

* 没有特殊的测试要求。

    设备具有符号链接。

#### <a name="type-of-io-plug-in-performs"></a>I/o 插件的类型执行

* 使用 Microsoft USB 测试工具（MUTT）设备的 USB 传输测试。 所涵盖的传输类型包括控制、大容量、同步、中断和流（仅当 SuperMUTT 插入 USB 3.0 控制器时）

#### <a name="how-to-triage-test-failures"></a>如何对测试失败进行会审

* 首先检查测试日志文件中的消息。
* 在 USB 2.0 和 USB 3.0 堆栈上启用 Windows 事件跟踪（ETW），进一步进行调查。
  * 对于 USB 2.0，请参阅[windows 7 usb 核心堆栈中](https://go.microsoft.com/fwlink/p/?linkid=266442)的 MICROSOFT Windows USB 核心团队博客-ETW
  * 对于 USB 3.0，请参阅 Microsoft Windows USB 核心团队博客-[如何在 Windows 8 中捕获和读取 USB ETW 跟踪]( https://go.microsoft.com/fwlink/p/?linkid=266443)

## <a name="device-fundamental-tests-that-have-specific-device-configuration-requirements"></a>具有特定设备配置要求的设备基础测试

在运行以下[设备基本测试](https://docs.microsoft.com/windows-hardware/drivers)之前，必须根据针对特定设备类型所述的要求配置测试计算机上的设备。 请参阅提供的[简单 i/o 插件和设备要求](#provided-simple-io-plugins-and-device-requirements-for-testing-and-tips-for-troubleshooting)的列表。

* PCI 根端口意外删除测试（仅适用于 PCI 设备）
* 设备路径试验测试（认证）
* 使用 IO 前后的睡眠和 PNP （禁用和启用）（认证）
* 即插即用驱动程序测试（认证）
* 并发硬件和操作系统（混乱）测试（认证）
* 在之前和之后安装 IO （认证）
* 针对文件系统一致性的设备安装检查（认证）
* 其他设备稳定性的设备安装检查（认证）

## <a name="related-topics"></a>相关主题

[设备基础功能测试](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-fundamentals-tests)  
[如何在运行时使用 Visual Studio 测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)  
[如何在运行时从命令提示符测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)  
[如何选择和配置设备基础功能测试](https://docs.microsoft.com/windows-hardware/drivers)  
[设备基础测试疑难解答](https://docs.microsoft.com/windows-hardware/drivers)  
