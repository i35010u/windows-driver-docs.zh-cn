---
title: ib、iw、id（从端口输入）
description: Ib、iw 和 id 命令读取并显示所选端口中的字节、字或双字。
keywords:
- ib、iw、id (来自端口) Windows 调试的输入
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ib, iw, id (Input from Port)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55f2475d00d7a29abf427f638d08259321f2e03d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836871"
---
# <a name="ib-iw-id-input-from-port"></a>ib、iw、id（从端口输入）


**Ib**、 **iw** 和 **id** 命令读取并显示所选端口中的字节、字或双字。

```dbgcmd
ib Address 
iw Address 
id Address
```

## <a name="span-idddk_cmd_input_from_port_dbgspanspan-idddk_cmd_input_from_port_dbgspanparameters"></a><span id="ddk_cmd_input_from_port_dbg"></span><span id="DDK_CMD_INPUT_FROM_PORT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
端口的地址。

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
<td align="left"><p>仅基于 x86 的计算机</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Ib** 命令读取单个字节， **iw** 命令读取一个单词， **id** 命令读取一个双字。

请确保读取 i/o 端口不会影响正在读取的设备的行为。 读取只读端口后，某些设备会更改状态。 还应不要尝试从不允许使用此长度值的端口读取字词或双字。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**ob、od、o (输出到端口)**](ob--ow--od--output-to-port-.md)

 

 






