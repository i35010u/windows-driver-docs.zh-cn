---
title: PackageInfo XML 文档
description: PackageInfo XML 文档
ms.assetid: 1fa9b8a5-d6ab-4952-8e2d-7cb7ccc88804
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 116aaffd2285ba77ea63681326967f5aefdac94e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365825"
---
# <a name="packageinfo-xml-document"></a>PackageInfo XML 文档


PackageInfo XML 文档包含指定的设备元数据包内容的数据。 操作系统使用此数据来安装包并引用其内容。

组件的设备元数据系统，如[Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md)(WMIS) 和[设备元数据检索客户端](device-metadata-retrieval-client.md)(DMRC) 使用要提供的 PackageInfo XML 文档设备和打印机用户界面的当前和最合适的信息，对于设备，如下所示：

-   设备的硬件或模型 ID。 此信息由指定[ **HardwareID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))并[ **ModelID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85)) PackageInfo XML 文档中的 XML 元素。

-   与计算机的区域设置匹配的设备元数据包的本地化的版本。 此信息由指定[**区域设置**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548647(v=vs.85)) PackageInfo XML 文档内的 XML 元素。

-   上次修改数据的匹配计算机的区域设置的设备元数据包。 此信息由指定[ **LastModifiedDate** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) PackageInfo XML 文档内的 XML 元素。

每个设备元数据包必须包含一个 PackageInfo XML 文档。 文档的名称必须是*PackageInfo.xml*。

PackageInfo XML 文档中的数据的格式根据[PackageInfo XML 架构](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549614(v=vs.85))。

 

 





