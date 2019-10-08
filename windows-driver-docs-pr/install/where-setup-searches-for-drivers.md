---
title: Windows 搜索驱动程序的位置
description: Windows 搜索驱动程序的位置
ms.assetid: 4c193b97-7b70-425f-99f2-ba976a4cc40a
keywords:
- 驱动程序选择 WDK 设备安装，其中设备 setupsearches
- 查找设备安装的设备安装 WDK 设备安装的驱动程序，其中设备 setupsearches
- 在设备安装过程中搜索驱动程序安装 WDK 设备，其中设备 setupsearches
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 861a2fea00fcc7f7cb5ecf1cc17805f86d86ff7b
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007646"
---
# <a name="where-windows-searches-for-drivers"></a>Windows 搜索驱动程序的位置


附加设备后，Windows 会尝试查找可从中安装设备驱动程序的匹配的[驱动程序包](driver-packages.md)。 Windows 在两个阶段中搜索驱动程序包，并按下表中所述的两个阶段执行此搜索。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">搜索阶段</th>
<th align="left">Windows 7</th>
<th align="left">Windows 8 及更高版本的 Windows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">安装驱动程序之前</td>
<td align="left"><p>DevicePath</p>
<p>Windows 更新</p>
<p><a href="driver-store.md" data-raw-source="[Driver store](driver-store.md)">驱动程序存储</a></p></td>
<td align="left"><a href="driver-store.md" data-raw-source="[Driver store](driver-store.md)">驱动程序存储</a></td>
</tr>
<tr class="even">
<td align="left">选择初始驱动程序之后</td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>DevicePath</p>
<p>Windows 更新</p></td>
</tr>
</tbody>
</table>

 

### <a name="searching-for-driver-packages"></a>搜索驱动程序包

附加设备后，Windows 首先会尝试在不受信任的系统上下文中找到并安装驱动程序，如下所示：

-   首先将驱动程序存储区中已存在的最佳匹配驱动程序安装到设备上，使设备能够快速启动操作。 在不同的进程中，将发生以下情况：

-   Windows 自动从 Windows 更新下载匹配的[驱动程序包](driver-packages.md)。 如果找到了匹配的驱动程序包，则 Windows 将下载包并将其暂存到[驱动程序存储区](driver-store.md)。 在 Windows 10 版本1709及更高版本中，Windows 提供了最好的排名最好的驱动程序，这并不是最新的。 驱动程序排名考虑 HWID、日期/版本和严重/自动/可选类别。 Windows 排名严重或自动驱动程序最高。 如果找不到匹配的驱动程序，则 WU 会在可选驱动程序中查找。 因此，其他相等级别的旧关键驱动程序优先于较新的可选驱动程序。 在早于1709的 Windows 版本中，Windows 提供具有相同优先级的关键更新和可选更新。

    Windows 还会搜索在**DevicePath**注册表值指定的位置预加载的驱动程序包。 此值在注册表的下列子项下。

    ```cpp
    HKEY_LOCAL_MACHINE
       Software
          Microsoft
             Windows
                CurrentVersion
    ```

    默认情况下， **DevicePath**值指定% SystemRoot% \\INF 目录。

    如果在 Windows 更新或在**DevicePath**值指定的位置找到更好的匹配驱动程序包，则 Windows 首先将驱动程序包置于驱动程序[存储区](driver-store.md)中，然后再安装驱动程序。随. 这样，Windows 将始终从驱动程序存储区中安装驱动程序。

 

 





