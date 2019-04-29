---
title: 设备元数据包结构
description: 设备元数据包结构
ms.assetid: 37614100-0a56-4a32-8e45-3161994e503a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3932c57925a4bd544bb20e6ef24f475e122dc5a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357787"
---
# <a name="device-metadata-package-structure"></a>设备元数据包结构


每个设备元数据包都具有以下目录结构：

PackageInfo.xml

DeviceInformation DeviceInfo.xml *DeviceIcon*.ico

WindowsInformation WindowsInfo.xml

创建设备元数据包 DeviceStage 时，XML 文档和图标文件存储在以下目录：

-   [PackageInfo XML 文档](packageinfo-xml-document.md)位于目录的根目录。 此 XML 文档的名称必须是 PackageInfo.xml。

-   DeviceInformation 子目录中都包含[DeviceInfo XML 文档](deviceinfo-xml-document.md)和可选的设备图标文件。 XML 文档的名称必须是 DeviceInfo.xml。

    如果你的设备元数据包包含设备图标文件，它可以具有任何名称，但必须以的后缀结尾 *.ico*。 有关详细信息，请参阅[设备图标文件](device-icon-file.md)。

-   WindowsInformation 子目录中都包含[WindowsInfo XML 文档](windowsinfo-xml-document.md)。 XML 文档的名称必须是 WindowsInfo.xml。

-   DeviceStage 子目录包含 Windows Device Stage 用于呈现 Device Stage 体验的特定文件。 设备阶段是用于开发和分发特定于设备的经验丰富的平台。 使用 Device Stage 设备制造者可以创建匹配该品牌，功能和其设备的服务通过定义仅几个 XML 文件和图形的体验。

    如果为该设备，设备制造者使用 Device Stage 体验，Windows 将要求 DeviceStage 目录中，设备元数据包。 否则，Windows 将在包中是否忽略目录。

    **请注意**Device Stage 支持有限数量的设备类。




有关 Windows 设备体验、 Device Stage 和设备阶段 XML 架构的详细信息可在[Microsoft 设备体验开发工具包](https://go.microsoft.com/fwlink/p/?linkid=192621)。


创建设备元数据包时，应遵循以下准则：

-   必须通过使用 utf-8 编码保存每个 XML 文档。

-   设备元数据包不需要包括设备图标。 但是，我们强烈建议，包含设备元数据包[设备图标文件](device-icon-file.md)。 这用于设备真实感图像显示在设备和打印机。

从 Windows 7 版本的 Windows Driver Kit (WDK) 中，开始[Toaster 示例](https://go.microsoft.com/fwlink/p/?linkid=256195)提供了示例设备元数据包。 此包的 XML 文档都位于*src\\常规\\toaster\\devicemetadatapackage* WDK 的子目录。









