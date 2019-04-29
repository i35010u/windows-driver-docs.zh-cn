---
title: GDI 文件、模块和进程服务
description: GDI 文件、模块和进程服务
ms.assetid: abf37bed-cad9-4fbc-95fe-346b0c07c81b
keywords:
- GDI WDK Windows 2000 显示，模块服务
- 图形驱动程序 WDK Windows 2000 显示，模块服务
- 绘制 WDK GDI，模块服务
- GDI WDK Windows 2000 显示，文件服务
- 图形驱动程序 WDK Windows 2000 显示，文件服务
- 绘制 WDK GDI，文件服务
- GDI WDK Windows 2000 显示，进程服务
- 图形驱动程序 WDK Windows 2000 显示，请处理服务
- 绘制 WDK GDI，处理服务
- 处理服务 WDK GDI
- 文件服务 WDK GDI
- 模块 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4613424238848cb3955b73f7724cfb17c11d7abe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385650"
---
# <a name="gdi-file-module-and-process-services"></a>GDI 文件、模块和进程服务


## <span id="ddk_gdi_file_module_and_process_services_gg"></span><span id="DDK_GDI_FILE_MODULE_AND_PROCESS_SERVICES_GG"></span>


GDI 提供各种服务以文件、 模块和过程操作。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564803" data-raw-source="[&lt;strong&gt;EngDeleteFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564803)"><strong>EngDeleteFile</strong></a></p></td>
<td align="left"><p>删除的文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564865" data-raw-source="[&lt;strong&gt;EngFindImageProcAddress&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564865)"><strong>EngFindImageProcAddress</strong></a></p></td>
<td align="left"><p>返回一个可执行模块内的某个函数的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564871" data-raw-source="[&lt;strong&gt;EngFindResource&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564871)"><strong>EngFindResource</strong></a></p></td>
<td align="left"><p>确定在模块中的资源的位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564902" data-raw-source="[&lt;strong&gt;EngFreeModule&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564902)"><strong>EngFreeModule</strong></a></p></td>
<td align="left"><p>取消映射系统内存中的文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564919" data-raw-source="[&lt;strong&gt;EngGetCurrentProcessId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564919)"><strong>EngGetCurrentProcessId</strong></a></p></td>
<td align="left"><p>获取当前进程的 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564922" data-raw-source="[&lt;strong&gt;EngGetCurrentThreadId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564922)"><strong>EngGetCurrentThreadId</strong></a></p></td>
<td align="left"><p>获取当前线程的 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564931" data-raw-source="[&lt;strong&gt;EngGetFileChangeTime&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564931)"><strong>EngGetFileChangeTime</strong></a></p></td>
<td align="left"><p>返回上次写入文件的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564935" data-raw-source="[&lt;strong&gt;EngGetFilePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564935)"><strong>EngGetFilePath</strong></a></p></td>
<td align="left"><p>确定与指定的字体文件相关联的文件路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564955" data-raw-source="[&lt;strong&gt;EngGetProcessHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564955)"><strong>EngGetProcessHandle</strong></a></p></td>
<td align="left"><p>检索当前客户端进程的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564963" data-raw-source="[&lt;strong&gt;EngLoadImage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564963)"><strong>EngLoadImage</strong></a></p></td>
<td align="left"><p>将指定的可执行映像加载到内核模式内存中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564964" data-raw-source="[&lt;strong&gt;EngLoadModule&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564964)"><strong>EngLoadModule</strong></a></p></td>
<td align="left"><p>将指定的数据模块加载到系统内存进行读取。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564965" data-raw-source="[&lt;strong&gt;EngLoadModuleForWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564965)"><strong>EngLoadModuleForWrite</strong></a></p></td>
<td align="left"><p>将指定的可执行模块加载到系统内存以进行写入。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564971" data-raw-source="[&lt;strong&gt;EngMapFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564971)"><strong>EngMapFile</strong></a></p></td>
<td align="left"><p>创建或打开文件并将映射到<a href="https://msdn.microsoft.com/library/windows/hardware/ff556336#wdkgloss-system-space" data-raw-source="&lt;em&gt;system space&lt;/em&gt;"><em>系统空间</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564972" data-raw-source="[&lt;strong&gt;EngMapFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564972)"><strong>EngMapFontFile</strong></a></p></td>
<td align="left"><p>已过时。 请参阅此表中的条目<strong>EngMapFontFileFD</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564973" data-raw-source="[&lt;strong&gt;EngMapFontFileFD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564973)"><strong>EngMapFontFileFD</strong></a></p></td>
<td align="left"><p>如有必要，将字体文件映射到系统内存中，并将指针返回到文件中的字体数据的基位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564974" data-raw-source="[&lt;strong&gt;EngMapModule&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564974)"><strong>EngMapModule</strong></a></p></td>
<td align="left"><p>返回的地址和加载的可执行文件的大小<strong>EngLoadModule</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564988" data-raw-source="[&lt;strong&gt;EngQueryFileTimeStamp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564988)"><strong>EngQueryFileTimeStamp</strong></a></p></td>
<td align="left"><p>返回一个文件的时间戳。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565041" data-raw-source="[&lt;strong&gt;EngUnloadImage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565041)"><strong>EngUnloadImage</strong></a></p></td>
<td align="left"><p>卸载映像加载<strong>EngLoadModule</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565437" data-raw-source="[&lt;strong&gt;EngUnmapFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565437)"><strong>EngUnmapFile</strong></a></p></td>
<td align="left"><p>取消映射中的文件的视图<a href="https://msdn.microsoft.com/library/windows/hardware/ff556336#wdkgloss-system-space" data-raw-source="&lt;em&gt;system space&lt;/em&gt;"><em>系统空间</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565441" data-raw-source="[&lt;strong&gt;EngUnmapFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565441)"><strong>EngUnmapFontFile</strong></a></p></td>
<td align="left"><p>已过时。 请参阅此表中的条目<strong>EngUnmapFontFileFD</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565445" data-raw-source="[&lt;strong&gt;EngUnmapFontFileFD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565445)"><strong>EngUnmapFontFileFD</strong></a></p></td>
<td align="left"><p>取消映射系统内存中的指定的字体文件。</p></td>
</tr>
</tbody>
</table>

 

 

 





