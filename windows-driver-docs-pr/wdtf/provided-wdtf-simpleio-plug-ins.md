---
title: 提供的 WDTF 简单 I/O 插件
description: 简单 I/O 插件是实现泛型特定于设备的 I/O 功能扩展到 Windows 驱动程序测试框架 (WDTF)。
ms.assetid: 948E8CF5-24A1-4A7C-BD18-374F989AD053
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c56049d8e203018f80c9531897d9b477c823532
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369487"
---
# <a name="provided-wdtf-simple-io-plug-ins"></a>提供的 WDTF 简单 I/O 插件

简单 I/O 插件是实现泛型特定于设备的 I/O 功能扩展到 Windows 驱动程序测试框架 (WDTF)。 如果所测试的设备类型的插件存在[设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)使用测试 I/O 的 WDTF 简单 I/O 接口。

下表显示了简单的 I/O 插件的设备类型。此表还指示是否存在针对测试设备的特定要求。 这些是你需要在你使用时应遵循的相同要求[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)。

如果未列出你的设备类型，可以创建一个，请参阅[如何为你的设备使用 WDTF 简单 I/O 操作插件自定义 I/O](to-customize-i-o-for-your-device-using-the-wdtf-simple-i-o-action-plug-in.md)

## <a name="provided-simple-io-plugins-and-device-requirements-for-testing-and-tips-for-troubleshooting"></a>用于测试和故障排除的提示提供简单的 I/O 插件和设备要求

以下部分列出了具有简单 I/O 插件的设备类型。部分也可指示是否存在针对测试设备的特定要求。 这些是你需要在你使用时应遵循的相同要求[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)。 部分还说明了可用于进行故障排除和会审的提示测试失败。

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
* [卷](#volume)
* [Webcam](#webcam)
* [WLAN](#wlan)
* [USB 控制器和使用 Mutt 中心](#usb-controller-and-hub-with-mutt)

具有特定要求的设备基础测试的列表，请参阅[具有特定设备的配置要求的设备基础测试](#device-fundamental-tests-that-have-specific-device-configuration-requirements)

### <a name="audio"></a>Audio

#### <a name="requirements"></a>要求

* 设备必须具有至少一个呈现类型端点连接 （扬声器、 耳机等）。

* 如果目标音频设备有 HDMI 视频和音频输出功能，以执行音频测试时，设备必须连接到 HDMI 音频支持设备如 HDMI 监视器或 A / V 接收方。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 播放正弦值优化呈现类型终结点。 捕获音频捕获类型终结点上。

#### <a name="how-to-triage-test-failures"></a>如何进行会审测试失败

* 查看失败的 HRESULT 来执行初步分类。
* 如果测试没有响应，使用目标计算机上内核调试程序来缩小根本原因。
* 运行的跟踪：
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

  * 查看使用 Xperf 合并的跟踪文件 (**xperfview**)。

### <a name="bluetooth"></a>蓝牙

#### <a name="requirements"></a>要求

* 没有特殊的要求。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 使用[ **BluetoothFindFirstDevice 函数**](https://docs.microsoft.com/windows/desktop/api/bluetoothapis/nf-bluetoothapis-bluetoothfindfirstdevice)查找 Bluetooth 的设备。

### <a name="cdrom"></a>CDROM

#### <a name="requirements"></a>要求

* 分配的驱动器号。
* 介质所在的设备中。
* 有上插入的媒体文件。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 查找在 CD-ROM 上的文件，并执行读取的操作使用 Win32 [ **ReadFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile) API。

#### <a name="how-to-triage-test-failures"></a>如何进行会审测试失败

* 在测试计算机上，导航到相关的 CD/DVD 驱动器并确认可以访问的驱动器的内容。
* 要用于执行读取从 CD/DVD 上的文件 CD-Rom 简单 I/O 插件搜索。 请确保 CD/DVD 具有编码在磁盘上的文件。
* 此简单 I/O 即插即用使用 Win32 [ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)， [ **WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)， [ **ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)函数。 返回的错误是最有可能从这些 Api 的 Win32 错误代码。

### <a name="disk"></a>Disk

#### <a name="requirements"></a>要求

* 磁盘都有至少一个关联的卷分配号的驱动器。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 使用简单的 I/O 插件[卷](#volume)。

### <a name="display"></a>显示

#### <a name="requirements"></a>要求

* 测试没有特殊要求。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 使用 D3DX Api 来执行图形适配器。

#### <a name="how-to-triage-test-failures"></a>如何进行会审测试失败

* 仔细查看测试日志，哪些报表使用的 Api 中的失败。

### <a name="gps-devices-and-gps-devices-in-systems"></a>GPS 设备 （和在系统中的 GPS 设备）

#### <a name="requirements"></a>要求

* 设备必须使用正确的 GPS 信号的位置中进行测试。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 使用插件 I/O[传感器](#sensors)。

### <a name="lan"></a>LAN

#### <a name="requirements"></a>要求

* 设备具有 IPv6 地址。

* 设备具有 IPv6 网关地址 （否则 WDTFREMOTESYSTEM 参数应传递给测试的测试 NIC 可以 ping 通的 IPv6 地址）。

* 设备的网络操作状态是 IfOperStatusUp。

* 网络设备不是 WWAN 或 WLAN 设备。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* Ping IPv6 网络网关地址。

#### <a name="how-to-triage-test-failures"></a>如何进行会审测试失败

* 确认有现有的 IP 地址。
* 请确认网关 IPv6 IP 地址。
* 手动确认 IP 网关地址 （使用 ping.exe）。

### <a name="mobile-broadband"></a>移动宽带

#### <a name="requirements"></a>要求

* 测试没有特殊要求。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 使用[ **IMbnInterface 接口**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface) ，并调用 GetHomeProvider， [ **IMbnInterface::GetInterfaceCapability 方法**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterface-getinterfacecapability)，和[**IMbnInterface::GetReadyState 方法**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterface-getreadystate) Api 来执行该设备。

#### <a name="how-to-triage-test-failures"></a>如何进行会审测试失败

* MobileBroadbandPlugin 具有有限的区域可能会失败。

  * "MobileBroadbandPlugin:获取所有的移动宽带接口返回了失败。"
  * "MobileBroadbandPlugin:获取返回失败的接口。"
  * "MobileBroadbandPlugin:获取返回的 DeviceId。"
  * "MobileBroadbandPlugin:获取界面功能返回了失败"
  * "MobileBroadbandPlugin:获取 ReadyState 返回了失败。"

* 请查找该故障的最佳位置启动从设备，并确定它是否无法指示设备功能或准备就绪的信息。 若要进一步调试 OS 跟踪文件需要进行收集。

  * 运行命令： **netsh 跟踪启动 wwan\_dbg**
  * 重现问题。
  * 运行命令： **netsh trace stop**

### <a name="portable-devices"></a>便携设备

#### <a name="requirements"></a>要求

* 设备已在其中创建文件夹和文件存储组件。

**执行 I/O 插件的类型：**

* 读取并使用 WPD Api WPD 设备上将文件写入到存储组件。

### <a name="smart-card-readers"></a>智能卡读卡器

#### <a name="requirements"></a>要求

* 设备了 Athena T0 测试卡插入。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 读取和写入到 Athena T0 卡插入读卡器中的数据。

### <a name="sensors"></a>传感器

#### <a name="requirements"></a>要求

* GPS 设备必须使用正确的 GPS 信号的位置中进行测试。

### <a name="volume"></a>Volume

#### <a name="requirements"></a>要求

* 卷已分配了驱动器号。
* 卷具有 5 MB 的可用空间。
* 卷不被写保护。
* 介质所在的设备中。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 创建一个名为 WDTF 目录\_卷\_IO，并创建一个名为 SimpleIO.tmp 文件。 通过调用来执行 I/O [ **ReadFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)并[ **WriteFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile) Api 对此文件。

#### <a name="how-to-triage-test-failures"></a>如何进行会审测试失败

* 在测试计算机上，导航到相关的驱动器，并确认可以访问该驱动器的内容。
* 尝试将文件保存到驱动器。 请确保可以保存并随时对其进行访问。
* 此简单 I/O 即插即用使用 Win32 [ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)， [ **WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)， [ **ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)函数。 返回的错误是最有可能从这些 Api 的 Win32 错误代码。

### <a name="webcam"></a>Webcam

#### <a name="requirements"></a>要求

* 测试没有特殊要求。

    > [!NOTE]
    > 简单的 I/O 的网络摄像机设备插件具有 MFPlat.dll 文件，其中不包括媒体播放机和相关的技术，例如 Windows 7 N 或 Windows 7 KN 的 Windows 版本上不可用的依赖关系。 在这些版本的 Windows 上，必须安装媒体功能包。 媒体功能包是可供下载。 有关详细信息，请参阅[KB 文章 968211](https://go.microsoft.com/fwlink/p/?linkid=266437)。

**执行 I/O 插件的类型：**

* 使用媒体基础接口捕获视频。

### <a name="wlan"></a>WLAN

#### <a name="requirements"></a>要求

* 请参阅[由设备基础测试记录的故障排除 WLAN SimpleIO 插件失败](https://go.microsoft.com/fwlink/p/?linkid=309556)HCK 文档中。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* 请参阅[由设备基础测试记录的故障排除 WLAN SimpleIO 插件失败](https://go.microsoft.com/fwlink/p/?linkid=309556)HCK 文档中。

#### <a name="how-to-triage-test-failures"></a>如何进行会审测试失败

* 请参阅[由设备基础测试记录的故障排除 WLAN SimpleIO 插件失败](https://go.microsoft.com/fwlink/p/?linkid=309556)HCK 文档中。

### <a name="usb-controller-and-hub-with-mutt"></a>USB 控制器和使用 Mutt 中心

#### <a name="requirements"></a>要求

* 测试没有特殊要求。

    设备有一个符号链接。

#### <a name="type-of-io-plug-in-performs"></a>执行的 I/O 插件类型

* USB 传输测试使用 Microsoft USB 测试工具 (MUTT) 设备。 涵盖的传输类型为控件、 大容量等时，中断和流 （仅当 SuperMUTT 插入到 USB 3.0 控制器）

#### <a name="how-to-triage-test-failures"></a>如何进行会审测试失败

* 先检查测试日志文件中的消息。
* 通过 USB 2.0 和 USB 3.0 在堆栈上启用事件跟踪 Windows (ETW) 进一步调查。
  * USB 2.0，请参阅 Microsoft Windows USB 核心团队博客- [Windows 7 USB core 堆栈中的 ETW](https://go.microsoft.com/fwlink/p/?linkid=266442)
  * USB 3.0，请参阅 Microsoft Windows USB 核心团队博客-[如何捕获和阅读 Windows 8 中的 USB ETW 跟踪]( https://go.microsoft.com/fwlink/p/?linkid=266443)

## <a name="device-fundamental-tests-that-have-specific-device-configuration-requirements"></a>具有特定设备的配置要求的设备基础测试

运行以下之前[设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)，必须根据特定设备类型所述的要求配置在测试计算机上的设备。 请参阅列表[提供简单的 I/O 插件和设备要求。](#provided-simple-io-plugins-and-device-requirements-for-testing-and-tips-for-troubleshooting)

* PCI 根端口意外删除测试 （仅限 PCI 设备）
* 设备路径试验程序测试 （认证）
* 睡眠和 PNP （禁用和启用） IO 前后的 （认证）
* Plug and Play 驱动程序测试 （认证）
* 并发硬件和操作系统 (CHAOS) 测试 （认证）
* 重新安装与 IO 之前和之后 （认证）
* 针对文件系统一致性 （认证） 设备安装检查
* 针对其他设备稳定性 （认证） 设备安装检查

## <a name="related-topics"></a>相关主题

[设备基础功能测试](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-fundamentals-tests)  
[如何在运行时使用 Visual Studio 测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)  
[如何测试在运行时从命令提示符下的驱动程序](https://docs.microsoft.com/windows-hardware/drivers)  
[如何选择和配置设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)  
[故障排除设备基础测试](https://docs.microsoft.com/windows-hardware/drivers)  
