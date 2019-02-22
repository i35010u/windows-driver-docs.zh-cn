---
title: 构建设备元数据包
description: 构建设备元数据包
ms.assetid: 8b95a88e-430c-4250-959f-43536fdc1824
keywords:
- 设备元数据包 WDK 构建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb342da01dca7cfe5a1fcb6e2a5eb2e5da73ee8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554813"
---
# <a name="building-device-metadata-packages"></a>构建设备元数据包


本主题提供有关如何构建设备元数据包的指南。

### <a href="" id="device-metadata-package-file-names"></a> 设备元数据的包文件名称

在创建设备元数据的包文件之前，必须首先创建元数据包的全局唯一标识符 (GUID)。 若要执行此操作，使用 Guidgen 工具 *(Guidgen.exe*) 中介绍[生成 GUID](https://go.microsoft.com/fwlink/p/?linkid=145426)网站。

设备元数据包的文件名必须使用以下命名约定：

```cpp
<GUID>.devicemetadata-ms
```

例如，如果您创建的值为 {20f001a99-4675-8707-248ca-187dfd9} 的 GUID，你使用该 GUID 来创建以下设备元数据的包文件：

```cpp
20f001a99-4675-8707-248ca-187dfd9.devicemetadata-ms
```

**请注意**  操作系统识别出设备元数据包，仅当具有后缀。*devicemetadata ms*。

 

以下规则适用于设备元数据的包文件：

-   对于每个元数据包文件的名称 GUID 必须是唯一的。 创建新的或修改元数据包时，必须创建新的 GUID，即使所做的更改是很微小的。

-   元数据的每个包可以支持只有一个区域设置。 如果你的设备支持多个区域设置，则必须创建单独元数据包的每个区域设置，每个元数据文件，包具有其自己的 GUID。 有关详细信息，请参阅[**区域设置 XML 元素**](https://msdn.microsoft.com/library/windows/hardware/ff548647)。

    **请注意**  如果为你的设备需要多个特定于区域设置的设备元数据的包文件，则可以通过创建一个非特定语言标识符分组的所有文件。 此标识符是 GUID，并可以在中指定相同的 GUID [ **LanguageNeutralIdentifier** ](https://msdn.microsoft.com/library/windows/hardware/ff548617)对于同一设备的所有元数据包内的 XML 元素。

     

-   *&lt;GUID&gt;* 设备元数据包文件名称的前缀必须指定而无需 GUID {或} 的分隔符。

### <a name="creating-a-device-metadata-package-file"></a>创建设备元数据包文件

[的设备元数据包组件](device-metadata-package-components.md)存储在使用 Cabarc 压缩来压缩文件 (*Cabarc.exe*) 工具。 有关此工具的详细信息，请参阅[Cabarc 概述](https://go.microsoft.com/fwlink/p/?linkid=145395)网站。

下面的代码示例演示如何使用 Cabarc 工具来创建设备元数据包文件。 在此示例中，元数据包的组件位于名为的本地目录中*MyMetadataPackage*。 以下列表显示了子目录和文件内*MyMetadataPackage*目录：

```cpp
.\MyMetadataPackages
.\MyMetadataPackage\PackageInfo.xml
.\MyMetadataPackage\DeviceInformation\DeviceInfo.xml
.\MyMetadataPackage\DeviceInformation\MyIcon.ico
.\MyMetadataPackage\WindowsInformation\WindowsInfo.xml
```

首先，为设备元数据包创建的 GUID 值为 {f4ea2b40-77ff-443d-8212-be7e74a344ae}。 下图显示了如何使用 Guidgen 工具创建的 GUID:

![屏幕截图： guidgen 创建 guid 对话框的](images/dmrc.png)

然后，以下命令使用 Cabarc 工具在一个名为的本地目录中创建新的设备元数据包文件*MyDeviceMetadataPackage*:

```cpp
Cabarc.exe -r -p -P .\MyMetadataPackage\ 
    N .\MyDeviceMetadataPackage\f4ea2b40-77ff-443d-8212-be7e74a344ae.devicemetadata-ms 
    .\MyMetadataPackage\PackageInfo.xml 
    .\MyMetadataPackage\DeviceInformation\DeviceInfo.xml 
    .\MyMetadataPackage\DeviceInformation\MyIcon.ico 
    .\MyMetadataPackage\WindowsInformation\WindowsInfo.xml
```

**请注意**  元数据的每个包可以支持只有一个区域设置。 如果你的设备支持多个区域设置，则必须创建单独元数据包的每个区域设置，每个元数据文件，包具有其自己的 GUID。

 

 

 





