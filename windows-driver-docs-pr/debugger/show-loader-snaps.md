---
title: 显示加载器快照
description: 显示加载器快照
keywords:
- '显示加载器 (全局标志的快照) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d12795b6666e917111c4cb284c72a8d4cc39f11d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836863"
---
# <a name="show-loader-snaps"></a>显示加载器快照


## <span id="ddk_show_loader_snaps_dtools"></span><span id="DDK_SHOW_LOADER_SNAPS_DTOOLS"></span>


**显示加载程序的 snap** 标记捕获有关加载和卸载可执行映像及其支持的库模块的详细信息，并在内核调试器控制台中显示数据。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>购买</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_SHOW_LDR_SNAPS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

对于系统范围 (注册表或内核标记) ，此标志显示有关驱动程序加载和卸载操作的信息。

对于每个进程 (映像文件) ，此标志显示有关加载和卸载 Dll 的信息。

 

 





