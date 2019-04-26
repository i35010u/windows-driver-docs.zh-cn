---
title: ob、ow、od（输出端口）
description: Ob ow，和 od 命令向所选端口发送的字节、 字或双字。
ms.assetid: 04133df7-4b60-4709-a9e1-5946c8d30f8c
keywords:
- ob，ow，od （输出端口） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ob, ow, od (Output to Port)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2123755b3c6904d83624152e3f9f38b79fbc2389
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330999"
---
# <a name="ob-ow-od-output-to-port"></a>ob、ow、od（输出端口）


**Ob**， **ow**，并**od**命令向所选端口发送的字节、 字或双字。

```dbgcmd
ob Address Value 
ow Address Value 
od Address Value 
```

## <a name="span-idddkcmdoutputtoportdbgspanspan-idddkcmdoutputtoportdbgspanparameters"></a><span id="ddk_cmd_output_to_port_dbg"></span><span id="DDK_CMD_OUTPUT_TO_PORT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的端口地址。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *值*   
指定要写入端口的十六进制值。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>基于 x86 的仅</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Ob**命令将写入一个字节**ow**命令写入一个单词，并**od**命令写入一个双字。

请确保，则不发送一个单词或双字不支持此大小的端口。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**ib，id，信息工作者 （输入从端口）**](ib--iw--id--input-from-port-.md)

 

 






