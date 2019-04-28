---
title: 蓝牙扩展 (Bthkd.dll)
description: 蓝牙调试器扩展插件在目标系统上会显示有关当前蓝牙环境的信息。
ms.assetid: F6C5295D-F1F9-4180-BE57-A7D47AC8690C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4614b6d713ce2fa49b094f15e2555f41ec076046
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347887"
---
# <a name="bluetooth-extensions-bthkddll"></a>蓝牙扩展 (Bthkd.dll)


蓝牙调试器扩展插件在目标系统上会显示有关当前蓝牙环境的信息。

**请注意**  以使用调试扩展的蓝牙，您可能会遇到未记录的行为或 Api。 我们强烈建议不要采用依赖项未记录的行为或 Api 受制于原样未来版本中更改。

 

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
<td align="left"><p><strong><a href="-bthkd-bthdevinfo.md" data-raw-source="[!bthkd.bthdevinfo](-bthkd-bthdevinfo.md)">!bthkd.bthdevinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthdevinfo.md" data-raw-source="[!bthkd.bthdevinfo](-bthkd-bthdevinfo.md)">！ Bthkd.bthdevinfo</a></strong>命令显示有关给定 BTHENUM 创建设备 PDO 的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthenuminfo.md" data-raw-source="[!bthkd.bthenuminfo](-bthkd-bthenuminfo.md)">!bthkd.bthenuminfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthenuminfo.md" data-raw-source="[!bthkd.bthenuminfo](-bthkd-bthenuminfo.md)">！ Bthkd.bthenuminfo</a></strong>命令显示有关 BTHENUM FDO 信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-bthinfo-.md" data-raw-source="[!bthkd.bthinfo](-bthkd-bthinfo-.md)">!bthkd.bthinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthinfo-.md" data-raw-source="[!bthkd.bthinfo](-bthkd-bthinfo-.md)">！ Bthkd.bthinfo</a></strong>命令显示有关 BTHPORT FDO 的详细信息。 此命令是蓝牙调查的良好起点，因为它显示可用于访问的许多其他蓝牙调试扩展命令的地址信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthhelp.md" data-raw-source="[!bthkd.bthhelp](-bthkd-bthhelp.md)">!bthkd.bthhelp</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthhelp.md" data-raw-source="[!bthkd.bthhelp](-bthkd-bthhelp.md)">！ Bthkd.bthhelp</a></strong>命令显示蓝牙调试扩展命令的帮助。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-bthtree.md" data-raw-source="[!bthkd.bthtree](-bthkd-bthtree.md)">!bthkd.bthtree</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthtree.md" data-raw-source="[!bthkd.bthtree](-bthkd-bthtree.md)">！ Bthkd.bthtree</a></strong>命令将显示完整的蓝牙设备树。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthusbtransfer.md" data-raw-source="[!bthkd.bthusbtransfer](-bthkd-bthusbtransfer.md)">!bthkd.bthusbtransfer</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthusbtransfer.md" data-raw-source="[!bthkd.bthusbtransfer](-bthkd-bthusbtransfer.md)">！ Bthkd.bthusbtransfer</a></strong>命令显示蓝牙 usb 传输上下文包括 Irp、 Bip 和传输缓冲区信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-dibflags.md" data-raw-source="[!bthkd.dibflags](-bthkd-dibflags.md)">!bthkd.dibflags</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-dibflags.md" data-raw-source="[!bthkd.dibflags](-bthkd-dibflags.md)">！ Bthkd.dibflags</a></strong>命令显示 DEVICE_INFO_BLOCK。DibFlags 转储 _DEVICE_INFO_BLOCK 中的标志集。DibFlags。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-hcicmd.md" data-raw-source="[!bthkd.hcicmd](-bthkd-hcicmd.md)">!bthkd.hcicmd</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-hcicmd.md" data-raw-source="[!bthkd.hcicmd](-bthkd-hcicmd.md)">！ Bthkd.hcicmd</a></strong>命令显示当前处于挂起状态的命令的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-hciinterface.md" data-raw-source="[!bthkd.hciinterface](-bthkd-hciinterface.md)">!bthkd.hciinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-hciinterface.md" data-raw-source="[!bthkd.hciinterface](-bthkd-hciinterface.md)">！ Bthkd.hciinterface</a></strong>命令显示 bthport ！ _HCI_INTERFACE 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-l2capinterface-.md" data-raw-source="[!bthkd.l2capinterface](-bthkd-l2capinterface-.md)">！ bthkd.l2capinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-l2capinterface-.md" data-raw-source="[!bthkd.l2capinterface](-bthkd-l2capinterface-.md)">！ Bthkd.l2capinterface</a></strong>命令显示有关 L2CAP 接口的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-rfcomminfo.md" data-raw-source="[!bthkd.rfcomminfo](-bthkd-rfcomminfo.md)">!bthkd.rfcomminfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcomminfo.md" data-raw-source="[!bthkd.rfcomminfo](-bthkd-rfcomminfo.md)">！ Bthkd.rfcomminfo</a></strong>命令显示有关 RFCOMM FDO 和 TDI 设备对象的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-rfcommconnection.md" data-raw-source="[!bthkd.rfcommconnection](-bthkd-rfcommconnection.md)">!bthkd.rfcommconnection</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcommconnection.md" data-raw-source="[!bthkd.rfcommconnection](-bthkd-rfcommconnection.md)">！ Bthkd.rfcommconnection</a></strong>命令显示有关给定 RFCOMM 连接对象的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-rfcommchannel.md" data-raw-source="[!bthkd.rfcommchannel](-bthkd-rfcommchannel.md)">!bthkd.rfcommchannel</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcommchannel.md" data-raw-source="[!bthkd.rfcommchannel](-bthkd-rfcommchannel.md)">！ Bthkd.rfcommchannel</a></strong>命令显示有关给定 RFCOMM 通道 CB 的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-sdpinterface.md" data-raw-source="[!bthkd.sdpinterface](-bthkd-sdpinterface.md)">!bthkd.sdpinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpinterface.md" data-raw-source="[!bthkd.sdpinterface](-bthkd-sdpinterface.md)">！ Bthkd.sdpinterface</a></strong>命令显示有关 SDP 接口的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-scointerface-.md" data-raw-source="[!bthkd.scointerface](-bthkd-scointerface-.md)">!bthkd.scointerface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-scointerface-.md" data-raw-source="[!bthkd.scointerface](-bthkd-scointerface-.md)">！ Bthkd.scointerface</a></strong>命令显示有关 SCO 接口的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-sdpnode.md" data-raw-source="[!bthkd.sdpnode](-bthkd-sdpnode.md)">!bthkd.sdpnode</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpnode.md" data-raw-source="[!bthkd.sdpnode](-bthkd-sdpnode.md)">！ Bthkd.sdpnode</a></strong> sdp 树中的命令显示有关节点的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-sdpstream.md" data-raw-source="[!bthkd.sdpstream](-bthkd-sdpstream.md)">!bthkd.sdpstream</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpstream.md" data-raw-source="[!bthkd.sdpstream](-bthkd-sdpstream.md)">！ Bthkd.sdpstream</a></strong>命令显示 SDP 流的内容。</p></td>
</tr>
</tbody>
</table>

 

 

 





