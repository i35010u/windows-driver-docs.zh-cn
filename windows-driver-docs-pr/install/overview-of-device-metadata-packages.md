---
title: 设备元数据包概述
description: 设备元数据包概述
ms.assetid: 1b17bdab-44e4-498b-ab80-f28fa94d9821
keywords:
- 设备元数据包 WDK，关于
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ebfd24096445b74471017b5d20d256846eaee7a
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095997"
---
# <a name="overview-of-device-metadata-packages"></a>设备元数据包概述

从 Windows 7 开始，设备元数据包包含表示设备属性及其硬件功能的 XML 文档。 "设备和打印机" 用户界面基于设备的元数据包中的 XML 文档向用户显示特定于设备的信息。

设备元数据包由多个 XML 文档组成，每个文档指定设备属性的各种组件。

从 Windows 7 开始，设备、设备和打印机的新用户界面将显示通常在一个窗口中连接到计算机的大多数设备。 此窗口称为库视图。 对于库视图中显示的每个设备，"设备和打印机" 会根据设备的元数据包中的 XML 文档向用户显示特定于设备的信息。 通过使用这些 XML 文档，OEM 可以自定义要包含的信息以及此信息的显示方式。 例如，库视图中的设备可由 OEM 提供的自定义图标和描述性文本表示。

设备元数据包中包含的 XML 文档指定描述该物理设备的信息。 以下列表显示 XML 文档可以指定的信息类型：

-   OEM 的名称。

-   设备的模型名称和说明。

-   设备支持的一个或多个功能类别。

每个设备元数据包都包含以下组件：

<a href="" id="packageinfo-xml-document"></a>[PackageInfo XML 文档](packageinfo-xml-document.md)  
此文档包含的数据用于指定设备元数据包的内容。 操作系统使用此数据来安装包并引用其内容。

此数据的格式基于 [PACKAGEINFO XML 架构](/previous-versions/windows/hardware/metadata/ff549614(v=vs.85))。

<a href="" id="deviceinfo-xml-document"></a>[DeviceInfo XML 文档](deviceinfo-xml-document.md)  
此文档包含指定设备的属性的数据，例如设备类别和型号名称。 "设备和打印机" 用户界面使用此数据显示有关设备的详细信息。

此数据的格式基于 [DEVICEINFO XML 架构](/previous-versions/windows/hardware/metadata/ff541135(v=vs.85))。

<a href="" id="device-icon-file"></a>[设备图标文件](device-icon-file.md)  
此文件包含在 "设备和打印机" 用户界面中表示设备的照片真实映像。

<a href="" id="windowsinfo-xml-document"></a>[WindowsInfo XML 文档](windowsinfo-xml-document.md)  
此文档包含指定设备和打印机用户界面为设备元数据包中的指定设备执行的显示操作的数据。

此数据的格式基于 [WINDOWSINFO XML 架构](/previous-versions/windows/hardware/metadata/ff553992(v=vs.85))。

每个设备元数据包都通过使用 Cabarc (*Cabarc.exe*) "工具，将其组件压缩到一个文件中。 有关此工具的详细信息，请参阅 [Cabarc 概述](https://go.microsoft.com/fwlink/p/?linkid=145395) 网站。

设备元数据包的文件名使用以下命名约定：

```cpp
<GUID>.devicemetadata-ms
```

* &lt; Guid &gt; *文件前缀是为设备元数据包创建 (guid) 的全局唯一标识符。 每个元数据包文件名的 GUID 都必须是唯一的。 当你创建新的或已修改的元数据包时，你必须创建新的 GUID，即使更改很小。

有关详细信息，请参阅 [构建设备元数据包](building-device-metadata-packages.md)。

 

