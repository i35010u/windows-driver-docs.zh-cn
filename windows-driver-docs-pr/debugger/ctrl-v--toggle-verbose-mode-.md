---
title: CTRL+V（切换详细模式）
description: CTRL + V 键用于打开和关闭详细模式。
keywords:
- CTRL + V (切换详细模式) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+V (Toggle Verbose Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 68146fa03a9da7ebfb3df5894ed807cade20d122
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786971"
---
# <a name="ctrlv-toggle-verbose-mode"></a>CTRL+V（切换详细模式）


CTRL + V 键用于打开和关闭详细模式。

CDB/KD 语法

```dbgcmd
CTRL+V  ENTER 
```

WinDbg 语法

```dbgcmd
CTRL+ALT+V 
```

## <span id="ddk_meta_ctrl_v_dbg"></span><span id="DDK_META_CTRL_V_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>CDB、KD、WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

启用详细模式后，某些显示命令 (如寄存器转储) 生成更详细的输出。 将显示发送到调试器的每个模块加载操作。 操作系统每次加载驱动程序或 DLL 时，都会通知调试器。

在 WinDbg，还可以通过选择 "视图" [| "详细输出](view---verbose-output.md)。

 

 





