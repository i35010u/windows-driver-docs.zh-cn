---
title: CTRL+A（切换波特率）
description: CTRL + A 键用于切换在内核调试连接中使用的波特率。
ms.assetid: 77a95ca1-073c-480a-abda-f484adbc1d23
keywords:
- CTRL + A （切换波特率） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+A (Toggle Baud Rate)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d31a1e41d2efe29af5f2feb2f73ad88605250b9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375418"
---
# <a name="ctrla-toggle-baud-rate"></a>CTRL+A（切换波特率）


CTRL + A 键用于切换在内核调试连接中使用的波特率。

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
<td align="left"><p>KD 和 WinDbg 仅</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

这将遍历的内核调试连接的所有可用波特率。

受支持的波特率有 19200、 38400、 57600 和 115200。 每次使用此控制密钥时，将选择下一步的波特率。 如果波特率已经以 115200 的速率，会将其减少到 19200。

在 WinDbg 中，还可以通过选择[调试 |内核连接 |周期波特率](debug---kernel-connection---cycle-baud-rate.md)。

此控制密钥实际上不能用于更改在其中进行调试的波特率。 在主计算机和目标计算机的波特率必须匹配，并且目标计算机的波特率不能更改而无需重新启动。 因此，只需通过的波特率切换，如果两台计算机尝试以不同速率进行通信。 在这种情况下，必须更改主计算机的波特率以匹配的目标计算机。

 

 





