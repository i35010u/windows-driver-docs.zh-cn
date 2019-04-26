---
title: 支持无线电管理
description: 当用户在其 Windows 8 便携式计算机、 笔记本或平板电脑上的 PC 设置中选择无线选项时，他们可以打开任何连接的无线设备，或关闭。
ms.assetid: AA7AB429-30C5-4C10-AA85-41ED9EAEE69A
keywords:
- 单选管理 API
- 单选管理 API 示例
- 单选管理示例
- GPS 无线电管理
- 单选管理、 GPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6bc428469d1290065e4669cd86eec6d3073dbbf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326179"
---
# <a name="supporting-radio-management"></a>支持无线电管理

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

当用户在其 Windows 8 便携式计算机、 笔记本或平板电脑上的 PC 设置中选择无线选项时，他们可以打开任何连接的无线设备，或关闭。 这些无线设备可能包括 Wi-fi 天线或 GPS 设备。 PC 设置以及给定的无线设备之间的内部链接是[单选管理 API](https://msdn.microsoft.com/library/windows/hardware/hh406615)和相应的单选管理 DLL 对于给定的设备。

单选管理 API 是一组作为 Windows 驱动程序工具包的一部分提供的 COM/Win32 接口。 这些接口包括方法的：

-   检索单选设备的当前状态
-   支持的无线电设备的通知事件
-   检索设备属性 （如的友好名称）

这些接口仅供 Oem 和 Ihv 而不是应用程序开发人员。

## <a name="the-radio-management-dynamic-link-library-dll"></a>单选管理动态链接库 (DLL)


创建用于单选设备，像 GPS 这样的设备驱动程序如果您的驱动程序将需要包含单选管理 API 中支持接口的其他动态链接库 (DLL)。 为了帮助你了解此 DLL 的要求，Microsoft 提供的示例中的地理位置驱动程序示例为 Microsoft Visual Studio 项目和源文件代码。 此示例项目，传感器地理位置驱动程序示例中找到 SampleRM.vcxproj\\C++\\RadioManagerGPS 文件夹的驱动程序示例。 它包括七个存储帐户C++源文件，六个C++标头文件、 模块定义文件、 资源文件、 两个 IDL 文件、 注册表文件 （适用于注册 DLL） 和的安装脚本。

下表列出了单选管理 API 中的方法和示例 DLL 中找到相应的方法。

|                                                     |                                                       |
|-----------------------------------------------------|-------------------------------------------------------|
| 单选管理器 API                                   | 单选管理器 DLL                                     |
| IMediaRadioManager::GetRadioInstances               | CSampleRadioManager::GetRadioInstances                |
| IMediaRadioManager::OnSystemRadioStateChange        | CSampleRadioManager::OnSystemRadioStateChange         |
| IRadioInstance::GetFriendlyName                     | CSampleRadioInstance::GetFriendlyName                 |
| IRadioInstance::GetInstanceSignature                | CSampleRadioInstance::GetInstanceSignature            |
| IRadioInstance::GetRadioManagerSignature            | CSampleRadioInstance::GetRadioManagerSignature        |
| IRadioInstance::GetRadioState                       | CSampleRadioInstance::GetRadioState                   |
| IRadioState::IsAssociatingDevice                    | CSampleRadioInstance::IsAssociatingDevice             |
| IRadioState::IsMultiComm                            | CSampleRadioInstance::IsMultiComm                     |
| IRadioState::SetRadioState                          | CSampleRadioInstance::SetRadioState                   |
| IRadioInstanceCollection::GetAt                     | CRadioInstanceCollection::GetAt                       |
| IRadioInstanceCollection::GetCount                  | CRadioInstanceCollection::GetCount                    |
| IMediaRadioManagerNotifySink::OnInstanceAdd         | CSampleRadioManager::\_FireEventOnInstanceAdd         |
| IMediaRadioManagerNotifySink::OnInstanceRadioChange | CSampleRadioManager::\_FireEventOnInstanceRadioChange |
| IMediaRadioManagerNotifySink::OnInstanceRemove      | CSampleRadioManager::\_FireEventOnInstanceRemove      |

 

## <a name="communicating-with-the-device-driver"></a>与设备驱动程序进行通信


当单选管理 DLL 收到请求以检索或设置从单选管理 API 单选状态时，它将作为相应的设备驱动程序 IOCTL 转发该请求。 DLL 的调用发送 Ioctl [DeviceIoControl]( https://go.microsoft.com/fwlink/p/?linkid=256462)函数。 特定于单选管理与相关联的 Ioctl 是：

-   IOCTL\_GPS\_RADIO\_MANAGEMENT\_GET\_RADIO\_STATE
-   IOCTL\_GPS\_单选\_管理\_获取\_上一步\_单选\_状态
-   IOCTL\_GPS\_RADIO\_MANAGEMENT\_SET\_RADIO\_STATE
-   IOCTL\_GPS\_单选\_管理\_设置\_上一步\_单选\_状态

在示例单选管理的情况下 DLL **CSensorCommuncation::GetRadioStateHelper**并**CSensorCommunication::SetRadioStateHelper**方法转发 Ioctl，示例地理位置驱动程序。

## <a name="driver-support-for-radio-management"></a>驱动程序支持的无线电管理


除了单选管理 DLL，还需要修改你的设备驱动程序来处理四个单选管理 Ioctl 从 DLL 发送到该驱动程序。 这些 Ioctl 通知的设备驱动程序，它应检索当前的广播状态，或者，打开或关闭设备的单选。

设备驱动程序最初接收并处理在任何 IOCTL **CMyQueue::OnDeviceIoControl**方法。 如果此方法标识四个单选管理 Ioctl 之一，它将转发到该 IOCTL **CMyDevice::ProcessIoControlRadioManagement**进行进一步的处理方法。 此方法，反过来，将转发到 IOCTL **CSensorManager::ProcessIoControlRadioManagement**。 在此最后一个方法中，设置或检索到的调用单选状态**CSensorDDI**类。

**CSensorDDI**类包含一个方法来检索单选状态 (**CSensorDDI::OnGetRadioState**) 和设置广播状态的一种方法 (**CSEnsorDDI::OnSetRadioState**). 这是最终 IOCTL 处理的示例设备驱动程序，它可以模拟硬件中出现的位置。 在实际的设备驱动程序的情况下**CSensorDDI::OnGetRadioState**方法会从设备固件请求单选状态并**CSensorDDI::OnSetRadioState**会发出方法请求对固件状态设置。

## <a name="debugging-the-radio-management-dll"></a>调试单选管理 DLL


通过完成以下步骤，可以调试在 Visual Studio 中的单选管理 DLL。

1.  1. 打开 Visual Studio 并选择**SampleRM.vcsproj**中C++ \\RadioManagerGPS 文件夹。
2.  2. 选择**调试/附加到进程**。 在列表中显示的可用进程**附加到进程**对话框中，选择 dllhost.exe。

请注意，是否 dllhost.exe 的多个实例正在运行，您可能需要排除过程中每个选择来确定无线电管理 DLL 与关联的进程。 一旦已附加到正确的进程，可以在 Visual Studio 中设置断点并开始调试。

 

 




