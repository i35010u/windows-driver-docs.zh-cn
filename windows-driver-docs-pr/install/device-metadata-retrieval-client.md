---
title: 设备元数据检索客户端
description: 设备元数据检索客户端
ms.assetid: fdcf3459-0fd4-4cf6-a9f5-13337fbd604b
keywords:
- DMRC WDK
- 设备元数据检索客户端 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a474379a07eae448c6365b7b0cd114a980d70533
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096507"
---
# <a name="device-metadata-retrieval-client"></a>设备元数据检索客户端


设备元数据检索客户端 (DMRC) 是与设备元数据包匹配的操作系统组件。 当用户打开 "设备和打印机" 用户界面的 "库视图" 窗口时，DMRC 将尝试获取设备和打印机将显示的设备的设备元数据。 首先，它检查本地计算机的 [设备元数据缓存](device-metadata-cache.md) 和 [设备元数据存储](device-metadata-store.md)。 如果设备是新安装的，或者如果为定期元数据更新计划了设备，DMRC 将查询 [Windows 元数据和 Internet 服务](windows-metadata-and-internet-services.md) (WMIS) 网站，以确定设备元数据包是否可用于设备。 如果设备元数据包可用，DMRC 会自动从 WMIS 下载包，提取包的设备元数据组件，并将它们保存在设备元数据缓存中。

[PACKAGEINFO XML 文档](packageinfo-xml-document.md) ( # A0) ，它是设备元数据包的组件，包含 DMRC 将设备与包匹配所需的信息。 此文件包含一个 [**MetadataKey**](/previous-versions/windows/hardware/metadata/ff548740(v=vs.85)) XML 元素，该元素指定设备匹配信息，该信息来自以下源之一：

-   标识设备支持的硬件功能的一个或多个硬件 Id 列表。 硬件 Id 列表是在 [**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85)) 子 XML 元素中指定的。

-   标识设备支持的硬件功能的一个或多个模型 Id 的列表。 每个模型 ID 都是 (GUID) 的全局唯一标识符，并且模型 Id 列表是在 [**ModelIDList**](/previous-versions/windows/hardware/metadata/ff549303(v=vs.85)) 子 XML 元素中指定的。

有关 [PACKAGEINFO xml 文档](packageinfo-xml-document.md)引用的 xml 架构的详细信息，请参阅 [PackageInfo xml 架构](/previous-versions/windows/hardware/metadata/ff549614(v=vs.85))。

 

