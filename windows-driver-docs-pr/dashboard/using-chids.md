---
title: 使用计算机硬件 ID (CHID)
description: 计算机硬件 ID (CHID) 在“为计算机指定硬件 ID”中定义。
ms.assetid: 45DCAED5-8D20-4A31-B316-0460AB030DAD
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44b223e99c2be3f0efeeed7360e0620c35d0462f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518127"
---
# <a name="using-computer-hardware-ids-chids"></a>使用计算机硬件 ID (CHID)


计算机硬件 ID (CHID) 在[为计算机指定硬件 ID](https://msdn.microsoft.com/windows/hardware/drivers/install/specifying-hardware-ids-for-a-computer) 中定义。

Windows 10 添加多个合并基板制造商和基板产品信息的新 CHID。 这些新 CHID 包含在 CHID 层次结构中，如下表所示。 此表以特异性的降序顺序显示该层次结构。 Windows 10 中新添加的 CHID 以粗体突出显示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>HWID</th>
<th>目录</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HardwareID-0</p></td>
<td><p>制造商 + 系列 + 产品名称 + SKU 号 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本</p></td>
</tr>
<tr class="even">
<td><p>HardwareID-1</p></td>
<td><p>制造商 + 系列 + 产品名称 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-2</p></td>
<td><p>制造商 + 产品名称 + BIOS 供应商 + BIOS 版本 + BIOS 主要版本 + BIOS 次要版本</p></td>
</tr>
<tr class="even">
<td><p>HardwareID-3</p></td>
<td><p><strong>制造商 + 系列 + 产品名称 + SKU 号 + Baseboard_Manufacturer + Baseboard_Product</strong></p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-4</p></td>
<td><p>制造商 + 系列 + 产品名称 + SKU 号</p></td>
</tr>
<tr class="even">
<td><p>HardwareID-5</p></td>
<td><p>制造商 + 系列 + 产品名称</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-6</p></td>
<td><p><strong>制造商 + SKU 号 + Baseboard_Manufacturer + Baseboard_Product</strong></p></td>
</tr>
<tr class="even">
<td><p>HardwareID-7</p></td>
<td><p>制造商 + SKU 号</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-8</p></td>
<td><p><strong>制造商 + 产品名称 + Baseboard_Manufacturer + Baseboard_Product</strong></p></td>
</tr>
<tr class="even">
<td><p>HardwareID-9</p></td>
<td><p>制造商 + 产品名称</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-10</p></td>
<td><p><strong>制造商 + 系列 + Baseboard_Manufacturer + Baseboard_Product</strong></p></td>
</tr>
<tr class="even">
<td><p>HardwareID-11</p></td>
<td><p>制造商 + 系列</p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-12</p></td>
<td><p>制造商 + 机箱类型</p></td>
</tr>
<tr class="even">
<td><p>HardwareID-13</p></td>
<td><p><strong>制造商 + Baseboard_Manufacturer + Baseboard_Product</strong></p></td>
</tr>
<tr class="odd">
<td><p>HardwareID-14</p></td>
<td><p>制造商</p></td>
</tr>
</tbody>
</table>

 

OEM 必须向驱动程序发布者提供正确的 CHID 信息。 包含在 Windows 桌面工具 SDK 中的 [ComputerHardwareIds](https://msdn.microsoft.com/library/windows/hardware/ff543505) 工具有助于从一组已知的系统管理 BIOS (SMBIOS) 值中报告 CHID。 ComputerHardwareIds 执行两个不同的任务。

1.  默认行为：该工具报告系统的 SMBIOS 值和生成的 CHID。

    默认情况下，该工具显示系统的 SMBIOS 值以及从 SMBIOS 值中生成的 CHID。

2.  模拟行为：该工具从用户提供的 SMBIOS 值中生成 CHID。

    可使用模拟 SMBIOS 值（例如制造商、系列和 SKU）运行该工具，以获取生成的 CHID 列表。 这允许你确定将在带有特定 SMBIOS 数据值的系统上生成哪些 CHID。

## <a name="span-idtipsforconsistentchidsspanspan-idtipsforconsistentchidsspanspan-idtipsforconsistentchidsspantips-for-consistent-chids"></a><span id="Tips_for_consistent_CHIDs"></span><span id="tips_for_consistent_chids"></span><span id="TIPS_FOR_CONSISTENT_CHIDS"></span>一致 CHID 的提示


CHID 基于区分大小写的 SMBIOS 值生成。 必须小心地确保系统不在 SMBIOS 文本值中混合大小写。 同样，不特殊处理 UNICODE 字符。 区别对待特殊字符的大写和小写版本，如土耳其语的带点和不带点的字母 I：I、ı、İ 和 i 是不同的。

ComputerHardwareIds 工具仅计算提供必要的 SMBIOS 值的 CHID。 如果缺少 SMBIOS 数据字段（或为空），不会生成任何相关的 CHID。 例如，如果 SMBIOS SKU 字段为空，CHID 0、3、4、6 和 7 将不可用于该特定系统。

有关 CHID 的详细信息，请参阅[指定计算机的硬件 ID](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer)。

 

 





