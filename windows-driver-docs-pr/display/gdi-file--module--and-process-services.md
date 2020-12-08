---
title: GDI 文件、模块和进程服务
description: GDI 文件、模块和进程服务
keywords:
- GDI WDK Windows 2000 显示，模块服务
- 图形驱动程序 WDK Windows 2000 显示，模块服务
- 绘制 WDK GDI，模块服务
- GDI WDK Windows 2000 显示，文件服务
- 图形驱动程序 WDK Windows 2000 显示，文件服务
- 绘制 WDK GDI，文件服务
- GDI WDK Windows 2000 显示，进程服务
- 图形驱动程序 WDK Windows 2000 显示，进程服务
- 绘制 WDK GDI，处理服务
- 进程服务 WDK GDI
- 文件服务 WDK GDI
- 模块 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10db78a0cb9a98c37b5a55d258c292de5d221b02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836829"
---
# <a name="gdi-file-module-and-process-services"></a>GDI 文件、模块和进程服务


## <span id="ddk_gdi_file_module_and_process_services_gg"></span><span id="DDK_GDI_FILE_MODULE_AND_PROCESS_SERVICES_GG"></span>


GDI 为文件、模块和处理操作提供各种服务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engdeletefile" data-raw-source="[&lt;strong&gt;EngDeleteFile&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engdeletefile)"><strong>EngDeleteFile</strong></a></p></td>
<td align="left"><p>删除文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engfindimageprocaddress" data-raw-source="[&lt;strong&gt;EngFindImageProcAddress&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engfindimageprocaddress)"><strong>EngFindImageProcAddress</strong></a></p></td>
<td align="left"><p>返回可执行模块内的函数的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engfindresource" data-raw-source="[&lt;strong&gt;EngFindResource&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engfindresource)"><strong>EngFindResource</strong></a></p></td>
<td align="left"><p>确定资源在模块中的位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engfreemodule" data-raw-source="[&lt;strong&gt;EngFreeModule&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engfreemodule)"><strong>EngFreeModule</strong></a></p></td>
<td align="left"><p>从系统内存 messagebox 取消文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-enggetcurrentprocessid" data-raw-source="[&lt;strong&gt;EngGetCurrentProcessId&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-enggetcurrentprocessid)"><strong>EngGetCurrentProcessId</strong></a></p></td>
<td align="left"><p>获取当前进程的 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-enggetcurrentthreadid" data-raw-source="[&lt;strong&gt;EngGetCurrentThreadId&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-enggetcurrentthreadid)"><strong>EngGetCurrentThreadId</strong></a></p></td>
<td align="left"><p>获取当前线程的 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-enggetfilechangetime" data-raw-source="[&lt;strong&gt;EngGetFileChangeTime&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-enggetfilechangetime)"><strong>EngGetFileChangeTime</strong></a></p></td>
<td align="left"><p>返回上次写入文件的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-enggetfilepath" data-raw-source="[&lt;strong&gt;EngGetFilePath&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-enggetfilepath)"><strong>EngGetFilePath</strong></a></p></td>
<td align="left"><p>确定与指定的字体文件相关联的文件路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-enggetprocesshandle" data-raw-source="[&lt;strong&gt;EngGetProcessHandle&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-enggetprocesshandle)"><strong>EngGetProcessHandle</strong></a></p></td>
<td align="left"><p>检索当前客户端进程的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engloadimage" data-raw-source="[&lt;strong&gt;EngLoadImage&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engloadimage)"><strong>EngLoadImage</strong></a></p></td>
<td align="left"><p>将指定的可执行映像加载到内核模式内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engloadmodule" data-raw-source="[&lt;strong&gt;EngLoadModule&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engloadmodule)"><strong>EngLoadModule</strong></a></p></td>
<td align="left"><p>将指定的数据模块加载到系统内存中以供读取。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engloadmoduleforwrite" data-raw-source="[&lt;strong&gt;EngLoadModuleForWrite&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engloadmoduleforwrite)"><strong>EngLoadModuleForWrite</strong></a></p></td>
<td align="left"><p>将指定的可执行模块加载到系统内存中以供写入。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engmapfile" data-raw-source="[&lt;strong&gt;EngMapFile&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engmapfile)"><strong>EngMapFile</strong></a></p></td>
<td align="left"><p>创建或打开文件，并将其映射到 <a href="/windows-hardware/drivers/#wdkgloss-system-space" data-raw-source="&lt;em&gt;system space&lt;/em&gt;"><em>系统空间</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engmapfontfile" data-raw-source="[&lt;strong&gt;EngMapFontFile&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engmapfontfile)"><strong>EngMapFontFile</strong></a></p></td>
<td align="left"><p>已过时。 请参阅此表中的 <strong>EngMapFontFileFD</strong>条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engmapfontfilefd" data-raw-source="[&lt;strong&gt;EngMapFontFileFD&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engmapfontfilefd)"><strong>EngMapFontFileFD</strong></a></p></td>
<td align="left"><p>如有必要，将字体文件映射到系统内存，并返回指向文件中字体数据基位置的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engmapmodule" data-raw-source="[&lt;strong&gt;EngMapModule&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engmapmodule)"><strong>EngMapModule</strong></a></p></td>
<td align="left"><p>返回由 <strong>EngLoadModule</strong>加载的可执行文件的地址和大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engqueryfiletimestamp" data-raw-source="[&lt;strong&gt;EngQueryFileTimeStamp&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engqueryfiletimestamp)"><strong>EngQueryFileTimeStamp</strong></a></p></td>
<td align="left"><p>返回文件的时间戳。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunloadimage" data-raw-source="[&lt;strong&gt;EngUnloadImage&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunloadimage)"><strong>EngUnloadImage</strong></a></p></td>
<td align="left"><p>卸载 <strong>EngLoadModule</strong>加载的映像。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunmapfile" data-raw-source="[&lt;strong&gt;EngUnmapFile&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunmapfile)"><strong>EngUnmapFile</strong></a></p></td>
<td align="left"><p>从 <a href="/windows-hardware/drivers/#wdkgloss-system-space" data-raw-source="&lt;em&gt;system space&lt;/em&gt;"><em>系统空间</em></a>messagebox 取消文件的视图。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunmapfontfile" data-raw-source="[&lt;strong&gt;EngUnmapFontFile&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunmapfontfile)"><strong>EngUnmapFontFile</strong></a></p></td>
<td align="left"><p>已过时。 请参阅此表中的 <strong>EngUnmapFontFileFD</strong>条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunmapfontfilefd" data-raw-source="[&lt;strong&gt;EngUnmapFontFileFD&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunmapfontfilefd)"><strong>EngUnmapFontFileFD</strong></a></p></td>
<td align="left"><p>从系统内存中 messagebox 取消指定的字体文件。</p></td>
</tr>
</tbody>
</table>

 

