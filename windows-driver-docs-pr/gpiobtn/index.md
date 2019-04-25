---
title: 硬件通知设计指南
description: 以标准化方式介绍对主要按钮（电源、Windows、音量和旋转锁）和其他指示器的支持，另外还介绍了已关联的相应 Windows 工程指南 (WEG)。
ms.assetid: E18DAA6C-C64D-40B3-A112-682A935655D0
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 89af40e81bf59ba0f68b4e28e40071aed167daeb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323431"
---
# <a name="hardware-notifications-design-guide"></a>硬件通知设计指南


以标准化方式介绍对主要按钮（电源、Windows、音量和旋转锁）和其他指示器的支持，另外还介绍了已关联的相应 Windows 工程指南 (WEG)。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md" data-raw-source="[GPIO buttons and indicators implementation guide](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)">GPIO 按钮和指示器实现指南</a></p></td>
<td align="left"><p>Windows 8 通过 HID 微型端口类驱动程序引入了对常规 I/O (GPIO) 按钮和指示器的支持。 目标是以标准化方式提供对主要按钮（电源、Windows、音量和旋转锁）的支持，另外还介绍了已关联的相应 Windows 工程指南 (WEG)。 Windows 8.1 专注于增强端到端用户体验的质量以及统一各种创新性外形规格的行为。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="gpio-buttons-and-indicators-supplemental-certification-testing-for-windows-8-1.md" data-raw-source="[GPIO buttons and indicators supplemental testing](gpio-buttons-and-indicators-supplemental-certification-testing-for-windows-8-1.md)">GPIO 按钮和指示器实现测试</a></p></td>
<td align="left"><p>本主题介绍适用于硬件按钮和指示器的 Windows 8.1 测试方案，目的是确保在使用不同外形规格时获得理想的用户体验。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="hardware-notifications-support.md" data-raw-source="[Hardware notifications support](hardware-notifications-support.md)">硬件通知支持</a></p></td>
<td align="left"><p>Windows 10 版本 1709 的基础结构可以为 LED 和振动机制等通知组件提供不区分硬件的支持。 实现此支持的方式是引入内核模式驱动程序框架 (KMDF) 类扩展，该扩展专用于硬件通知组件，因此可以快速开发客户端驱动程序。 KMDF 类扩展实质上是 KMDF 驱动程序，它为给定的设备类提供一组定义的功能，类似于 Windows 驱动程序模型 (WDM) 中的端口驱动程序。 此部分概述硬件通知类扩展的体系结构。 有关 KMDF 的其他信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver" data-raw-source="[Using WDF to Develop a Driver](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)">Using WDF to Develop a Driver</a>（使用 WDF 来开发驱动程序）。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[硬件通知参考](https://msdn.microsoft.com/library/windows/hardware/dn789336)



