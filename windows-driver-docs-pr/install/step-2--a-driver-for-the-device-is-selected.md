---
title: 步骤2选择设备的驱动程序
description: 步骤2选择设备的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25de1f66ec92ada6c7c3541064cff97b9d7452f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829849"
---
# <a name="step-2-a-driver-for-the-device-is-selected"></a>步骤 2：选择设备的驱动程序


检测到新设备并进行识别后，Windows 及其 [设备安装组件](/previous-versions/ff541277(v=vs.85)) 将执行以下步骤：

1.  Windows 将在设备上搜索合适的 [驱动程序包](driver-packages.md) 。 有关此步骤的详细信息，请参阅 [搜索驱动程序包](#searching-for-the-driver)。
2.  Windows 从一个或多个驱动程序包中为设备选择最适合的驱动程序。 有关此步骤的详细信息，请参阅 [选择驱动程序](#selecting-the-driver)。

### <a name="searching-for-the-driver-package"></a><a href="" id="searching-for-the-driver"></a>搜索驱动程序包

使用由总线或集线器驱动程序报告的 [硬件标识符 (ID) ](hardware-ids.md) ，Windows 会搜索与设备匹配的 [驱动程序包](driver-packages.md) 。 如果硬件 ID 与驱动程序包的 [inf 文件](overview-of-inf-files.md)的 " [**INF *模型*" 部分**](inf-models-section.md)条目中的硬件 id 或 [兼容 ID](compatible-ids.md)相匹配，则驱动程序包与设备匹配。

根据操作系统版本，Windows 会在不同位置中搜索匹配的驱动程序包，如下表所述。

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

 

例如，如果用户在运行 Windows 7 的计算机上将无线局域网 (WLAN) 适配器插入 USB 集线器的端口，则会执行以下步骤：

-   USB 集线器驱动程序创建 WLAN 适配器的硬件 Id 列表后，Windows 会先在 [驱动程序存储区](driver-store.md) 中搜索设备的匹配 [驱动程序包](driver-packages.md) 。

-   设备安装过程从下列位置之一搜索匹配的驱动程序包：

    -   通用命名约定 (*UNC*) 路径，由 **HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ Windows \\ CurrentVersion** 的 **DevicePath** 注册表值标识。

    -   Windows 更新

    -   独立硬件供应商 (IHV) 为设备提供的分发介质。

    如果找到了驱动程序包，Windows 会将包暂存到驱动程序存储区中，将在该驱动程序存储区中安装设备驱动程序。

**注意** 从 Windows Vista 开始，操作系统始终从 [驱动程序存储区](driver-store.md)安装 [驱动程序包](driver-packages.md)。 如果在其他位置找到了匹配的驱动程序包，则 Windows 首先会将包安装到驱动程序存储区，然后再安装设备驱动程序。

 

再举一个例子，如果用户将 WLAN 适配器插入运行 Windows 8 的计算机上的 USB 集线器端口，则会执行以下步骤：

-   USB 集线器驱动程序为 WLAN 适配器创建硬件 ID 后，Windows 会先在驱动程序存储区中搜索设备的匹配 [驱动程序包](driver-packages.md) 。 如果在驱动程序存储区中找到了驱动程序包，则 Windows 将在设备上安装该程序包。 这允许设备快速开始工作。

-   在单独的进程中，Windows 会搜索 Windows 更新和 DevicePath，以便获得比安装更好的驱动程序。 如果找到一个，驱动程序将暂存到驱动程序存储区中，然后安装到设备上。

有关 [驱动程序包](driver-packages.md) 搜索过程的详细信息，请参阅 [Windows 搜索驱动程序的位置](./how-windows-selects-a-driver-for-a-device.md)。

### <a name="selecting-the-driver"></a>选择驱动程序

一旦 Windows 找到了设备的一个或多个匹配的 [驱动程序包](driver-packages.md) ，windows 会按照以下步骤选择最佳驱动程序：

1.  如果 Windows 只找到一个匹配的驱动程序包，则会从该设备的该包中安装驱动程序。

2.  如果 Windows 找到多个匹配的驱动程序包，则 Windows 首先会将排名值从每个驱动程序包分配给驱动程序。 如果仅有一个驱动程序的排名值最低，则会从该设备的该程序包安装驱动程序。

    有关排名过程的详细信息，请参阅 [Windows 如何对驱动程序进行排名](how-setup-ranks-drivers--windows-vista-and-later-.md)。

3.  如果多个驱动程序具有相同的最低排名值，Windows 将使用以下条件来选择设备的最佳驱动程序：

    -   驱动程序是否已进行数字签名。 从 Windows Vista 开始，无论其他选择条件如何，Windows 始终会选择签名的驱动程序而不是未签名的驱动程序。 有关驱动程序的数字签名的详细信息，请参阅 [驱动程序签名](driver-signing.md)。

    -   驱动程序日期和版本，其中的日期和版本由驱动程序包的 [inf 文件](overview-of-inf-files.md)中包含的 [**INF DriverVer 指令**](inf-driverver-directive.md)指定。

Windows 选择设备驱动程序后，Windows [会按照步骤3：安装设备驱动程序](step-3--the-driver-for-the-device-is-installed.md)中所述安装驱动程序。

有关如何为设备选择驱动程序的详细信息，请参阅 [Windows 如何选择驱动程序](./how-windows-selects-a-driver-for-a-device.md)。

