---
title: CTRL+V（切换详细模式）
description: CTRL + V 键切换详细模式下打开和关闭。
ms.assetid: 1aca1452-86dd-4573-8ad0-e46aa474a324
keywords:
- CTRL + V （切换详细模式） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+V (Toggle Verbose Mode)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c4ddf221b72862cef4d520fe8e34a7c4524c709
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374952"
---
# <a name="ctrlv-toggle-verbose-mode"></a>CTRL+V（切换详细模式）


CTRL + V 键切换详细模式下打开和关闭。

CDB / KD 语法

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
<td align="left"><p>KD、 CDB WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

启用详细模式后，某些显示的命令 （例如注册转储） 生成更详细的输出。 将显示发送到调试器的每个模块加载操作。 并且每次由操作系统加载驱动程序或 DLL，调试器将会收到通知。

在 WinDbg 中，还可以通过选择[视图 |详细输出](view---verbose-output.md)。

 

 





