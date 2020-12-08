---
title: .kframes（设置堆栈长度）
description: Kframes 命令设置堆栈跟踪显示的默认长度。
keywords:
- " () 命令设置堆栈长度"
- kframes (设置堆栈长度) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .kframes (Set Stack Length)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 88c068ef308555d5e2f06c74131d580a23c6a206
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826753"
---
# <a name="kframes-set-stack-length"></a>.kframes（设置堆栈长度）


**Kframes** 命令设置堆栈跟踪显示的默认长度。

```dbgcmd
.kframes FrameCountDefault 
```

## <a name="span-idddk_meta_set_stack_length_dbgspanspan-idddk_meta_set_stack_length_dbgspanparameters"></a><span id="ddk_meta_set_stack_length_dbg"></span><span id="DDK_META_SET_STACK_LENGTH_DBG"></span>参数


<span id="_______FrameCountDefault______"></span><span id="_______framecountdefault______"></span><span id="_______FRAMECOUNTDEFAULT______"></span>*FrameCountDefault*   
指定在使用堆栈跟踪命令时要显示的堆栈帧的数目。

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

可以使用 **kframes** 命令设置堆栈跟踪显示的默认长度。 此长度控制 [**k、kb、kp、kp 和 kv**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令显示的帧数，以及 \_ **KD** 命令显示的 DWORD PTRs 的数量。

可以通过对这些命令使用 *FrameCount* 或 *WordCount* 参数来重写此默认长度。

如果从不发出 **kframes** 命令，默认计数为 20 (0x14) 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**k、kb、kc、kd、kp、kP、kv（显示堆栈回溯）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

 

 






