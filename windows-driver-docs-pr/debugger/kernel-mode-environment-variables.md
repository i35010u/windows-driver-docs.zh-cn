---
title: 内核模式环境变量
description: 内核模式环境变量
keywords:
- 环境变量，内核模式
- _NT_DEBUG_PORT 环境变量
- _NT_DEBUG_BAUD_RATE 环境变量
- KDQUIET 环境变量
- _NT_DEBUG_CACHE_SIZE 环境变量
- _NT_DEBUG_BUS 环境变量
- _NT_DEBUG_1394_CHANNEL 环境变量
- _NT_DEBUG_1394_SYMLINK 环境变量
- _NT_DEBUG_OPTIONS 环境变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d139a4a9bf99c8bca3f09b1026773e8d85341732
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840835"
---
# <a name="kernel-mode-environment-variables"></a>内核模式环境变量


## <span id="ddk_kernel_mode_environment_variables_dbg"></span><span id="DDK_KERNEL_MODE_ENVIRONMENT_VARIABLES_DBG"></span>


下表列出了仅用于内核模式调试的环境变量。

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
<td align="left"><p>指定要在内核连接中使用的 COM 端口。 有关详细信息，请参阅 <a href="getting-set-up-for-debugging.md" data-raw-source="[Getting Set Up for Debugging](getting-set-up-for-debugging.md)">获取调试设置</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_BAUD_RATE = <em>波特率</em></p></td>
<td align="left"><p>指定用于 COM 端口连接的波特率。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_BUS = 1394</p></td>
<td align="left"><p>指定将通过1394电缆连接完成内核调试。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_1394_CHANNEL = <em>1394Channel</em></p></td>
<td align="left"><p>指定要用于1394内核连接的通道。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_DEBUG_1394_SYMLINK = <em>协议</em></p></td>
<td align="left"><p>指定用于1394内核连接的连接协议。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KDQUIET =<em>任何</em></p></td>
<td align="left"><p>如果定义了 KDQUIET，则调试器将在 <em>安静模式下</em>运行。 安静模式涉及三个不同的效果：</p>
<p>1. 每次加载或卸载扩展 DLL 时，调试器都不显示消息。</p>
<p>2.<strong><a href="r--registers-.md" data-raw-source="[r (Registers)](r--registers-.md)">R (注册) </a></strong>命令不再要求其语法使用等号。</p>
<p>3. 当打断目标计算机时，调试器不会显示警告消息。</p>
<p>还可以使用 <strong><a href="sq--set-quiet-mode-.md" data-raw-source="[sq (Set Quiet Mode)](sq--set-quiet-mode-.md)">sq (设置静默模式) </a></strong> 命令控制静默模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
_NT_DEBUG_CACHE_SIZE = <em>大小</em></td>
<td align="left"><p>指定最大内核调试缓存大小（以字节为单位）。 此缓存保存主机从串行连接接收的数据。 默认值为1024000。</p></td>
</tr>
<tr class="even">
<td align="left"><p>_NT_DEBUG_OPTIONS = <em>选项</em></p></td>
<td align="left"><p>指定以下两个值之一：</p>
<p>NOEXTWARNING 通知调试器当找不到扩展命令时不输出警告。</p>
<p>NOVERSIONCHECK 通知调试器不要检查调试器扩展的版本。</p>
<p></p>
<p>可以通过使用 <strong><a href="so--set-kernel-debugging-options-.md" data-raw-source="[so (Set Kernel Options)](so--set-kernel-debugging-options-.md)"> (Set Kernel options) </a></strong> 命令来修改或显示这些选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>_NT_KD_FILES = <em>映射</em></p></td>
<td align="left"><p>指定驱动程序替换映射文件。 有关详细信息和控制驱动程序替换的其他方法，请参阅 <a href="mapping-driver-files.md" data-raw-source="[Mapping Driver Files](mapping-driver-files.md)">映射驱动程序文件</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





