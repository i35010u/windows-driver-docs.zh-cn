---
title: DMRC 如何确定何时搜索 WMIS 服务器
description: DMRC 如何确定何时搜索 WMIS 服务器
ms.assetid: dc68045e-85c2-443d-9e4d-099bbd21590d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c80c21f3267cd4d88bada6f24df18260c276b51
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568661"
---
# <a name="how-the-dmrc-determines-when-to-search-the-wmis-server"></a>DMRC 如何确定何时搜索 WMIS 服务器


设备元数据检索客户端 ([dmrc 如何](device-metadata-retrieval-client.md)) 维护的设备元数据包缓存。 此缓存填充的 dmrc 如何从 Windows 元数据和 Internet 服务下载的元数据包 ([WMIS](windows-metadata-and-internet-services.md)) 服务器。

当设备和打印机或设备阶段打开用户界面 (Ui)，dmrc 如何搜索用户界面中显示每个设备的最适当的和当前元数据包其缓存。

定期，它从其缓存选择元数据包之前，dmrc 如何搜索较新的设备元数据包上[WMIS](windows-metadata-and-internet-services.md)服务器。 如果找到，dmrc 如何下载包并将其安装在计算机上其缓存。 然后，dmrc 如何选择从其缓存的元数据包的较新版本。

根据以下值，dmrc 如何决定何时搜索[WMIS](windows-metadata-and-internet-services.md)较新的设备元数据包的服务器：

<a href="" id="lastcheckeddate"></a>**LastCheckedDate**  
此值指示的最新 dmrc 如何查询设备元数据的 WMIS 服务器时的日期。 此日期不反映 dmrc 如何是否已成功下载的元数据的包。

Dmrc 如何管理包含的设备元数据包的每个属性的索引表[设备 ID](device-ids.md)系统中。 **LastCheckedDate**值是此索引表中每行的字段。

<a href="" id="checkbackmdnotretrieved"></a>**CheckBackMDNotRetrieved**  
此注册表值指示的天数 dmrc 如何在为设备元数据包重复 WMIS 服务器的查询前等待。 此值适用于为其 dmrc 如何尚未下载的元数据从 WMIS 的设备。

**CheckBackMDNotRetrieved**值位于以下注册表项下：

```cpp
HKLM\Software\Microsoft\Windows\CurrentVersion\Device Metadata
```

下表描述的格式和值范围**CheckBackMDNotRetrieved**值。

| 数据类型  | 值范围         | 默认值 |
|------------|---------------------|---------------|
| [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) | 0 到 256 个，非独占 | 5             |

 

<a href="" id="checkbackmdretrieved"></a>**CheckBackMDRetrieved**  
此注册表值指示的天数 dmrc 如何在它查询之前等待更新设备元数据包。 此值适用于设备 dmrc 如何以前已下载的元数据的包。

**CheckBackMDRetrieved**值位于以下注册表项下：

```cpp
HKLM\Software\Microsoft\Windows\CurrentVersion\Device Metadata
```

下表描述的格式和值范围**CheckBackMDRetrieved**值。

| 数据类型  | 值范围         | 默认值 |
|------------|---------------------|---------------|
| [REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types) | 0 到 256 个，非独占 | 8             |

 

**请注意**  WMIS 服务器合作 dmrc 如何，使用设置的值**CheckBackMDRetrieved**并**CheckBackMDNotRetrieved**客户端上的注册表值系统。 这些值根据设置的网络状况和负载均衡。 每个来自 WMIS 服务器响应包含的客户端配置数据，并控制 dmrc 如何行为。

 

Dmrc 如何按照以下步骤来确定是否搜索 WMIS 服务器的较新的设备元数据包：

1.  如果目标设备[设备 ID](device-ids.md)未列出在 dmrc 如何索引表中，dmrc 如何搜索设备元数据包第一次。 在这种情况下，dmrc 如何查询 WMIS 服务器。

2.  如果目标设备[设备 ID](device-ids.md)列出在 dmrc 如何索引表中，dmrc 如何计算是否要在查询 WMIS 服务器再次为设备元数据包的时间。 在这种情况下，dmrc 如何查询 WMIS 服务器，如下所示：

    1.  Dmrc 如何 dmrc 如何以前已经下载设备元数据包的设备，如果将的值进行比较**CheckBackMDRetrieved**注册表项的当前日期减值**LastCheckedDate**值。 如果**CheckBackMDRetrieved**较小的值、 dmrc 如何查询 WMIS 服务器。

    2.  Dmrc 如何 dmrc 如何以前尚未下载设备元数据包的设备，如果将的值进行比较**CheckBackMDNotRetrieved**注册表项的当前日期减值**LastCheckedDate**值。 如果**CheckBackMDNotRetrieved**较小的值、 dmrc 如何查询 WMIS 服务器。

 

 





