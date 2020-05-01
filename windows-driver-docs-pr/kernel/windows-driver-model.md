---
title: Windows 驱动程序模型 (WDM)
description: 本部分介绍了 Windows 驱动模型 (WDM)，并讨论了 WDM 驱动程序的类型、设备配置、驱动程序分层和 WDM 版本控制。
ms.assetid: 9e76c5a8-a19a-44cf-867a-b2246ea8eaf1
keywords:
- 内核模式驱动程序 WDK，WDM 驱动程序
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 5d61d773b7e15b1728631a3fabcaaf51ec80d407
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007582"
---
# <a name="windows-driver-model-wdm"></a>Windows 驱动程序模型 (WDM)


本部分介绍了 Windows 驱动模型  (WDM)，并讨论了 WDM 驱动程序的类型、设备配置、驱动程序分层和 WDM 版本控制。 WDM 简化了编写为在多个版本的 Windows 操作系统上运行的内核模式驱动程序的设计。




## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="introduction-to-wdm.md" data-raw-source="[Introduction to WDM](introduction-to-wdm.md)">WDM 简介</a></p></td>
<td><p>为了使驱动程序开发人员能够编写在所有 Microsoft Windows 操作系统中源代码兼容的设备驱动程序，我们引入了 Windows 驱动模型 (WDM)。 遵循 WDM 规则的内核模式驱动程序称为 WDM 驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="types-of-wdm-drivers.md" data-raw-source="[Types of WDM Drivers](types-of-wdm-drivers.md)">WDM 驱动程序的类型</a></p></td>
<td><p>有三种类型的 WDM 驱动程序：总线驱动程序、函数驱动程序和筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-configurations-and-layered-drivers.md" data-raw-source="[Device Configurations and Layered Drivers](device-configurations-and-layered-drivers.md)">设备配置和分层驱动程序</a></p></td>
<td><p>对于最常见的设备类型，Windows 驱动程序工具包 (WDK) 提供了一组功能完备的系统驱动程序示例。 为类似类型的设备开发新的驱动程序时，可以将单个示例驱动程序用作模型。 但是，系统的驱动程序具有额外的设计要求：要便于开发新的设备驱动程序。 因此，许多系统驱动程序都有一个分层体系结构，以便可以重用某些驱动程序来支持类似设备的新驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdm-versions.md" data-raw-source="[WDM Versions](wdm-versions.md)">WDM 版本</a></p></td>
<td><p>WDM 的更高版本通常支持在更早版本的 WDM 中提供的所有功能，也就是说，每个新版 WDM 都是上一 WDM 版本的超集。 在可能的情况下，跨系统驱动程序应符合任何操作系统上的最低 WDM 版本。</p></td>
</tr>
</tbody>
</table>

 

 

 




