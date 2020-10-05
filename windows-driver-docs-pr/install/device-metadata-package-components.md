---
title: 设备元数据包结构
description: 设备元数据包结构
ms.assetid: 37614100-0a56-4a32-8e45-3161994e503a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66573ed1808e9331f84cd3aec85ff1f41e772b8b
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732873"
---
# <a name="device-metadata-package-structure"></a>设备元数据包结构


每个设备元数据包都具有以下目录结构：

PackageInfo.xml

DeviceInformation DeviceInfo.xml *DeviceIcon*

WindowsInformation WindowsInfo.xml

DeviceStage 创建设备元数据包时，XML 文档和图标文件存储在以下目录中：

-   [PACKAGEINFO XML 文档](packageinfo-xml-document.md)位于目录的根目录。 此 XML 文档的名称必须 PackageInfo.xml。

-   DeviceInformation 子目录包含 [DEVICEINFO XML 文档](deviceinfo-xml-document.md) 和可选的设备图标文件。 XML 文档的名称必须 DeviceInfo.xml。

    如果设备元数据包包含设备图标文件，则它可以具有任何名称，但必须以 *.ico*后缀结尾。 有关详细信息，请参阅 [设备图标文件](device-icon-file.md)。

-   WindowsInformation 子目录包含 [WINDOWSINFO XML 文档](windowsinfo-xml-document.md)。 XML 文档的名称必须 WindowsInfo.xml。

-   DeviceStage 子目录包含 Windows 设备阶段用于显示设备阶段体验的特定文件。 设备阶段是用于开发和分发特定于设备的体验的丰富平台。 使用设备阶段，设备制造商可以通过仅定义少量的 XML 文件和图形来创建与设备的品牌、功能和服务相匹配的体验。

    如果设备制造商使用设备的设备阶段体验，则 Windows 要求 DeviceStage 目录位于设备元数据包中。 否则，Windows 将忽略包中的目录。

    **注意**  设备阶段支持的设备类数量有限。




有关 Windows 设备体验、设备阶段和设备阶段 XML 架构的详细信息，请参阅 [Microsoft 设备体验开发工具包](../download-the-wdk.md)。


创建设备元数据包时，应遵循以下准则：

-   必须使用 UTF-8 编码保存每个 XML 文档。

-   设备元数据包不需要包含设备图标。 但是，我们强烈建议设备元数据包包含 [设备图标文件](device-icon-file.md)。 这用于在设备和打印机中显示设备的照片真实图像。

从 Windows 7 版本的 Windows 驱动程序工具包开始 (WDK) ， [Toaster 示例](/samples/browse/) 提供了一个设备元数据包示例。 此包的 XML 文档位于 WDK 的 *src \\ general \\ toaster \\ devicemetadatapackage* 子目录中。