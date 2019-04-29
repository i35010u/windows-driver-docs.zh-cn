---
title: 内核模式环境变量
description: 内核模式环境变量
ms.assetid: 619ebe55-1b57-4182-ada9-0c99c78056b3
keywords:
- 环境变量、 内核模式
- _NT_DEBUG_PORT 环境变量
- _NT_DEBUG_BAUD_RATE environment variable
- KDQUIET 环境变量
- _NT_DEBUG_CACHE_SIZE 环境变量
- _NT_DEBUG_BUS 环境变量
- _NT_DEBUG_1394_CHANNEL 环境变量
- _NT_DEBUG_1394_SYMLINK 环境变量
- _NT_DEBUG_OPTIONS 环境变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e16627de75b81be5d8429ff9f1150df4be288670
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367191"
---
# <a name="kernel-mode-environment-variables"></a>内核模式环境变量


## <span id="ddk_kernel_mode_environment_variables_dbg"></span><span id="DDK_KERNEL_MODE_ENVIRONMENT_VARIABLES_DBG"></span>


下表列出了仅在内核模式调试中使用的环境变量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">变量</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_PORT = <em>ComPort</em></p></td>
<td align="left"><p>指定要在内核连接中使用的 COM 端口。 有关详细信息，请参阅<a href="getting-set-up-for-debugging.md" data-raw-source="[Getting Set Up for Debugging](getting-set-up-for-debugging.md)">获取设置以便进行调试</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_BAUD_RATE = <em>BaudRate</em></p></td>
<td align="left"><p>指定要使用通过 COM 端口连接的波特率。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_BUS = 1394</p></td>
<td align="left"><p>指定将通过 1394年电缆连接进行内核调试。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_1394_CHANNEL = <em>1394Channel</em></p></td>
<td align="left"><p>指定要用于 1394年内核连接的通道。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_1394_SYMLINK = <em>Protocol</em></p></td>
<td align="left"><p>指定要用于 1394年内核连接的连接协议。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KDQUIET =<em>任何内容</em></p></td>
<td align="left"><p>如果定义 KDQUIET，则调试器将在中运行<em>安静模式下</em>。 静默模式都涉及到三个不同的效果：</p>
<p>1. 调试器不显示每次的扩展 DLL 加载或卸载的消息。</p>
<p>2. <strong><a href="r--registers-.md" data-raw-source="[r (Registers)](r--registers-.md)">R （寄存器）</a></strong>命令不再要求其语法中一个等号。</p>
<p>3. 分解为目标计算机时，调试器将不会显示一条警告消息。</p>
<p>安静模式还可通过使用控制<strong><a href="sq--set-quiet-mode-.md" data-raw-source="[sq (Set Quiet Mode)](sq--set-quiet-mode-.md)">sq （设置安静模式下）</a></strong>命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
_NT_DEBUG_CACHE_SIZE= <em>大小</em></td>
<td align="left"><p>指定最大内核调试缓存大小 （字节）。 此缓存保存主机计算机的串行连接从收到的数据。 默认值为 1,024,000。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_OPTIONS = <em>Option</em></p></td>
<td align="left"><p>指定以下两个值之一：</p>
<p>NOEXTWARNING 告知调试程序不要执行时找不到扩展命令输出一条警告。</p>
<p>NOVERSIONCHECK 告知调试器不自动检查调试器扩展的版本。</p>
<p></p>
<p>可以修改这些选项或通过使用显示<strong><a href="so--set-kernel-debugging-options-.md" data-raw-source="[so (Set Kernel Options)](so--set-kernel-debugging-options-.md)">因此 （设置内核选项）</a></strong> 命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_KD_FILES = <em>MapFile</em></p></td>
<td align="left"><p>指定驱动程序替换映射文件。 有关详细信息和控制驱动程序替换的其他方法，请参阅<a href="mapping-driver-files.md" data-raw-source="[Mapping Driver Files](mapping-driver-files.md)">映射驱动程序文件</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





