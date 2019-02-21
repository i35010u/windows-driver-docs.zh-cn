---
title: 设备元数据检索客户端
description: 设备元数据检索客户端
ms.assetid: fdcf3459-0fd4-4cf6-a9f5-13337fbd604b
keywords:
- DMRC 如何 WDK
- 设备元数据检索客户端 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f3ac1d6c5635e2553a62ef2b14c1fe58e2e5e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542290"
---
# <a name="device-metadata-retrieval-client"></a>设备元数据检索客户端


设备元数据检索客户端 (DMRC) 是与设备元数据包的设备相匹配的操作系统组件。 当用户打开设备的库视图窗口，打印机用户界面，dmrc 如何尝试获取设备和打印机将显示的设备的设备元数据。 首先，它会检查本地计算机[设备元数据缓存](device-metadata-cache.md)并[设备元数据存储区](device-metadata-store.md)。 如果新安装该设备，或者设备已计划定期的元数据更新，dmrc 如何查询[Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md)(WMIS) 网站，以确定是否可用于设备元数据包设备。 如果可用的设备元数据包，dmrc 如何自动从 WMIS 下载包、 提取包的设备元数据组件，并将它们保存在设备元数据缓存。

[PackageInfo XML 文档](packageinfo-xml-document.md)(Packageinfo.xml) 的设备元数据包，组件包含 dmrc 如何需匹配的设备包的信息。 该文件包含[ **MetadataKey** ](https://msdn.microsoft.com/library/windows/hardware/ff548740)指定来自以下源之一的设备匹配信息的 XML 元素：

-   标识设备支持的硬件函数一个或多个硬件 Id 的列表。 中指定的硬件 Id 列表[ **HardwareIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff546121)子 XML 元素。

-   标识设备支持的硬件函数的一个或多个模型 Id 列表。 每个模型 ID 是全局唯一标识符 (GUID)，并在指定的模型 Id 的列表[ **ModelIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff549303)子 XML 元素。

有关被引用的 XML 架构的详细信息[PackageInfo XML 文档](packageinfo-xml-document.md)，请参阅[PackageInfo XML 架构](https://msdn.microsoft.com/library/windows/hardware/ff549614)。

 

 





