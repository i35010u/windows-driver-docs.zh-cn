---
title: sq（设置安静模式）
description: Sq 命令打开或关闭安静模式。
keywords:
- sq (设置静默模式) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sq (Set Quiet Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef68db2e872047da581fd623da973cbac46ff0c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817483"
---
# <a name="sq-set-quiet-mode"></a>sq（设置安静模式）


**Sq** 命令打开或关闭安静模式。

```dbgcmd
sq 
sq{e|d} 
```

## <span id="ddk_cmd_set_quiet_mode_dbg"></span><span id="DDK_CMD_SET_QUIET_MODE_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Sqe** 命令打开安静模式， **sqd** 命令将其关闭。 **Sq** 命令打开和关闭静默模式。 其中每个命令还显示新的安静模式状态。

可以通过使用 KDQUIET [环境变量](kernel-mode-environment-variables.md)，在 KD 或内核模式 WinDbg 中设置静默模式。  (请注意，在用户模式和内核模式调试中同时存在静默模式，但仅在内核模式下识别 KDQUIET 环境变量。 ) 

*安静模式* 有三个不同的效果：

-   每次加载或卸载扩展 DLL 时，调试器都不显示消息。

-   [**R (寄存器)**](r--registers-.md)命令不再需要在其语法中使用等号 (=) 。

-   当你在内核调试时进入目标计算机时，将抑制长警告消息。

不要将静默模式与 **-myob** [命令行选项](command-line-options.md) (在 CDB 和 KD) 中的效果或在 WinDbg) 中 (**-Q** [**命令行选项**](windbg-command-line-options.md) 混淆。

 

 





