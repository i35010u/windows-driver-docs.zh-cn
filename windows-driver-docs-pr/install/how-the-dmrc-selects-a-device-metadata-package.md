---
title: DMRC 如何选择设备元数据包
description: DMRC 如何选择设备元数据包
ms.assetid: dbedc995-520a-4b54-8613-d5a7810ab99c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1209b160d327724d9313355086552dd90cce21b2
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095269"
---
# <a name="how-the-dmrc-selects-a-device-metadata-package"></a>DMRC 如何选择设备元数据包


当打开 "设备和打印机" 或 "设备阶段" 用户界面时，操作系统将启动 "设备元数据检索客户端 ([DMRC](device-metadata-retrieval-client.md) ") ，在其缓存中搜索设备最合适和最新的元包。 DMRC 还会在 Windows 元数据和 Internet 服务 ([WMIS](windows-metadata-and-internet-services.md)) 服务器上搜索设备的更新的元数据包。 如果找到一个，DMRC 将下载包并将其安装在计算机上。

**注意**   如果 DMRC 最近下载了某个设备的元数据包，则它将为该设备使用缓存的元数据包，而不是在 WMIS 服务器中搜索更高版本的包。 有关详细信息，请参阅 [DMRC 如何确定何时搜索 WMIS 服务器](how-the-dmrc-determines-when-to-search-the-wmis-server.md)。

 

DMRC 使用在包中指定的以下元数据 XML 元素为设备选择适当的包。 这些 XML 元素的顺序反映了 DMRC 用于选择元数据包的优先级：

-   [**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))和[ **ModelIDList**](/previous-versions/windows/hardware/metadata/ff549303(v=vs.85))

-   [**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))和[ **HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))

-   [**本地**](/previous-versions/windows/hardware/metadata/ff548647(v=vs.85))

-   [**LastModifiedDate**](/previous-versions/windows/hardware/metadata/ff548624(v=vs.85))

[DMRC](device-metadata-retrieval-client.md)在为设备选择元数据包时遵循以下步骤：

1.  如果设备具有模型 ID，则 DMRC 会在设备元数据包的[**ModelIDList**](/previous-versions/windows/hardware/metadata/ff549303(v=vs.85)) XML 元素和设备[**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))的模型 ID 值之间搜索设备元数据包，使之匹配。

2.  如果设备没有模型 ID，则 DMRC 会在设备元数据包中搜索包的[**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85)) XML 元素中[**HardwareID**](/previous-versions/windows/hardware/metadata/ff546114(v=vs.85))项与设备的硬件 id 之间的匹配项。

3.  DMRC 创建一个设备元数据包列表，该列表满足步骤1和步骤2中所述的搜索条件。 在此列表中，DMRC 随后会搜索列表条目，以查找包的 [**区域设置**](/previous-versions/windows/hardware/metadata/ff548647(v=vs.85)) XML 元素与计算机上首选用户区域设置列表之间的匹配项。

    如果列表中没有条目与此搜索条件相匹配，则 DMRC 将在列表中搜索条目中的条目，其中包含一个设置为**true****的 Locale** XML 元素。 如果 DMRC 找到匹配项，则会选择该元数据包。

4.  如果 DMRC 在步骤3中找到了多个设备元数据包，则会选择具有最新时间戳的 [**LastModifiedDate**](/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) XML 元素的包。

以下点与 [DMRC](device-metadata-retrieval-client.md)使用的选择算法相关：

-   如果 DMRC 选择基于硬件 Id 的元数据包，则它将使用在驱动程序安装过程中操作系统所用的相同级别的硬件 Id。 DMRC 排名比不太具体的硬件 Id 更多的特定硬件 Id。 例如，下列硬件 Id 按排名顺序列出：

    ```cpp
    <HardwareID>DOID:USB\VID_XXXX&PID_YYYY&REV_0000</HardwareID>
    <HardwareID>DOID:USB\VID_XXXX&PID_YYYY</HardwareID>
    ```

    有关硬件 Id 的信息，请参阅 [硬件 id](hardware-ids.md)。

-   对于一个设备，只应将[**Locale**](/previous-versions/windows/hardware/metadata/ff548647(v=vs.85)) XML 元素的**默认**属性设置为**true**。 只应在包含排名值最高的硬件 ID 的包中将此特性设置为 true。

-   [**LastModifiedDate**](/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) XML 元素用于版本控制，用于为设备选择较新版本的设备元数据包。

-   如果本地元数据存储中的两个或多个设备元数据包包含相同的 [**ModelIDList**](/previous-versions/windows/hardware/metadata/ff549303(v=vs.85))、 [**HardwareIDList**](/previous-versions/windows/hardware/metadata/ff546121(v=vs.85))、 [**Locale**](/previous-versions/windows/hardware/metadata/ff548647(v=vs.85))或 [**LASTMODIFIEDDATE**](/previous-versions/windows/hardware/metadata/ff548624(v=vs.85)) XML 元素的值，则 DMRC 只为设备选择其中的一个。 在这种情况下，DMRC 将以不确定的方式选择其中一个包。

有关设备元数据 XML 架构和元素的详细信息，请参阅 [设备元数据架构参考](/previous-versions/windows/hardware/metadata/ff541452(v=vs.85))。

 

