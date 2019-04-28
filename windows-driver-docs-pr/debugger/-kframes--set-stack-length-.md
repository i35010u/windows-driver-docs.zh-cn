---
title: .kframes（设置堆栈长度）
description: .Kframes 命令设置堆栈跟踪显示的默认长度。
ms.assetid: 4f11a197-add1-4957-8345-dfbdb2037605
keywords:
- 设置堆栈长度 (.kframes) 命令
- .kframes （设置堆栈的长度） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .kframes (Set Stack Length)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6775751def8fa5a72ec6b191b660a11f22907ce7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336329"
---
# <a name="kframes-set-stack-length"></a>.kframes（设置堆栈长度）


**.Kframes**命令设置的堆栈跟踪显示默认长度。

```dbgcmd
.kframes FrameCountDefault 
```

## <a name="span-idddkmetasetstacklengthdbgspanspan-idddkmetasetstacklengthdbgspanparameters"></a><span id="ddk_meta_set_stack_length_dbg"></span><span id="DDK_META_SET_STACK_LENGTH_DBG"></span>参数


<span id="_______FrameCountDefault______"></span><span id="_______framecountdefault______"></span><span id="_______FRAMECOUNTDEFAULT______"></span> *FrameCountDefault*   
指定要显示使用堆栈跟踪命令时的堆栈帧数。

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

可以使用 **.kframes**命令以设置堆栈跟踪显示的默认长度。 此长度控制帧数， [ **k、 kb、 kp，kP 和 kv** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令显示和双字节数\_合作伙伴的**kd**命令将显示。

可以通过使用重写此默认长度*FrameCount*或*WordCount*这些命令的参数。

如果永远不会发出 **.kframes**命令中，默认计数为 20 (0x14)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

 

 






