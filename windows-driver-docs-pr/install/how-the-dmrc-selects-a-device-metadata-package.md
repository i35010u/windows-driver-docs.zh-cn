---
title: DMRC 如何选择设备元数据包
description: DMRC 如何选择设备元数据包
ms.assetid: dbedc995-520a-4b54-8613-d5a7810ab99c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48545d2f50c2cf8f11ca0fd2ea601707f28b5b9f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386969"
---
# <a name="how-the-dmrc-selects-a-device-metadata-package"></a>DMRC 如何选择设备元数据包


当设备和打印机或设备阶段用户界面将被打开，在操作系统启动设备元数据检索客户端 ([dmrc 如何](device-metadata-retrieval-client.md)) 若要搜索其缓存，以最适当的和当前元数据包的设备。 Dmrc 如何还会搜索 Windows 元数据和 Internet 服务上的设备的较新的元数据包 ([WMIS](windows-metadata-and-internet-services.md)) 服务器。 如果找到，dmrc 如何下载包并将其安装在计算机上。

**请注意**  如果 dmrc 如何最近下载设备元数据包，它使用缓存的元数据的包有关的设备而不是搜索 WMIS 服务器的较新的包。 有关详细信息，请参阅[dmrc 如何如何确定何时搜索 WMIS 服务器](how-the-dmrc-determines-when-to-search-the-wmis-server.md)。

 

Dmrc 如何使用包中指定的以下元数据 XML 元素来选择适当的包内的设备。 这些 XML 元素的顺序反映了 dmrc 如何用于选择元数据包的优先级：

-   [**ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295)并[ **ModelIDList**](https://msdn.microsoft.com/library/windows/hardware/ff549303)

-   [**HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)并[ **HardwareIDList**](https://msdn.microsoft.com/library/windows/hardware/ff546121)

-   [**Locale**](https://msdn.microsoft.com/library/windows/hardware/ff548647)

-   [**LastModifiedDate**](https://msdn.microsoft.com/library/windows/hardware/ff548624)

[Dmrc 如何](device-metadata-retrieval-client.md)它选择的设备元数据包时应遵循以下步骤：

1.  如果设备有一个模型 ID，dmrc 如何将搜索设备元数据包之间的匹配[ **ModelID** ](https://msdn.microsoft.com/library/windows/hardware/ff549295)在包中的条目[ **ModelIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff549303)XML 元素和设备的模型 ID 值。

2.  如果设备没有模型 ID，dmrc 如何将搜索设备元数据包之间的匹配[ **HardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff546114)包中的条目[ **HardwareIDList**](https://msdn.microsoft.com/library/windows/hardware/ff546121) XML 元素和设备的硬件 Id。

3.  Dmrc 如何创建设备的列表符合搜索条件在步骤 1 和 2 中所述的元数据包。 从此列表中，dmrc 如何则搜索的列表项的包之间的匹配[**区域设置**](https://msdn.microsoft.com/library/windows/hardware/ff548647) XML 元素和列表的首选的计算机上的用户区域设置。

    Dmrc 如何如果列表中的没有项匹配此搜索条件，设备元数据包，其中包含具有的区域设置 XML 元素的列表中搜索条目**默认**属性设置为**true**。 如果 dmrc 如何找到的匹配项，它将选择该元数据包。

4.  如果在步骤 3 期间，dmrc 如何发现多个设备元数据包，它将选择具有的包[ **LastModifiedDate** ](https://msdn.microsoft.com/library/windows/hardware/ff548624)具有最新时间戳的 XML 元素。

以下点是可供选择算法与相关[dmrc 如何](device-metadata-retrieval-client.md):

-   如果 dmrc 如何选择元数据包的基于硬件 Id，它使用的硬件驱动程序安装期间使用的操作系统的 Id 相同的排名。 Dmrc 如何进行排名大于不太具体的硬件 Id 的更具体的硬件 Id。 例如，以下的硬件 Id 会列在排名顺序：

    ```cpp
    <HardwareID>DOID:USB\VID_XXXX&PID_YYYY&REV_0000</HardwareID>
    <HardwareID>DOID:USB\VID_XXXX&PID_YYYY</HardwareID>
    ```

    有关硬件 Id 的信息，请参阅[硬件 Id](hardware-ids.md)。

-   设置应只有一个设备元数据包**默认**的属性[**区域设置**](https://msdn.microsoft.com/library/windows/hardware/ff548647)到 XML 元素**true**。 只应将此属性设置为 true 的包中，包含具有最高的排名值的硬件 ID。

-   [ **LastModifiedDate** ](https://msdn.microsoft.com/library/windows/hardware/ff548624) XML 元素中用于版本控制并用于选择设备的设备元数据包的较新版本。

-   如果本地元数据存储区中的两个或多个设备元数据包包含相同的值[ **ModelIDList**](https://msdn.microsoft.com/library/windows/hardware/ff549303)， [ **HardwareIDList** ](https://msdn.microsoft.com/library/windows/hardware/ff546121)， [**区域设置**](https://msdn.microsoft.com/library/windows/hardware/ff548647)，或[ **LastModifiedDate** ](https://msdn.microsoft.com/library/windows/hardware/ff548624) XML 元素，dmrc 如何选择仅是其中之一的设备。 在这种情况下，dmrc 如何选择这些包之一具有不确定性的方式。

有关设备元数据 XML 架构和元素的详细信息，请参阅[设备元数据架构参考](https://msdn.microsoft.com/library/windows/hardware/ff541452)。

 

 





