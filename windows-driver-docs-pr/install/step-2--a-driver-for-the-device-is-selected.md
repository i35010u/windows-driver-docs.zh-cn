---
title: 选择该设备的步骤 2 驱动程序
description: 选择该设备的步骤 2 驱动程序
ms.assetid: 2134cab6-58ea-4258-9a45-09bf54156e0a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45dcb8b103765de7969092f6d8f802494c9a3234
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565141"
---
# <a name="step-2-a-driver-for-the-device-is-selected"></a>步骤 2：选择设备的驱动程序


检测到新设备并将其标识 Windows 后并将其[设备安装组件](https://msdn.microsoft.com/library/windows/hardware/ff541277)请执行以下步骤：

1.  Windows 搜索的相应[驱动程序包](driver-packages.md)设备。 有关此步骤的详细信息，请参阅[为驱动程序包搜索](#searching-for-the-driver)。
2.  Windows 从一个或多个驱动程序包中选择最适用于设备的驱动程序。 有关此步骤的详细信息，请参阅[选择该驱动程序](#selecting-the-driver)。

### <a href="" id="searching-for-the-driver"></a>搜索驱动程序包

使用[硬件标识符 (ID)](hardware-ids.md)总线或中心驱动程序，Windows 搜索报告[驱动程序包](driver-packages.md)与设备相匹配。 驱动程序包与设备相匹配，如果硬件 ID 相匹配的硬件 ID 或[兼容 ID](compatible-ids.md)中[ **INF*模型*部分**](inf-models-section.md)的条目驱动程序包[INF 文件](inf-files.md)。

具体取决于操作系统版本，Windows 搜索匹配的以下表中所述的不同位置中的驱动程序包。

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

 

例如，如果用户运行的 Windows 7 的计算机上的 USB 集线器的端口将无线局域网 (WLAN) 适配器，则执行以下步骤：

-   USB 集线器驱动程序创建一个用于将 WLAN 适配器的硬件 Id 的列表后，Windows 将首先搜索[驱动程序存储区](driver-store.md)匹配[驱动程序包](driver-packages.md)设备。

-   设备安装过程中搜索匹配的驱动程序包从以下位置之一：

    -   通用命名约定 (*UNC*) 由标识的路径**DevicePath**的注册表值**HKEY_LOCAL_MACHINE\\软件\\Microsoft\\Windows\\CurrentVersion**。

    -   Windows 更新

    -   独立硬件供应商 (IHV) 提供的设备分发媒体。

    如果找到驱动程序包，则 Windows 将从其安装在设备的驱动程序在驱动程序存储中暂存程序包。

**请注意**  从 Windows Vista 开始，在操作系统始终安装[驱动程序包](driver-packages.md)从[驱动程序存储区](driver-store.md)。 如果匹配的驱动程序包位于在另一个位置中，Windows 驱动程序程序包存储之前会安装设备驱动程序的第一个阶段。

 

另举一例，如果用户运行 Windows 8 的计算机上的 USB 集线器的端口将 WLAN 适配器将执行以下步骤：

-   USB 集线器驱动程序创建将 WLAN 适配器的硬件 ID 后，Windows 将首先搜索匹配的驱动程序存储区[驱动程序包](driver-packages.md)设备。 如果在驱动程序存储区中找到驱动程序的程序包，Windows 会将其安装在设备上。 这样，若要开始快速工作的设备。

-   单独的进程，在 Windows 搜索 Windows Update 和更好地匹配的驱动程序 DevicePath 比已安装。 如果找到一个，则驱动程序暂存到驱动程序存储区，，，然后安装在设备上。

有关详细信息[驱动程序包](driver-packages.md)搜索过程，请参阅[其中 Windows 搜索驱动程序](where-setup-searches-for-drivers.md)。

### <a name="selecting-the-driver"></a>选择驱动程序

只要 Windows 已找到一个或多个匹配[驱动程序包](driver-packages.md)对于设备，Windows 会通过执行以下步骤选择最适合的驱动程序：

1.  如果 Windows 已找到一个匹配的驱动程序包，会从设备该包安装驱动程序。

2.  如果 Windows 已找到多个匹配的驱动程序包，Windows 先将分配一个排名值给驱动程序从每个驱动程序包。 如果只有一个驱动程序具有最低的排名值，它将从设备该包安装驱动程序。

    有关排序过程的详细信息，请参阅[如何 Windows Ranks Drivers](how-setup-ranks-drivers.md)。

3.  如果多个驱动程序具有相同最低排名值，Windows 将使用以下条件来选择该设备的最佳驱动程序：

    -   是否进行数字签名的驱动程序。 从 Windows Vista 开始，Windows 始终选择签名的驱动程序而不是未签名的驱动程序，而不考虑其他选择条件。 有关数字签名的驱动程序的详细信息，请参阅[驱动程序签名](driver-signing.md)。

    -   驱动程序日期和版本，其中由指定的日期和版本[ **INF DriverVer 指令**](inf-driverver-directive.md)驱动程序包中包含的[INF 文件](inf-files.md)。

一旦 Windows，已选中设备的驱动程序，Windows 安装驱动程序，如中所述[步骤 3:安装设备的驱动程序](step-3--the-driver-for-the-device-is-installed.md)。

有关如何为设备选择驱动程序的详细信息，请参阅[Windows 中如何选择驱动程序](how-setup-selects-drivers.md)。

 

 





