---
description: 可以使用 Microsoft 网络监视器（也称为 Netmon）查看 USB ETW 事件跟踪。
title: Netmon 中的 USB ETW 跟踪的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb7e9d991ae9febe3f4b52268fb52757a6d2758e
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969072"
---
# <a name="overview-of-usb-etw-traces-in-netmon"></a>Netmon 中的 USB ETW 跟踪的概述


可以使用 Microsoft 网络监视器（也称为 Netmon）查看 USB ETW 事件跟踪。 Netmon 不会自动分析跟踪。 它需要 USB ETW 分析。 USB ETW 分析器是以网络监视器分析器语言编写的文本文件， (NPL) ，用于描述 USB ETW 事件跟踪的结构。 分析器还会定义 USB 特定的列和筛选器。 这些分析器使 Netmon 成为分析 USB ETW 跟踪的最佳工具。

## <a name="in-this-section"></a>在本节中


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
<td><p><a href="how-to-install-netmon-and-the-netmon-usb-parser.md" data-raw-source="[How to install Netmon and USB ETW Parsers](how-to-install-netmon-and-the-netmon-usb-parser.md)">如何安装 Netmon 和 USB ETW 分析程序</a></p></td>
<td><p>本主题提供有关 Netmon 和 USB ETW 分析器的安装信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-examining-a-trace-file-by-using-netmon.md" data-raw-source="[How to view a USB ETW trace in Netmon](how-to-examining-a-trace-file-by-using-netmon.md)">如何在 Netmon 中查看 USB ETW 跟踪</a></p></td>
<td><p>本主题说明如何使用 Netmon 来举例说明如何使用事件跟踪文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="best-practices--debugging-usb-device-problems.md" data-raw-source="[Debugging USB device issues by using ETW events](best-practices--debugging-usb-device-problems.md)">使用 ETW 事件调试 USB 设备问题</a></p></td>
<td><p>本主题提供使用 ETW 事件调试 USB 设备问题的提示。</p></td>
</tr>
<tr class="even">
<td><p><a href="case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md" data-raw-source="[Case Study: Troubleshooting an unknown USB device by using ETW and Netmon](case-study--troubleshooting-an-unknown-usb-device-by-using-etw-and-netmon.md)">案例研究：使用 ETW 和 Netmon 排查未知 USB 设备的问题</a></p></td>
<td><p>本主题提供有关如何使用 USB ETW 和 Netmon 排查 Windows 无法识别的 USB 设备的示例。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  



