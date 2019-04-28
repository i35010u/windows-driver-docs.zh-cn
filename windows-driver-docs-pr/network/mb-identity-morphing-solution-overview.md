---
title: MB 标识变形解决方案概述
description: 该解决方案将变形设备的 USB 配置映射到一的 USB 函数。
ms.assetid: 4A3EDD12-00CC-48A0-BCD9-8F64E90FA9F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0ed2366c45c5dc523cd77a0d9f0d9156d5d1495
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343431"
---
# <a name="mb-identity-morphing-solution-overview"></a>MB 标识变换解决方案概述


该解决方案将变形设备的 USB 配置映射到一的 USB 函数。 在任何时间点，一组 （通过配置） 的功能是向主机公开的。 该解决方案来实现变形通过这些配置之间切换。

## <a name="logical-configurations"></a>逻辑配置


在设备中存在的函数可分为以下逻辑集。

*逻辑组的函数*

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">逻辑组的函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows-7-Configuration</p></td>
<td align="left"><p>第一次变形设备插入到主机时选择的 Windows 7 和 Windows 的较旧版本的配置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows-8-Configuration</p></td>
<td align="left"><p>变形设备插入到主机时，Windows 8 通过所选的配置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IHV-NCM-1.0-Configuration</p></td>
<td align="left"><p>IHV 软件用户安装的驱动程序包后，在 Windows 7 和较旧版本的 Windows 上安装所选的配置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHV-NCM-2.0-Configuration</p></td>
<td align="left"><p>IHV 软件用户安装的驱动程序包后，在 Windows 8 上安装所选的配置。</p></td>
</tr>
</tbody>
</table>

 

下表显示了可能的接口和函数以及上表中列出的 USB 配置。 中的剩余的子主题描述了每个配置的其他要求。

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
<th align="left">配置 1 （Windows 7 配置）</th>
<th align="left">配置 2(IHV–NCM-10-Configuration)</th>
<th align="left">配置 3 (Windows 8 配置)</th>
<th align="left">配置 4 (IHV – NCM-20-配置)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>大容量 CD-ROM</p>
<p>大容量 SD</p></td>
<td align="left"><p>大容量 CD-ROM</p>
<p>大容量 SD</p>
<p>NCM1.0</p>
<p>调制解调器</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC 智能卡</p>
<p>语音</p>
<p>诊断工具</p></td>
<td align="left"><p>大容量 CD-ROM</p>
<p>大容量 SD</p>
<p>MBIM</p></td>
<td align="left"><p>大容量 CD-ROM</p>
<p>大容量 SD</p>
<p>NCM2.0</p>
<p>调制解调器</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC 智能卡</p>
<p>语音</p>
<p>诊断工具</p></td>
</tr>
</tbody>
</table>

 

解决方案的目标

-   在 Windows 7 中，用户需要执行额外的步骤，然后才能使用移动宽带函数变形的设备上安装驱动程序包。
-   在 Windows 8 中，用户应该不需要安装驱动程序包，用于移动宽带函数变形符合 MBIM 规范的设备上执行额外的步骤。
-   在 Windows 8 中，用户需要执行额外的步骤，然后才能使用 IHV 函数变形而没有收件箱驱动程序的设备上安装驱动程序包。

**假设**

MBIM NCM 1.0 还包括向后兼容性。

## <a name="supported-transitions"></a>受支持的转换


适用于 Windows 8

未配置-&gt; Windows 8 配置

Windows 8 配置-&gt; IHV NCM 2.0 配置

有关 Windows 7

未配置-&gt; 7 的 Windows 配置

Windows-7-Configuration -&gt; IHV–NCM-1.0-Configuration

![配置适用于 windows 7 和 windows 8 的转换路径](images/mbim7.png)

Windows 7 和 Windows 8 的配置转换路径

请注意，不会显示任何转换之前，不支持。

## <a name="transition-details"></a>转换详细信息


请考虑使用以下函数在其配置中的示例 USB 变形设备。

![usb 变形具有 4 个不同配置的设备和及其功能](images/mbim8.png)

多个函数的 USB 设备

**Windows 8**

Windows-8-Configuration

当变形设备插入到运行 Windows 8 的计算机时，Windows 8 配置将被选中，公开 MBIM 函数。 Windows 8 移动宽带类驱动程序 (MBCD) 将加载上 MBIM 函数。 在以下示例中，配置 3 是 Windows 8-配置包含 MBIM 函数。

![移动宽带设备的 windows 8 和四个配置。 配置三个突出显示。](images/mbim9.png)

在 Windows 8 后在插入设备上的驱动程序堆栈和设备配置

IHV-NCM-2.0-Configuration

在 Windows-8-配置变形设备还具有将允许用户安装 IHV 驱动程序包的大容量存储函数。 从大容量存储函数的驱动程序包的安装后，设备将执行 morph 以公开 IHV NCM-2.0-配置中的函数。 此配置具有其他 IHV 函数如 GPS、 诊断和等等。 下图中的配置 4 表示的 IHV-NCM-2.0-配置。

![windows 8 （驱动程序安装后） 和移动宽带设备有关的以下四种配置。 配置四个突出显示。](images/mbim10.png)

在 Windows 8 中的用户安装 IHV 驱动程序包之后，驱动程序的堆栈和设备配置

**Windows 7**

Windows-7-Configuration

当变形设备插入到运行 Windows 7 或 Windows 的早期版本的计算机时，Windows 7 配置将被选中，公开大容量存储函数。 这将允许用户从大容量存储函数安装 IHV 驱动程序包。

在以下示例中，配置 1 是 Windows 7 配置

![移动宽带设备的 windows 7 和四个配置。 配置一个突出显示。](images/mbim11.png)

当用户在不安装 IHV 驱动程序包的 Windows 7 上的驱动程序堆栈和设备配置

IHV-NCM-1.0-Configuration

在 Windows 7 中，用户可以从大容量存储函数安装驱动程序包。 安装驱动程序软件，以及 IHV 软件将执行从 Windows 7 配置设备的 IHV-NCM-1.0-配置还 morph。

![移动宽带设备的 windows 7 和四个配置。 配置两个将突出显示。](images/mbim12.png)

在 Windows 7 中的用户安装 IHV 驱动程序包之后，驱动程序的堆栈和设备配置

 

 





