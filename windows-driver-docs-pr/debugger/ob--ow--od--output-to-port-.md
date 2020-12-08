---
title: ob、ow、od（输出端口）
description: Ob、o 和 od 命令向所选端口发送字节、字或双字。
keywords:
- ob、o、od (输出到端口) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ob, ow, od (Output to Port)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50eca226d295a548512c07912006950fee045588
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833635"
---
# <a name="ob-ow-od-output-to-port"></a>ob、ow、od（输出端口）


**Ob**、 **o** 和 **od** 命令向所选端口发送字节、字或双字。

```dbgcmd
ob Address Value 
ow Address Value 
od Address Value 
```

## <a name="span-idddk_cmd_output_to_port_dbgspanspan-idddk_cmd_output_to_port_dbgspanparameters"></a><span id="ddk_cmd_output_to_port_dbg"></span><span id="DDK_CMD_OUTPUT_TO_PORT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定端口的地址。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span>*值*   
指定要写入端口的十六进制值。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>仅基于 x86</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Ob** 命令写入一个字节， **o** 命令写入一个词，而 **od** 命令写入一个双字。

请确保不要向不支持此大小的端口发送字或双字。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**ib、id、iw (来自端口) 的输入**](ib--iw--id--input-from-port-.md)

 

 






