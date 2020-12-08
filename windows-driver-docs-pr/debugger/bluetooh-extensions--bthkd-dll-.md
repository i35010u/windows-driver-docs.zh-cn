---
title: 蓝牙扩展 (Bthkd.dll)
description: 蓝牙调试器扩展显示有关目标系统上当前蓝牙环境的信息。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d626d1f636c81ca24a76c1620e96f3925ece9b2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805771"
---
# <a name="bluetooth-extensions-bthkddll"></a>蓝牙扩展 (Bthkd.dll)


蓝牙调试器扩展显示有关目标系统上当前蓝牙环境的信息。

**注意**  使用蓝牙调试扩展时，可能会遇到未记录的行为或 Api。 我们强烈建议不要依赖于未记录的行为或 Api，因为在将来的版本中可能会发生更改。

 

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
<td align="left"><p><strong><a href="-bthkd-bthdevinfo.md" data-raw-source="[!bthkd.bthdevinfo](-bthkd-bthdevinfo.md)">!bthkd.bthdevinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthdevinfo.md" data-raw-source="[!bthkd.bthdevinfo](-bthkd-bthdevinfo.md)">！ Bthkd. bthdevinfo</a></strong>命令显示有关给定 BTHENUM 创建的设备 PDO 的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthenuminfo.md" data-raw-source="[!bthkd.bthenuminfo](-bthkd-bthenuminfo.md)">!bthkd.bthenuminfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthenuminfo.md" data-raw-source="[!bthkd.bthenuminfo](-bthkd-bthenuminfo.md)">！ Bthkd. bthenuminfo</a></strong>命令显示有关 BTHENUM FDO 的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-bthinfo-.md" data-raw-source="[!bthkd.bthinfo](-bthkd-bthinfo-.md)">!bthkd.bthinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthinfo-.md" data-raw-source="[!bthkd.bthinfo](-bthkd-bthinfo-.md)">！ Bthkd. bthinfo</a></strong>命令显示有关 BTHPORT FDO 的详细信息。 此命令是一种很好的蓝牙调查开始点，因为它显示可用于访问其他许多蓝牙调试扩展命令的地址信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthhelp.md" data-raw-source="[!bthkd.bthhelp](-bthkd-bthhelp.md)">!bthkd.bthhelp</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthhelp.md" data-raw-source="[!bthkd.bthhelp](-bthkd-bthhelp.md)">！ Bthkd. bthhelp</a></strong>命令显示有关蓝牙调试扩展命令的帮助。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-bthtree.md" data-raw-source="[!bthkd.bthtree](-bthkd-bthtree.md)">!bthkd.bthtree</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthtree.md" data-raw-source="[!bthkd.bthtree](-bthkd-bthtree.md)">！ Bthkd. bthtree</a></strong>命令显示完整的蓝牙设备树。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-bthusbtransfer.md" data-raw-source="[!bthkd.bthusbtransfer](-bthkd-bthusbtransfer.md)">!bthkd.bthusbtransfer</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-bthusbtransfer.md" data-raw-source="[!bthkd.bthusbtransfer](-bthkd-bthusbtransfer.md)">！ Bthkd. bthusbtransfer</a></strong>命令显示蓝牙 usb 传输上下文，包括 Irp、Bip 和传输缓冲区信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-dibflags.md" data-raw-source="[!bthkd.dibflags](-bthkd-dibflags.md)">!bthkd.dibflags</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-dibflags.md" data-raw-source="[!bthkd.dibflags](-bthkd-dibflags.md)">！ Bthkd. dibflags</a></strong>命令显示 DEVICE_INFO_BLOCK。DibFlags 转储 _DEVICE_INFO_BLOCK 中设置的标志。DibFlags.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-hcicmd.md" data-raw-source="[!bthkd.hcicmd](-bthkd-hcicmd.md)">!bthkd.hcicmd</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-hcicmd.md" data-raw-source="[!bthkd.hcicmd](-bthkd-hcicmd.md)">！ Bthkd. hcicmd</a></strong>命令显示当前挂起的命令的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-hciinterface.md" data-raw-source="[!bthkd.hciinterface](-bthkd-hciinterface.md)">!bthkd.hciinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-hciinterface.md" data-raw-source="[!bthkd.hciinterface](-bthkd-hciinterface.md)">！ Bthkd. hciinterface</a></strong>命令显示 bthport！ _HCI_INTERFACE 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-l2capinterface-.md" data-raw-source="[!bthkd.l2capinterface](-bthkd-l2capinterface-.md)">!bthkd.l2capinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-l2capinterface-.md" data-raw-source="[!bthkd.l2capinterface](-bthkd-l2capinterface-.md)">！ Bthkd. l2capinterface</a></strong>命令显示有关 L2CAP 接口的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-rfcomminfo.md" data-raw-source="[!bthkd.rfcomminfo](-bthkd-rfcomminfo.md)">!bthkd.rfcomminfo</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcomminfo.md" data-raw-source="[!bthkd.rfcomminfo](-bthkd-rfcomminfo.md)">！ Bthkd. rfcomminfo</a></strong>命令显示有关 RFCOMM FDO 和 TDI 设备对象的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-rfcommconnection.md" data-raw-source="[!bthkd.rfcommconnection](-bthkd-rfcommconnection.md)">!bthkd.rfcommconnection</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcommconnection.md" data-raw-source="[!bthkd.rfcommconnection](-bthkd-rfcommconnection.md)">！ Bthkd. rfcommconnection</a></strong>命令显示有关给定 RFCOMM 连接对象的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-rfcommchannel.md" data-raw-source="[!bthkd.rfcommchannel](-bthkd-rfcommchannel.md)">!bthkd.rfcommchannel</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-rfcommchannel.md" data-raw-source="[!bthkd.rfcommchannel](-bthkd-rfcommchannel.md)">！ Bthkd. rfcommchannel</a></strong>命令显示有关给定 RFCOMM 通道 CB 的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-sdpinterface.md" data-raw-source="[!bthkd.sdpinterface](-bthkd-sdpinterface.md)">!bthkd.sdpinterface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpinterface.md" data-raw-source="[!bthkd.sdpinterface](-bthkd-sdpinterface.md)">！ Bthkd. sdpinterface</a></strong>命令显示有关 SDP 接口的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-scointerface-.md" data-raw-source="[!bthkd.scointerface](-bthkd-scointerface-.md)">!bthkd.scointerface</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-scointerface-.md" data-raw-source="[!bthkd.scointerface](-bthkd-scointerface-.md)">！ Bthkd. scointerface</a></strong>命令显示有关 SCO 接口的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-bthkd-sdpnode.md" data-raw-source="[!bthkd.sdpnode](-bthkd-sdpnode.md)">!bthkd.sdpnode</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpnode.md" data-raw-source="[!bthkd.sdpnode](-bthkd-sdpnode.md)">！ Bthkd. sdpnode</a></strong>命令显示有关 sdp 树中的节点的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-bthkd-sdpstream.md" data-raw-source="[!bthkd.sdpstream](-bthkd-sdpstream.md)">!bthkd.sdpstream</a></strong></p></td>
<td align="left"><p><strong><a href="-bthkd-sdpstream.md" data-raw-source="[!bthkd.sdpstream](-bthkd-sdpstream.md)">！ Bthkd. sdpstream</a></strong>命令显示 SDP 流的内容。</p></td>
</tr>
</tbody>
</table>

 

 

 





