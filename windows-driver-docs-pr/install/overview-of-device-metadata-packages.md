---
title: 设备元数据包概述
description: 设备元数据包概述
ms.assetid: 1b17bdab-44e4-498b-ab80-f28fa94d9821
keywords:
- 设备元数据打包有关 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c257eb5f37e7a73fa5c12fe7db5099f61801e9b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379441"
---
# <a name="overview-of-device-metadata-packages"></a>设备元数据包概述

从 Windows 7 开始，设备元数据包包含表示设备和其硬件功能的属性的 XML 文档。 设备和打印机用户界面为用户基于设备的元数据的包中的 XML 文档上显示特定于设备的信息。

多个 XML 文档，包括设备元数据包和每个文档指定设备的属性的各种组件。

从 Windows 7，对于设备，新的用户界面开始设备和打印机，显示大部分通常连接到一个窗口中的计算机的设备。 此窗口称为库视图。 显示在库视图中的每台设备，设备和打印机特定于设备的信息为用户显示基于设备的元数据的包中的 XML 文档。 通过使用这些 XML 文档，OEM 可以自定义将包括哪些信息和此信息的显示方式。 例如，可以由自定义图标和 OEM 提供的描述性文本表示库视图中的设备。

设备元数据包中包含的 XML 文档指定描述物理设备的信息。 以下列表显示 XML 文档可以指定的信息的类型：

-   OEM 的名称。

-   模型名称和设备的说明。

-   一个或多个功能类别的设备支持。

每个设备元数据包包含下列组件：

<a href="" id="packageinfo-xml-document"></a>[PackageInfo XML 文档](packageinfo-xml-document.md)  
本文档包含指定的设备元数据包内容的数据。 操作系统使用此数据来安装包并引用其内容。

此数据的格式根据[PackageInfo XML 架构](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549614(v=vs.85))。

<a href="" id="deviceinfo-xml-document"></a>[DeviceInfo XML 文档](deviceinfo-xml-document.md)  
本文档包含指定设备的属性，例如设备类别和型号名称的数据。 设备和打印机用户界面使用此数据以显示有关设备的详细的信息。

此数据的格式根据[DeviceInfo XML 架构](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541135(v=vs.85))。

<a href="" id="device-icon-file"></a>[设备图标文件](device-icon-file.md)  
此文件包含真实感图像，表示设备和打印机用户界面中的设备。

<a href="" id="windowsinfo-xml-document"></a>[WindowsInfo XML 文档](windowsinfo-xml-document.md)  
本文档包含指定的设备和打印机用户界面执行设备元数据包中的指定设备的显示操作的数据。

此数据的格式根据[WindowsInfo XML 架构](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff553992(v=vs.85))。

每个设备元数据包已使用 Cabarc 压缩到一个文件及其组件 (*Cabarc.exe*) 工具。 有关此工具的详细信息，请参阅[Cabarc 概述](https://go.microsoft.com/fwlink/p/?linkid=145395)网站。

设备元数据包的文件名使用以下命名约定：

```cpp
<GUID>.devicemetadata-ms
```

*&lt;GUID&gt;* 文件前缀是为设备元数据包创建的全局唯一标识符 (GUID)。 对于每个元数据包文件的名称 GUID 必须是唯一的。 创建新的或修改元数据包时，必须创建新的 GUID，即使所做的更改是很微小的。

有关详细信息，请参阅[构建设备元数据包](building-device-metadata-packages.md)。

 

 





