---
title: CTRL+A（切换波特率）
description: CTRL + A 键用于切换内核调试连接中使用的波特率。
keywords:
- CTRL + A (切换波特率) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+A (Toggle Baud Rate)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd14d20a9bfb21679d33a0eeda1f8a74166a7ff4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783511"
---
# <a name="ctrla-toggle-baud-rate"></a>CTRL+A（切换波特率）


CTRL + A 键用于切换内核调试连接中使用的波特率。

KD 语法

```dbgcmd
CTRL+A  ENTER 
```

WinDbg 语法

```dbgcmd
CTRL+ALT+A 
```

## <span id="ddk_meta_ctrl_a_dbg"></span><span id="DDK_META_CTRL_A_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>仅限 KD 和 WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

这会遍历内核调试连接的所有可用波特率。

支持的波特速率为19200、38400、57600和115200。 每次使用此控制键时，将选择下一个波特率。 如果波特率已经为115200，则会将其缩减为19200。

在 WinDbg，还可以通过选择 "调试" [|内核连接 |循环波特率](debug---kernel-connection---cycle-baud-rate.md)。

你不能使用此控制键来更改调试时的波特率。 主计算机和目标计算机的波特率必须匹配，并且无法在不重新启动的情况下更改目标计算机的波特率。 因此，如果两台计算机尝试以不同速率通信，则只需通过波特率进行切换。 在这种情况下，必须更改主机计算机的波特率，使其与目标计算机的波特率匹配。

 

 





