---
title: PackageInfo XML 文档
description: PackageInfo XML 文档
ms.assetid: 1fa9b8a5-d6ab-4952-8e2d-7cb7ccc88804
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 620c477a6a5d49d049b72367bad796766d178385
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348988"
---
# <a name="packageinfo-xml-document"></a>PackageInfo XML 文档


PackageInfo XML 文档包含指定的设备元数据包内容的数据。 操作系统使用此数据来安装包并引用其内容。

组件的设备元数据系统，如[Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md)(WMIS) 和[设备元数据检索客户端](device-metadata-retrieval-client.md)(DMRC) 使用要提供的 PackageInfo XML 文档设备和打印机用户界面的当前和最合适的信息，对于设备，如下所示：

-   设备的硬件或模型 ID。 此信息由指定[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)并[ **ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295) PackageInfo XML 文档中的 XML 元素。

-   与计算机的区域设置匹配的设备元数据包的本地化的版本。 此信息由指定[**区域设置**](https://msdn.microsoft.com/library/windows/hardware/ff548647) PackageInfo XML 文档内的 XML 元素。

-   上次修改数据的匹配计算机的区域设置的设备元数据包。 此信息由指定[ **LastModifiedDate** ](https://msdn.microsoft.com/library/windows/hardware/ff548624) PackageInfo XML 文档内的 XML 元素。

每个设备元数据包必须包含一个 PackageInfo XML 文档。 文档的名称必须是*PackageInfo.xml*。

PackageInfo XML 文档中的数据的格式根据[PackageInfo XML 架构](https://msdn.microsoft.com/library/windows/hardware/ff549614)。

 

 





