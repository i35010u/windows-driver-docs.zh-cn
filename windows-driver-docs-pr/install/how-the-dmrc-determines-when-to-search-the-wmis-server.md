---
title: DMRC 如何确定何时搜索 WMIS 服务器
description: DMRC 如何确定何时搜索 WMIS 服务器
ms.assetid: dc68045e-85c2-443d-9e4d-099bbd21590d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df13f3e0cddbd17b5d5d1ccf3a00eb9f9b9415d0
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095271"
---
# <a name="how-the-dmrc-determines-when-to-search-the-wmis-server"></a>DMRC 如何确定何时搜索 WMIS 服务器


设备元数据检索客户端 ([DMRC](device-metadata-retrieval-client.md)) 维护设备元数据包的缓存。 此缓存中填充了 DMRC 从 Windows 元数据和 Internet 服务 ([WMIS](windows-metadata-and-internet-services.md)) 服务器下载的元数据包。

当打开设备和打印机或设备阶段 (Ui) 的用户界面时，DMRC 会在其缓存中搜索在 UI 中显示的每个设备的最合适和最新的元数据包。

在从其缓存中选择元数据包之前，DMRC 会定期搜索 [WMIS](windows-metadata-and-internet-services.md) 服务器上某个设备的更新的元数据包。 如果找到一个，DMRC 将下载包并将其安装在计算机上的缓存中。 然后，DMRC 从其缓存中选择较新版本的元数据包。

根据以下值，DMRC 确定何时在 [WMIS](windows-metadata-and-internet-services.md) 服务器中搜索设备的更新的元数据包：

<a href="" id="lastcheckeddate"></a>**LastCheckedDate**  
此值指示 DMRC 在 WMIS 服务器中查询设备的元数据时的最近日期。 此日期不会反映 DMRC 是否已成功下载元数据包。

DMRC 管理包含系统中每个 [设备 ID](device-ids.md) 的设备元数据包的属性的索引表。 **LastCheckedDate**值是此索引表中每行的一个字段。

<a href="" id="checkbackmdnotretrieved"></a>**CheckBackMDNotRetrieved**  
此注册表值指示 DMRC 在对设备元数据包重复 WMIS 服务器的查询之前等待的天数。 此值适用于 DMRC 尚未下载 WMIS 的元数据的设备。

**CheckBackMDNotRetrieved**值位于以下注册表项下：

```cpp
HKLM\Software\Microsoft\Windows\CurrentVersion\Device Metadata
```

下表描述了 **CheckBackMDNotRetrieved** 值的格式和值范围。

| 数据类型  | 取值范围         | 默认值 |
|------------|---------------------|---------------|
| REG_DWORD  | 0到256（含） | 5             |

 

<a href="" id="checkbackmdretrieved"></a>**CheckBackMDRetrieved**  
此注册表值指示 DMRC 在查询已更新设备元数据包之前等待的天数。 此值适用于 DMRC 先前已下载元数据包的设备。

**CheckBackMDRetrieved**值位于以下注册表项下：

```cpp
HKLM\Software\Microsoft\Windows\CurrentVersion\Device Metadata
```

下表描述了 **CheckBackMDRetrieved** 值的格式和值范围。

| 数据类型  | 取值范围         | 默认值 |
|------------|---------------------|---------------|
| REG_DWORD  | 0到256（含） | 8             |

 

**注意**   WMIS 服务器与 DMRC 合作，设置客户端系统上的**CheckBackMDRetrieved**和**CheckBackMDNotRetrieved**注册表值的值。 这些值是基于网络条件和负载平衡设置的。 来自 WMIS 服务器的每个响应都包含客户端配置数据并控制 DMRC 行为。

 

DMRC 遵循以下步骤来确定是否必须在 WMIS 服务器上搜索设备的更新的元数据包：

1.  如果目标设备的 [设备 ID](device-ids.md) 未在 DMRC 索引表中列出，则 DMRC 将首次搜索设备的元数据包。 在这种情况下，DMRC 将查询 WMIS 服务器。

2.  如果 DMRC 索引表中列出了目标设备的 [设备 ID](device-ids.md) ，则 DMRC 将计算是否需要再次查询设备的元数据包的 WMIS 服务器。 在这种情况下，DMRC 将按以下方式查询 WMIS 服务器：

    1.  如果 DMRC 先前已下载设备的设备元数据包，则 DMRC 会将 **CheckBackMDRetrieved** 注册表项的值与当天日期减去 **LastCheckedDate** 值的值进行比较。 如果 **CheckBackMDRetrieved** 值较小，则 DMRC 将查询 WMIS 服务器。

    2.  如果 DMRC 之前未下载设备的设备元数据包，则 DMRC 会将 **CheckBackMDNotRetrieved** 注册表项的值与当天日期的值减去 **LastCheckedDate** 值进行比较。 如果 **CheckBackMDNotRetrieved** 值较小，则 DMRC 将查询 WMIS 服务器。

 

