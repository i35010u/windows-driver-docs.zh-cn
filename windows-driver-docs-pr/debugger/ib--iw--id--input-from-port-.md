---
title: ib、iw、id（从端口输入）
description: Ib、 信息工作者和 id 的命令读取和显示字节、 字或双字来自所选端口。
ms.assetid: 68f9e0c2-3cfd-46e1-a513-5a96c93de63c
keywords:
- ib，信息工作者，id （从端口输入） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ib, iw, id (Input from Port)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7b7e5a6658f9bcb46e0e5e3616e3f7ef3c3a56f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381034"
---
# <a name="ib-iw-id-input-from-port"></a>ib、iw、id（从端口输入）


**Ib**， **iw**，并**id**命令读取和显示字节、 字或双字来自所选端口。

```dbgcmd
ib Address 
iw Address 
id Address
```

## <a name="span-idddkcmdinputfromportdbgspanspan-idddkcmdinputfromportdbgspanparameters"></a><span id="ddk_cmd_input_from_port_dbg"></span><span id="DDK_CMD_INPUT_FROM_PORT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
该端口的地址。

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
<td align="left"><p>基于 x86 的计算机</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Ib**命令读取一个字节**iw**命令读取一个词并**id**命令读取双字。

请确保读取 I/O 端口不会影响从查看设备的行为。 读取只读的端口后，某些设备将更改状态。 您也不应尝试从端口不允许此长度的值中读取的单词或双字。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**ob，od，ow （输出到端口）**](ob--ow--od--output-to-port-.md)

 

 






