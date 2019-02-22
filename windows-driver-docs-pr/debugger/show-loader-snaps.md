---
title: 显示加载程序的快照
description: 显示加载程序的快照
ms.assetid: fb3843fe-451f-444c-a690-862253df944e
keywords:
- 显示加载程序对齐 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 565841af185edf5ca38827643f8f3820a04354df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520309"
---
# <a name="show-loader-snaps"></a>显示加载程序的快照


## <span id="ddk_show_loader_snaps_dtools"></span><span id="DDK_SHOW_LOADER_SNAPS_DTOOLS"></span>


**显示加载程序快照**标志捕获有关加载和卸载的可执行映像和其支持的库模块的详细的信息和内核调试程序控制台中显示的数据。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>sls</p></td>
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
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

对于系统范围内 （注册表或内核标志），此标志显示驱动程序加载和卸载操作的信息。

对于每个进程 （图像文件），此标志显示有关加载和卸载的 Dll 的信息。

 

 





