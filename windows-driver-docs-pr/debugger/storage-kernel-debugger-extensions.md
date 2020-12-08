---
title: 存储内核调试程序扩展
description: 存储内核调试器扩展 (storagekd) 用于调试 Windows 8 及更高版本操作系统 (OS) 目标上的存储驱动程序。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 935f99d6a06219a2735134d3868ac51f96e9a07c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786911"
---
# <a name="storage-kernel-debugger-extensions"></a>存储内核调试程序扩展


存储内核调试器扩展 (storagekd) 用于调试 Windows 8 及更高版本操作系统 (OS) 目标上的存储驱动程序。

可在 **Storagekd.dll** 中找到用于调试存储驱动程序的扩展命令（通过 classpnp 托管存储类驱动程序和 Storport 托管存储微型端口驱动程序）。

有关操作系统目标的 Windows 7 和更低版本的调试需求，请参阅 [SCSI 微型端口扩展 ( # A0 和 Minipkd.dll) ](scsi-miniport-extensions--scsikd-dll-and-minipkd-dll-.md) 。

**重要提示**  需要使用特殊符号才能使用此扩展。 有关详细信息，请参阅 [Debugging Tools for Windows](index.md)（Windows 调试工具）。

 

## <a name="span-idstorage_kernel_debugger_extension_commandsspanspan-idstorage_kernel_debugger_extension_commandsspanspan-idstorage_kernel_debugger_extension_commandsspanstorage-kernel-debugger-extension-commands"></a><span id="Storage_kernel_debugger_extension_commands"></span><span id="storage_kernel_debugger_extension_commands"></span><span id="STORAGE_KERNEL_DEBUGGER_EXTENSION_COMMANDS"></span>存储内核调试器扩展命令


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storhelp"></span><span id="_STORAGEKD.STORHELP"></span><strong><a href="-storagekd-storhelp.md" data-raw-source="[!storagekd.storhelp](-storagekd-storhelp.md)">!storagekd.storhelp</a></strong></p></td>
<td align="left"><p>显示 <strong>Storagekd.dll</strong> 扩展命令的帮助文本。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storclass"></span><span id="_STORAGEKD.STORCLASS"></span><strong><a href="-storagekd-storclass.md" data-raw-source="[!storagekd.storclass](-storagekd-storclass.md)">!storagekd.storclass</a></strong></p></td>
<td align="left"><p>显示有关指定 <em>classpnp</em> 设备的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storadapter"></span><span id="_STORAGEKD.STORADAPTER"></span><strong><a href="-storagekd-storadapter.md" data-raw-source="[!storagekd.storadapter](-storagekd-storadapter.md)">!storagekd.storadapter</a></strong></p></td>
<td align="left"><p>显示有关指定的 <em>Storport</em> 适配器的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storunit"></span><span id="_STORAGEKD.STORUNIT"></span><strong><a href="-storagekd-storunit.md" data-raw-source="[!storagekd.storunit](-storagekd-storunit.md)">!storagekd.storunit</a></strong></p></td>
<td align="left"><p>显示指定的 <em>Storport</em> 逻辑单元的相关信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storloglist"></span><span id="_STORAGEKD.STORLOGLIST"></span><strong><a href="-storagekd-storloglist.md" data-raw-source="[!storagekd.storloglist](-storagekd-storloglist.md)">!storagekd.storloglist</a></strong></p></td>
<td align="left"><p>显示 <em>Storport</em> 适配器的内部日志条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storlogirp"></span><span id="_STORAGEKD.STORLOGIRP"></span><strong><a href="-storagekd-storlogirp.md" data-raw-source="[!storagekd.storlogirp](-storagekd-storlogirp.md)">!storagekd.storlogirp</a></strong></p></td>
<td align="left"><p>显示为提供的 IRP 筛选的适配器的 <em>Storport</em> 内部日志条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_storagekd.storlogsrb"></span><span id="_STORAGEKD.STORLOGSRB"></span><strong><a href="-storagekd-storlogsrb.md" data-raw-source="[!storagekd.storlogsrb](-storagekd-storlogsrb.md)">!storagekd.storlogsrb</a></strong></p></td>
<td align="left"><p>显示为存储 (或 SCSI) 请求块筛选的适配器的 <em>Storport</em> 内部日志条目 (提供的 SRB) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_storagekd.storsrb"></span><span id="_STORAGEKD.STORSRB"></span><strong><a href="-storagekd-storsrb.md" data-raw-source="[!storagekd.storsrb](-storagekd-storsrb.md)">!storagekd.storsrb</a></strong></p></td>
<td align="left"><p>显示有关指定的存储 (或 SCSI) 请求块 (SRB) 的信息。</p></td>
</tr>
</tbody>
</table>

 

 

 





