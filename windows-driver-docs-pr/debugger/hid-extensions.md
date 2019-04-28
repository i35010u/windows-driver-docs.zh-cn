---
title: HID 扩展
description: 本部分介绍人体学接口设备 (HID) 调试器扩展命令。
ms.assetid: 796DB87B-1E04-40FA-90F9-699EE7032B3C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60eee0bf524d43a6c5ee68dd7bc427fe916709b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342449"
---
# <a name="hid-extensions"></a>HID 扩展


本部分介绍人体学接口设备 (HID) 调试器扩展命令。

HID 调试器扩展命令中 Hidkd.dll 实现。 若要加载的 HID 命令，请输入 **.load hidkd.dll**在调试器中。

## <a name="span-idgettingstartedwiththehidextensionsspanspan-idgettingstartedwiththehidextensionsspanspan-idgettingstartedwiththehidextensionsspangetting-started-with-the-hid-extensions"></a><span id="Getting_started_with_the_HID_extensions_"></span><span id="getting_started_with_the_hid_extensions_"></span><span id="GETTING_STARTED_WITH_THE_HID_EXTENSIONS_"></span>HID 扩展入门


若要开始调试 HID 问题，请输入[ **！ hidtree** ](-hidkd-hidtree.md)命令。 **！ Hidtree**命令显示的命令的列表以及可用于调查 preparsed 的设备对象的地址 HID 数据，并 HID 报告描述符。

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
<td align="left"><p><strong><a href="-hidkd-help.md" data-raw-source="[!hidkd.help](-hidkd-help.md)">!hidkd.help</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-help.md" data-raw-source="[!hidkd.help](-hidkd-help.md)">！ Hidkd.help</a></strong>命令显示 HID 调试器扩展命令的帮助。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidfdo.md" data-raw-source="[!hidkd.hidfdo](-hidkd-hidfdo.md)">!hidkd.hidfdo</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidfdo.md" data-raw-source="[!hidkd.hidfdo](-hidkd-hidfdo.md)">！ Hidkd.hidfdo</a></strong>命令显示 HID 信息与功能的设备对象 (FDO) 相关联。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-hidkd-hidpdo.md" data-raw-source="[!hidkd.hidpdo](-hidkd-hidpdo.md)">!hidkd.hidpdo</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidpdo.md" data-raw-source="[!hidkd.hidpdo](-hidkd-hidpdo.md)">！ Hidkd.hidpdo</a></strong>命令将显示与物理设备对象 (PDO) 相关联的 HID 信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidtree.md" data-raw-source="[!hidkd.hidtree](-hidkd-hidtree.md)">!hidkd.hidtree</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidtree.md" data-raw-source="[!hidkd.hidtree](-hidkd-hidtree.md)">！ Hidkd.hidtree</a></strong>命令显示所有已以及及其子节点的 HID 函数驱动程序的设备节点的列表。 子节点有一个物理设备对象 (PDO) 创建的父节点的 HID 功能驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-hidkd-hidppd.md" data-raw-source="[!hidkd.hidppd](-hidkd-hidppd.md)">!hidkd.hidppd</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidppd.md" data-raw-source="[!hidkd.hidppd](-hidkd-hidppd.md)">！ Hidkd.hidppd</a></strong>命令显示 HID preparsed 数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidrd.md" data-raw-source="[!hidkd.hidrd](-hidkd-hidrd.md)">!hidkd.hidrd</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidrd.md" data-raw-source="[!hidkd.hidrd](-hidkd-hidrd.md)">！ Hidkd.hidrd</a></strong>命令显示 HID 报表描述符中原始和已分析格式。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[RCDRKD 扩展](rcdrkd-extensions.md)

[专用的扩展命令](specialized-extensions.md)

 

 






