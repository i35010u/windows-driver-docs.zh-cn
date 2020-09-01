---
title: 支持无线电管理
description: 当用户在其 Windows 8 便携式计算机、笔记本或平板电脑上的 "电脑设置" 中选择 "无线" 选项时，他们可以打开或关闭任何连接的无线设备。
ms.assetid: AA7AB429-30C5-4C10-AA85-41ED9EAEE69A
keywords:
- 收音机管理 API
- 收音机管理 API，示例
- 收音机管理，示例
- GPS 收音机管理
- 收音机管理，GPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf052d0c9b63a89aad719b57d780e4300869d6bd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193257"
---
# <a name="supporting-radio-management"></a>支持无线电管理

> [!IMPORTANT]
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

当用户在其 Windows 8 便携式计算机、笔记本或平板电脑上的 "电脑设置" 中选择 "无线" 选项时，他们可以打开或关闭任何连接的无线设备。 这些无线设备可能包括 Wi-fi 天线或 GPS 设备。 PC 设置与给定无线设备之间的内部链接是 [无线电管理 API](/previous-versions/windows/hardware/radio/hh406615(v=vs.85)) 和给定设备的相应收音机管理 DLL。

收音机管理 API 是一组作为 Windows 驱动程序工具包附带的 COM/Win32 接口。 这些接口包括以下方法：

- 检索无线设备的当前状态

- 支持收音机设备的通知事件

- 检索设备属性， (如友好名称) 

这些接口仅适用于 Oem 和 Ihv，而不是应用程序开发人员。

## <a name="the-radio-management-dynamic-link-library-dll"></a>收音机管理动态链接库 (DLL) 

如果为收音机设备创建设备驱动程序，如 GPS，则驱动程序将需要包含附加的动态链接库 (DLL) ，该库支持收音机管理 API 中的接口。 为了帮助你了解此 DLL 的要求，Microsoft 提供了一个示例 Microsoft Visual Studio 项目和源代码，作为地理位置驱动程序示例的一部分。 此示例项目 SampleRM，请参阅驱动程序示例的传感器地理位置驱动程序示例 \\ c + + \\ RadioManagerGPS 文件夹中的 .vcxproj。 它包括七个 c + + 源文件、六个 c + + 头文件、一个模块定义文件、一个资源文件、两个 IDL 文件、一个注册表文件 (用于注册 DLL) 和一个安装脚本。

下表列出了无线电管理 API 中的方法和示例 DLL 中的相应方法。

**收音机管理器 API**：收音机管理器 DLL

**IMediaRadioManager：： GetRadioInstances**： CSampleRadioManager：： GetRadioInstances

**IMediaRadioManager：： OnSystemRadioStateChange**： CSampleRadioManager：： OnSystemRadioStateChange

**IRadioInstance：： GetFriendlyName**： CSampleRadioInstance：： GetFriendlyName

**IRadioInstance：： GetInstanceSignature**： CSampleRadioInstance：： GetInstanceSignature

**IRadioInstance：： GetRadioManagerSignature**： CSampleRadioInstance：： GetRadioManagerSignature

**IRadioInstance：： GetRadioState**： CSampleRadioInstance：： GetRadioState

**IRadioState：： IsAssociatingDevice**： CSampleRadioInstance：： IsAssociatingDevice

**IRadioState：： IsMultiComm**： CSampleRadioInstance：： IsMultiComm

**IRadioState：： SetRadioState**： CSampleRadioInstance：： SetRadioState

**IRadioInstanceCollection：： GetAt**： CRadioInstanceCollection：： GetAt

**IRadioInstanceCollection：： GetCount**： CRadioInstanceCollection：： GetCount

**IMediaRadioManagerNotifySink：： OnInstanceAdd**： CSampleRadioManager：： \_ FireEventOnInstanceAdd

**IMediaRadioManagerNotifySink：： OnInstanceRadioChange**： CSampleRadioManager：： \_ FireEventOnInstanceRadioChange

**IMediaRadioManagerNotifySink：： OnInstanceRemove**： CSampleRadioManager：： \_ FireEventOnInstanceRemove


## <a name="communicating-with-the-device-driver"></a>与设备驱动程序通信

当收音机管理 DLL 收到从无线电管理 API 检索或设置无线电状态的请求时，它会将该请求作为 IOCTL 转发到相应的设备驱动程序。 DLL 通过调用 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数发送 IOCTLs。 与收音机管理关联的特定 IOCTLs 是：

- IOCTL \_ GPS \_ 收音机 \_ 管理 \_ 获取 \_ 无线电 \_ 状态

- IOCTL \_ GPS \_ 收音机 \_ 管理 \_ 获取 \_ 上一 \_ 无线电 \_ 状态

- IOCTL \_ GPS \_ 收音机 \_ 管理 \_ 设置 \_ 无线电 \_ 状态

- IOCTL \_ GPS \_ 收音机 \_ 管理 \_ 设置 \_ 上一 \_ 无线电 \_ 状态

对于示例收音机管理 DLL， **CSensorCommunication：： GetRadioStateHelper** 和 **CSensorCommunication：： SetRadioStateHelper** 方法转发 IOCTLs，以便进行示例地理位置驱动程序。

## <a name="driver-support-for-radio-management"></a>对收音机管理的驱动程序支持

除了广播管理 DLL 外，还需要修改设备驱动程序，以处理从 DLL 发送到驱动程序的四个收音机管理 IOCTLs。 这些 IOCTLs 通知设备驱动程序它应检索当前无线电状态，或打开或关闭设备的无线电。

设备驱动程序最初接收并处理 **CMyQueue：： OnDeviceIoControl** 方法中的任何 IOCTL。 如果此方法标识四个单选管理 IOCTLs 中的一个，则会将该 IOCTL 转发到 **CMyDevice：:P rocessiocontrolradiomanagement** 方法以便进一步处理。 此方法反过来将 IOCTL 转发到 **CSensorManager：:P rocessiocontrolradiomanagement**。 在最后一种方法中，通过调用 **CSensorDDI** 类设置或检索无线电状态。

**CSensorDDI**类包含一个检索无线电状态 (**CSensorDDI：： OnGetRadioState**) 的方法，以及一个 (**CSensorDDI：： OnSetRadioState**) 设置无线电状态的方法。 这是在模拟硬件的示例设备驱动程序中发生最终 IOCTL 处理的地方。 对于实际设备驱动程序， **CSensorDDI：： OnGetRadioState** 方法会从设备固件请求无线电状态，而 **CSensorDDI：： OnSetRadioState** 方法会向固件发出请求以设置状态。

## <a name="debugging-the-radio-management-dll"></a>调试收音机管理 DLL

可以通过完成以下步骤，在 Visual Studio 中调试收音机管理 DLL。

1. 打开 Visual Studio，并在 c + + RadioManagerGPS 文件夹中选择**SampleRM. vcsproj** 。 \\

1. 选择 " **调试"/"附加到进程**"。 在 " **附加到进程** " 对话框中显示的可用进程列表中，选择 "dllhost.exe"。

请注意，如果 dllhost.exe 的多个实例正在运行，则可能需要在排除过程中选择每个实例，以确定与广播管理 DLL 关联的进程。 附加到正确的进程后，可以在 Visual Studio 中设置断点并开始调试。