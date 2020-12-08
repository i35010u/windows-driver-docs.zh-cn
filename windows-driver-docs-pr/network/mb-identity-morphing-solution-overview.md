---
title: MB 标识变形解决方案概述
description: 该解决方案将变形设备的 USB 配置映射到一组 USB 功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0900f91569beb16ce64f86b7b9de75643f5b6f5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814961"
---
# <a name="mb-identity-morphing-solution-overview"></a>MB 标识变换解决方案概述


该解决方案将变形设备的 USB 配置映射到一组 USB 功能。 在任意时间点，通过配置)  (一组函数向主机公开。 通过在这些配置之间切换，解决方案实现了变形。

## <a name="logical-configurations"></a>逻辑配置


设备中存在的函数分为以下逻辑集。

*逻辑函数集*

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">逻辑函数集</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 7-配置</p></td>
<td align="left"><p>首次将变形设备插入主机时，Windows 7 和更早版本的 Windows 所选的配置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8-配置</p></td>
<td align="left"><p>变形设备插入主机时由 Windows 8 选择的配置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHV-NCM-1.0-配置</p></td>
<td align="left"><p>用户安装驱动程序包后，在 Windows 7 和更早版本的 Windows 上安装的 IHV 软件所选择的配置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHV-NCM-2.0-配置</p></td>
<td align="left"><p>用户安装驱动程序包后，在 Windows 8 上安装的 IHV 软件所选择的配置。</p></td>
</tr>
</tbody>
</table>

 

下表显示了上表中列出的 USB 配置以及可能的接口和函数。 其余子主题介绍了每个配置的其他要求。

*USB 配置*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">配置 1 (Windows 7-配置) </th>
<th align="left">配置 2 (IHV – NCM-配置) </th>
<th align="left">配置 3 (Windows-8-配置) </th>
<th align="left">配置 4 (IHV – NCM –配置) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>批量 cd-rom</p>
<p>群发 SD</p></td>
<td align="left"><p>批量 cd-rom</p>
<p>群发 SD</p>
<p>NCM 1。0</p>
<p>调制解调器</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC 智能卡</p>
<p>语音</p>
<p>斜</p></td>
<td align="left"><p>批量 cd-rom</p>
<p>群发 SD</p>
<p>MBIM</p></td>
<td align="left"><p>批量 cd-rom</p>
<p>群发 SD</p>
<p>NCM 2。0</p>
<p>调制解调器</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC 智能卡</p>
<p>语音</p>
<p>斜</p></td>
</tr>
</tbody>
</table>

 

解决方案的目标

-   在 Windows 7 中，用户需要执行额外的步骤来安装驱动程序包，然后才能在变形设备上使用移动宽带功能。
-   在 Windows 8 中，用户无需执行额外的步骤来安装驱动程序包，以便在符合 MBIM 规范的变形设备上使用移动宽带功能。
-   在 Windows 8 中，用户需要执行额外的步骤来安装驱动程序包，然后才能在没有收件箱驱动程序的变形设备上使用 IHV 函数。

**假设**

MBIM 还包括 NCM 1.0 的向后兼容性。

## <a name="supported-transitions"></a>支持的转换


适用于 Windows 8

Not-Configured- &gt; 8-配置

Windows-8-配置- &gt; NCM-2.0-配置

对于 Windows 7

Not-Configured- &gt; 7-配置

Windows 7-配置- &gt; IHV – NCM-1.0-配置

![windows 7 和 windows 8 的配置转换路径](images/mbim7.png)

Windows 7 和 Windows 8 的配置转换路径

请注意，不支持以前未显示的任何转换。

## <a name="transition-details"></a>过渡详细信息


请考虑一个示例 USB 变形设备，其中包含其配置中的以下功能。

![具有4个不同配置及其功能的 usb 变形设备](images/mbim8.png)

具有多个功能的 USB 设备

**Windows 8**

Windows 8-配置

将变形设备插入运行 Windows 8 的计算机时，将选择 Windows 8-配置，这将公开 MBIM 函数。 将在 MBIM 函数上加载 Windows 8 Mobile 宽带类驱动程序 (MBCD) 。 在下面的示例中，配置3是包含 MBIM 函数的 Windows 8 配置。

![用于移动宽带设备的 windows 8 和四种配置。 将突出显示配置三。](images/mbim9.png)

设备接通电源后，Windows 8 上的驱动程序堆栈和设备配置

IHV-NCM-2.0-配置

在 Windows 8 配置中，变形设备还具有一个大容量存储功能，该功能将允许用户安装 IHV 驱动程序包。 从大容量存储函数安装驱动程序包之后，设备将进行平滑以公开 NCM-2.0-配置中的函数。 此配置具有其他 IHV 功能，如 GPS、诊断等。 下图中的配置4表示 NCM-2.0-配置。

![windows 8 (安装了驱动程序的驱动程序安装) 和四种配置。 将突出显示配置4。](images/mbim10.png)

用户安装 IHV 驱动程序包后，Windows 8 上的驱动程序堆栈和设备配置

**Windows 7**

Windows 7-配置

将变形设备插入运行 Windows 7 或更早版本的 Windows 的计算机时，将选择 "Windows 7-配置"，这将公开大容量存储功能。 这将允许用户从大容量存储函数安装 IHV 驱动程序包。

在以下示例中，配置1为 Windows 7 配置

![用于移动宽带设备的 windows 7 和四种配置。 将突出显示配置一个。](images/mbim11.png)

用户尚未安装 IHV 驱动程序包时 Windows 7 上的驱动程序堆栈和设备配置

IHV-NCM-1.0-配置

在 Windows 7 中，用户可以从大容量存储函数安装驱动程序包。 除了安装驱动程序软件外，IHV 软件还会将设备从 Windows 7 配置中 1.0 NCM--配置。

![用于移动宽带设备的 windows 7 和四种配置。 将突出显示配置二。](images/mbim12.png)

用户安装 IHV 驱动程序包后，Windows 7 中的驱动程序堆栈和设备配置

 

 





