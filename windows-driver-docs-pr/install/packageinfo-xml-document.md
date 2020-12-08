---
title: PackageInfo XML 文档
description: PackageInfo XML 文档
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d32f54d72d1ac5f7942063ba8f93e32ec6b8f1e0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789823"
---
# <a name="packageinfo-xml-document"></a>PackageInfo XML 文档


PackageInfo XML 文档包含的数据用于指定设备元数据包的内容。 操作系统使用此数据来安装包并引用其内容。

设备元数据系统的组件，例如 [Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md) (WMIS) 和 [设备元数据检索客户端](device-metadata-retrieval-client.md) (DMRC) 使用 PackageInfo XML 文档为设备和打印机用户界面提供设备的当前和最合适的信息，如下所示：

-   设备的硬件或型号 ID。 此信息由 PackageInfo XML 文档中的 [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85)) 和 [**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85)) XML 元素指定。

-   与计算机的区域设置匹配的设备元数据包的本地化版本。 此信息由 PackageInfo XML 文档中的 [**Locale**](/previous-versions/windows/hardware/metadata/ff548647(v=vs.85)) xml 元素指定。

-   与计算机的区域设置匹配的设备元数据包的最后修改的数据。 此信息由 PackageInfo XML 文档中的 [**LastModifiedDate**](/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) XML 元素指定。

每个设备元数据包必须只包含一个 PackageInfo XML 文档。 文档的名称必须 *PackageInfo.xml*。

PackageInfo XML 文档中的数据基于 [PACKAGEINFO xml 架构](/previous-versions/windows/hardware/metadata/ff549614(v=vs.85))进行格式设置。

 

