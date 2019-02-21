---
title: sq （设置安静模式）
description: Sq 命令打开或关闭安静模式。
ms.assetid: db8a266c-e2e5-4de7-8154-993a78585f04
keywords:
- sq （设置安静模式） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sq (Set Quiet Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b4ff1ee435585c99cb0bb2f7df467d2a011b3b07
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544143"
---
# <a name="sq-set-quiet-mode"></a>sq （设置安静模式）


**Sq**命令会启用安静模式下打开或关闭。

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Sqe**命令将启用安静模式，并**sqd**命令会将其关闭。 **Sq**命令，开启和关闭安静模式。 每个命令还会显示新的安静模式状态。

可以在 KD 或内核模式下设置安静模式下使用 KDQUIET WinDbg[环境变量](kernel-mode-environment-variables.md)。 （请注意安静模式存在于用户模式和内核模式调试中，但 KDQUIET 环境变量仅在内核模式中识别。）

*安静模式下*具有三个不同的效果：

-   调试器不显示消息每次加载或卸载扩展 DLL。

-   [ **R （寄存器）** ](r--registers-.md)命令不再需要等号 （=） 其语法中。

-   当您分解为目标计算机的内核调试，长时间时禁止显示警告消息。

不要混淆的安静模式下 **-myob** [命令行选项](command-line-options.md)（在 CDB 和 KD） 或 **-Q** [**命令行选项** ](windbg-command-line-options.md) （在 WinDbg)。

 

 





