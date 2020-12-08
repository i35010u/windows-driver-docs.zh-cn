---
title: 构建设备元数据包
description: 构建设备元数据包
keywords:
- 设备元数据包 WDK，生成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d219aa5a078bd255899ddc238882a0c4a507c948
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814425"
---
# <a name="building-device-metadata-packages"></a>构建设备元数据包


本主题提供有关如何生成设备元数据包的准则。

### <a name="device-metadata-package-file-names"></a><a href="" id="device-metadata-package-file-names"></a> 设备元数据包文件名

创建设备元数据包文件之前，必须先为元数据包创建 (GUID) 全局唯一标识符。 为此，请使用 [GUID 生成](/previous-versions/aa475087(v=msdn.10))网站中所述 *( # B0*) 的 guidgen.exe 工具。

设备元数据包的文件名必须使用以下命名约定：

```cpp
<GUID>.devicemetadata-ms
```

例如，如果你创建的 GUID 的值为 {20f001a99-4675-8707-248ca-187dfd9}，则使用该 GUID 创建以下设备元数据包文件：

```cpp
20f001a99-4675-8707-248ca-187dfd9.devicemetadata-ms
```

**注意**  仅当设备元数据包具有后缀时，操作系统才会将其识别。*devicemetadata-ms*。

 

以下规则适用于设备元数据包文件：

-   每个元数据包文件名的 GUID 都必须是唯一的。 当你创建新的或已修改的元数据包时，你必须创建新的 GUID，即使更改很小。

-   每个元数据包只能支持一个区域设置。 如果你的设备支持多个区域设置，则必须为每个区域设置创建单独的元数据包，其中每个元包都具有自己的 GUID。 有关详细信息，请参阅 [**LOCALE XML 元素**](/previous-versions/windows/hardware/metadata/ff548647(v=vs.85))。

    **注意**  如果你的设备需要多个特定于区域设置的设备元数据包文件，则可以通过创建非特定语言标识符来对所有文件进行分组。 此标识符是一个 GUID，可以在同一设备的所有元数据包内的 [**LanguageNeutralIdentifier**](/previous-versions/windows/hardware/metadata/ff548617(v=vs.85)) XML 元素中指定相同的 guid。

     

-   设备元数据包文件名的 *&lt; guid &gt;* 前缀必须指定不带 "{" 或 "}" 分隔符的 guid。

### <a name="creating-a-device-metadata-package-file"></a>创建设备元数据包文件

[设备元数据包的组件](device-metadata-package-components.md)存储在使用 Cabarc (*Cabarc.exe*) 工具压缩的文件中。 有关此工具的详细信息，请参阅 [Cabarc 概述](/previous-versions/windows/it-pro/windows-server-2003/cc781787(v=ws.10)) 网站。

下面的代码示例演示如何使用 Cabarc 工具创建设备元数据包文件。 在此示例中，元数据包的组件位于名为 *MyMetadataPackage* 的本地目录中。 以下列表显示了 *MyMetadataPackage* 目录中的子目录和文件：

```cpp
.\MyMetadataPackages
.\MyMetadataPackage\PackageInfo.xml
.\MyMetadataPackage\DeviceInformation\DeviceInfo.xml
.\MyMetadataPackage\DeviceInformation\MyIcon.ico
.\MyMetadataPackage\WindowsInformation\WindowsInfo.xml
```

首先，为设备元数据包创建值为 {f4ea2b40-77ff-443d-8212-be7e74a344ae} 的 GUID。 下图显示了如何使用 Guidgen.exe 工具创建 GUID：

![guidgen.exe "创建 guid" 对话框的屏幕截图](images/dmrc.png)

然后，下面的命令使用 Cabarc 工具在名为 *MyDeviceMetadataPackage* 的本地目录中创建新的设备元数据包文件：

```cpp
Cabarc.exe -r -p -P .\MyMetadataPackage\ 
    N .\MyDeviceMetadataPackage\f4ea2b40-77ff-443d-8212-be7e74a344ae.devicemetadata-ms 
    .\MyMetadataPackage\PackageInfo.xml 
    .\MyMetadataPackage\DeviceInformation\DeviceInfo.xml 
    .\MyMetadataPackage\DeviceInformation\MyIcon.ico 
    .\MyMetadataPackage\WindowsInformation\WindowsInfo.xml
```

**注意**  每个元数据包只能支持一个区域设置。 如果你的设备支持多个区域设置，则必须为每个区域设置创建单独的元数据包，其中每个元包都具有自己的 GUID。

 

