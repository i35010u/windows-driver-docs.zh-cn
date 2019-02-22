---
title: Windows 搜索驱动程序的位置
description: Windows 搜索驱动程序的位置
ms.assetid: 4c193b97-7b70-425f-99f2-ba976a4cc40a
keywords:
- 驱动程序选择 WDK 设备安装，其中设备 setupsearches
- 定位驱动程序对于设备安装 WDK 设备安装，其中设备 setupsearches
- 设备安装 WDK 设备安装期间，搜索驱动程序的设备 setupsearches
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08daf6511d424e5d892c4c1afd13ff3f0db73b01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533555"
---
# <a name="where-windows-searches-for-drivers"></a>Windows 搜索驱动程序的位置


连接设备后，Windows 将尝试找到匹配[驱动程序包](driver-packages.md)其可以安装设备的驱动程序。 Windows 搜索驱动程序包从不同位置，并在两个阶段中执行此搜索下, 表中所述。

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
<th align="left">Windows 8 和更高版本的 Windows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">之前安装驱动程序</td>
<td align="left"><p>DevicePath</p>
<p>Windows 更新</p>
<p><a href="driver-store.md" data-raw-source="[Driver store](driver-store.md)">驱动程序存储区</a></p></td>
<td align="left"><a href="driver-store.md" data-raw-source="[Driver store](driver-store.md)">驱动程序存储区</a></td>
</tr>
<tr class="even">
<td align="left">选定后初始驱动程序</td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>DevicePath</p>
<p>Windows 更新</p></td>
</tr>
</tbody>
</table>

 

### <a name="searching-for-driver-packages"></a>搜索驱动程序包

连接设备后，Windows 将首先尝试查找并按如下所示在无需用户交互，受信任的系统上下文中安装一个驱动程序：

-   在设备上，允许快速开始操作对设备首次安装驱动程序存储区中已存在的最佳匹配驱动程序。 在并行和不同的过程中，将发生以下情况：

-   Windows 会自动下载匹配[驱动程序包](driver-packages.md)从 Windows 更新。 如果找到匹配的驱动程序包，Windows 会将程序包下载和暂存到[驱动程序存储区](driver-store.md)。 在 Windows 10 版本 1709年及更高版本，Windows 提供了最排名的驱动程序，而不一定是最新。 驱动程序分级会考虑 HWID，日期/版本和关键/自动/的可选类别。 Windows 对关键的或自动驱动程序最高评级。 如果找不到匹配的驱动程序，WU 会查找下一步的可选驱动程序。 因此，否则为相同级别的旧的关键驱动程序将优先于较新的可选驱动程序。 在 Windows 版本早于 1709，Windows 提供关键和可选的更新具有相同的优先级。

    Windows 还会搜索驱动程序包的位置预先加载由指定的**DevicePath**注册表值。 此值是注册表的下列子项下。

    ```cpp
    HKEY_LOCAL_MACHINE
       Software
          Microsoft
             Windows
                CurrentVersion
    ```

    默认情况下**DevicePath**值指定的 %systemroot%\\INF 目录。

    如果更好地匹配比最初安装的驱动程序包位于 Windows 更新上或在由指定的位置**DevicePath**值，Windows 先暂存的驱动程序包[驱动程序存储区](driver-store.md)之前安装该驱动程序。 这样一来，Windows 始终从驱动程序存储区安装驱动程序。

 

 





