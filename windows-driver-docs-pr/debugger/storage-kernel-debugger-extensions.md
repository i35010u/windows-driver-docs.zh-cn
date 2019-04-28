---
title: 存储内核调试程序扩展
description: 存储内核调试器扩展 (storagekd) 用于调试在 Windows 8 及更高版本操作系统 (OS) 目标的存储驱动程序。
ms.assetid: 8EF83BC8-6ABB-496C-98A6-EF0298D78F76
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fe9018af0a2906d22c742a78b249d5a4ba8a0ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335516"
---
# <a name="storage-kernel-debugger-extensions"></a>存储内核调试程序扩展


存储内核调试器扩展 (storagekd) 用于调试在 Windows 8 及更高版本操作系统 (OS) 目标的存储驱动程序。

扩展命令，可用于调试存储驱动程序，通过托管 classpnp 会存储类驱动程序和托管 Storport 存储微型端口驱动程序，可在**Storagekd.dll**。

请参阅[SCSI 微型端口扩展 （Scsikd.dll 和 Minipkd.dll）](scsi-miniport-extensions--scsikd-dll-and-minipkd-dll-.md)调试需求适用于 Windows 7 和低于的操作系统的目标版本。

**重要**  需要使用此扩展的特殊符号。 有关详细信息，请参阅[有关 Windows 调试工具](index.md)。

 

## <a name="span-idstoragekerneldebuggerextensioncommandsspanspan-idstoragekerneldebuggerextensioncommandsspanspan-idstoragekerneldebuggerextensioncommandsspanstorage-kernel-debugger-extension-commands"></a><span id="Storage_kernel_debugger_extension_commands"></span><span id="storage_kernel_debugger_extension_commands"></span><span id="STORAGE_KERNEL_DEBUGGER_EXTENSION_COMMANDS"></span>存储内核调试器扩展命令


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storhelp"></span><span id="_STORAGEKD.STORHELP"></span><strong><a href="-storagekd-storhelp.md" data-raw-source="[!storagekd.storhelp](-storagekd-storhelp.md)">!storagekd.storhelp</a></strong></p></td>
<td align="left"><p>显示的帮助文字<strong>Storagekd.dll</strong>扩展命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storclass"></span><span id="_STORAGEKD.STORCLASS"></span><strong><a href="-storagekd-storclass.md" data-raw-source="[!storagekd.storclass](-storagekd-storclass.md)">!storagekd.storclass</a></strong></p></td>
<td align="left"><p>显示有关指定的信息<em>classpnp 会</em>设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storadapter"></span><span id="_STORAGEKD.STORADAPTER"></span><strong><a href="-storagekd-storadapter.md" data-raw-source="[!storagekd.storadapter](-storagekd-storadapter.md)">!storagekd.storadapter</a></strong></p></td>
<td align="left"><p>显示有关指定的信息<em>Storport</em>适配器。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storunit"></span><span id="_STORAGEKD.STORUNIT"></span><strong><a href="-storagekd-storunit.md" data-raw-source="[!storagekd.storunit](-storagekd-storunit.md)">!storagekd.storunit</a></strong></p></td>
<td align="left"><p>显示有关指定的信息<em>Storport</em>逻辑单元。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storloglist"></span><span id="_STORAGEKD.STORLOGLIST"></span><strong><a href="-storagekd-storloglist.md" data-raw-source="[!storagekd.storloglist](-storagekd-storloglist.md)">!storagekd.storloglist</a></strong></p></td>
<td align="left"><p>显示<em>Storport</em>适配器的内部日志条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storlogirp"></span><span id="_STORAGEKD.STORLOGIRP"></span><strong><a href="-storagekd-storlogirp.md" data-raw-source="[!storagekd.storlogirp](-storagekd-storlogirp.md)">!storagekd.storlogirp</a></strong></p></td>
<td align="left"><p>显示<em>Storport 的</em>筛选出的适配器的内部日志条目的 IRP 提供。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storlogsrb"></span><span id="_STORAGEKD.STORLOGSRB"></span><strong><a href="-storagekd-storlogsrb.md" data-raw-source="[!storagekd.storlogsrb](-storagekd-storlogsrb.md)">!storagekd.storlogsrb</a></strong></p></td>
<td align="left"><p>显示<em>Storport 的</em>适配器内部日志条目筛选，存储 （或 SCSI） 请求块 (SRB) 提供。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storsrb"></span><span id="_STORAGEKD.STORSRB"></span><strong><a href="-storagekd-storsrb.md" data-raw-source="[!storagekd.storsrb](-storagekd-storsrb.md)">!storagekd.storsrb</a></strong></p></td>
<td align="left"><p>显示有关指定的存储 （或 SCSI） 的信息请求块 (SRB)。</p></td>
</tr>
</tbody>
</table>

 

 

 





