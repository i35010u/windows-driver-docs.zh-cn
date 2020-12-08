---
title: CTRL+D（切换调试信息）
description: CTRL + D 键用于打开和关闭调试器内部信息流。 这用于在调试器未正确通信的情况下重新启动通信。
keywords:
- CTRL + D (切换调试信息) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+D (Toggle Debug Info)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ced47b865d73ce14b7794c359f0c8a97cf9e761a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786999"
---
# <a name="ctrld-toggle-debug-info"></a>CTRL+D（切换调试信息）


CTRL + D 键用于打开和关闭调试器内部信息流。 这用于在调试器未正确通信的情况下，重新启动目标计算机与主计算机之间的通信。

KD 语法

```dbgcmd
CTRL+D  ENTER 
```

WinDbg 语法

```dbgcmd
CTRL+ALT+D 
```

## <span id="ddk_meta_ctrl_d_dbg"></span><span id="DDK_META_CTRL_D_DBG"></span>


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

切换到此时，调试器会输出有关主计算机与目标计算机之间的通信的信息。

此密钥可用于测试调试器是否崩溃。 如果怀疑调试器或目标已冻结，请使用此密钥。 如果看到正在发送的数据包，则目标仍在运行。 如果你看到超时消息，则目标没有响应。 如果根本没有消息，则调试器已崩溃。

如果目标未响应，请按 CTRL + R ENTER CTRL + C。 如果持续显示超时消息，则目标 (崩溃，或者调试程序) 配置错误。

这对于调试 KD 调试器本身也很有用。

 

 





