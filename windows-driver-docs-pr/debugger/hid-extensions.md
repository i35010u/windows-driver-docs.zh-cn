---
title: HID 扩展
description: 本部分介绍 (HID) 调试器扩展命令中的人机接口设备。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7fdf25fe2e649187870ec2f358b2b4b58e62478
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806563"
---
# <a name="hid-extensions"></a>HID 扩展


本部分介绍 (HID) 调试器扩展命令中的人机接口设备。

HID 调试器扩展命令在 Hidkd.dll 中实现。 若要加载 HID 命令，请在调试器中输入 **. load hidkd.dll** 。

## <a name="span-idgetting_started_with_the_hid_extensions_spanspan-idgetting_started_with_the_hid_extensions_spanspan-idgetting_started_with_the_hid_extensions_spangetting-started-with-the-hid-extensions"></a><span id="Getting_started_with_the_HID_extensions_"></span><span id="getting_started_with_the_hid_extensions_"></span><span id="GETTING_STARTED_WITH_THE_HID_EXTENSIONS_"></span>HID 扩展入门


若要开始调试 HID 问题，请输入 [**！ hidtree**](-hidkd-hidtree.md) 命令。 **！ Hidtree** 命令显示可用于调查设备对象、preparsed HID 数据和 HID 报表描述符的命令和地址列表。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p><strong><a href="-hidkd-help.md" data-raw-source="[!hidkd.help](-hidkd-help.md)">！ Hidkd</a></strong>命令显示 HID 调试器扩展命令的帮助。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidfdo.md" data-raw-source="[!hidkd.hidfdo](-hidkd-hidfdo.md)">!hidkd.hidfdo</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidfdo.md" data-raw-source="[!hidkd.hidfdo](-hidkd-hidfdo.md)">！ Hidkd hidfdo</a></strong>命令显示与功能设备对象相关联 (FDO) 的 HID 信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-hidkd-hidpdo.md" data-raw-source="[!hidkd.hidpdo](-hidkd-hidpdo.md)">!hidkd.hidpdo</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidpdo.md" data-raw-source="[!hidkd.hidpdo](-hidkd-hidpdo.md)">！ Hidkd hidpdo</a></strong>命令显示与 (PDO) 的物理设备对象相关联的 HID 信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidtree.md" data-raw-source="[!hidkd.hidtree](-hidkd-hidtree.md)">!hidkd.hidtree</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidtree.md" data-raw-source="[!hidkd.hidtree](-hidkd-hidtree.md)">！ Hidkd. hidtree</a></strong>命令显示具有 HID 函数驱动程序及其子节点的所有设备节点的列表。 子节点的物理设备对象 (PDO) 由父节点的 HID 函数驱动程序创建。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-hidkd-hidppd.md" data-raw-source="[!hidkd.hidppd](-hidkd-hidppd.md)">!hidkd.hidppd</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidppd.md" data-raw-source="[!hidkd.hidppd](-hidkd-hidppd.md)">！ Hidkd. hidppd</a></strong>命令显示 HID preparsed 数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidrd.md" data-raw-source="[!hidkd.hidrd](-hidkd-hidrd.md)">!hidkd.hidrd</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidrd.md" data-raw-source="[!hidkd.hidrd](-hidkd-hidrd.md)">！ Hidkd. hidrd</a></strong>命令以原始格式和已分析格式显示 HID 报表说明符。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[RCDRKD 扩展](rcdrkd-extensions.md)

[专业扩展命令](specialized-extensions.md)

 

 






