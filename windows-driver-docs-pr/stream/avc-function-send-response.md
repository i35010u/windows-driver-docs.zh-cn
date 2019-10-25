---
title: AVC\_函数\_发送\_响应
description: AVC\_函数\_发送\_响应
ms.assetid: f04caed8-8521-4dfa-9bfa-cf71ec7a658e
keywords:
- AVC_FUNCTION_SEND_RESPONSE 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_SEND_RESPONSE
api_location:
- avc.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a0dbd6069705f0e05b9d1a465f635f634150a35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845072"
---
# <a name="avc_function_send_response"></a>AVC\_函数\_发送\_响应


## <span id="ddk_avc_function_send_response_ks"></span><span id="DDK_AVC_FUNCTION_SEND_RESPONSE_KS"></span>


**AVC\_函数\_发送\_响应**功能代码用于响应 AV/C 单元和子请求。

### <a name="io-status-block"></a>I/O 状态块

如果成功，AV/C 协议驱动程序可以将**Irp&gt;IoStatus**设置为：

如果由于自原始请求以来发生了一个或多个总线重置而放弃响应，则状态\_成功，或

如果响应成功传递到*61883* （表示成功传递到请求发起方），则状态\_挂起。

可能的其他返回值包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>内部缓冲区分配失败。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>只要

### <a name="comments"></a>备注

此函数使用 AVC\_命令\_IRB 结构，如下所示。

```cpp
typedef struct _AVC_COMMAND_IRB {
  AVC_IRB  Common;
  UCHAR  SubunitAddrFlag : 1;
  UCHAR  AlternateOpcodesFlag : 1;
  UCHAR  TimeoutFlag : 1;
  UCHAR  RetryFlag : 1;
  union {
    UCHAR  CommandType;
    UCHAR  ResponseCode;
  };
  PUCHAR  SubunitAddr;
  PUCHAR  AlternateOpcodes;
  LARGE_INTEGER  Timeout;
  UCHAR  Retries;
  UCHAR  Opcode;
  ULONG  OperandLength;
  UCHAR  Operands[MAX_AVC_OPERAND_BYTES];
  NODE_ADDRESS  NodeAddress;
  ULONG  Generation;
} AVC_COMMAND_IRB, *PAVC_COMMAND_IRB;
```

### <a name="span-idavc_command_irb_inputspanspan-idavc_command_irb_inputspanavc_command_irb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC\_命令\_IRB 输入

**常见问题解答**  
此成员的**函数**submember 必须设置为**AVC\_函数\_** 通过 AVC\_函数枚举发送\_响应。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
设置为从**AVC\_函数获取的值\_获取\_请求**完成。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
掉.

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
掉.

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
掉.

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
对于响应已被忽略。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
此成员必须设置为**AvcResponseCode**枚举中的值之一。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
设置为从**AVC\_函数获取的值\_获取\_请求**完成。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
掉.

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**Timeout**  
掉.

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**重试**  
掉.

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**码**  
这必须包含适用于响应的 AV/C 单位操作码（可能不同于原始请求中提供的操作码）。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
设置为响应的操作数列表中的字节数。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**个数**  
响应的操作数列表。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
原始请求的源的节点地址。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**产生**  
从原始请求获取的生成 ID。

在 GUID\_AVC\_类设备接口的上下文中， **AVC\_函数\_SEND\_** 用于响应 AV/C 单元请求。

对于*avc*的虚拟实例（即，将 GUID 注册\_虚拟\_AVC\_类设备接口）的实例，将使用**avc\_函数\_SEND\_RESPONSE**函数代码来响应 AV/C 单元*和*子请求。

如果第一个响应使用**AVC\_响应\_了过渡**响应代码（来自**AvcResponseType**枚举），则需要跟进处理。 完成**AVC\_函数\_获取\_请求**原始函数时获得的**NodeAddress**和**代**成员必须在后续响应中使用。 在任何情况下，下一个**AVC\_函数\_获取\_请求**函数应在从初始 AVC\_函数返回之前提交\_**发送\_响应**完成例程，以便下一个单位可能收到请求。

此结构的建议用法是使用原始请求的内容，并根据响应更新**Opcode**、 **OperandLength**和**操作数**成员。

此函数代码可在 IRQL &lt;= 调度\_级别调用。

### <a name="see-also"></a>另请参阅

[**AVC\_函数\_获取\_请求**](avc-function-get-request.md)、 [**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)、 [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Avc （包括 Avc）</td>
</tr>
</tbody>
</table>

 

 





