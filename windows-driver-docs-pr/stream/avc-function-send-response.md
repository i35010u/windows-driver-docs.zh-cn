---
title: AVC\_函数\_发送\_响应
description: AVC\_函数\_发送\_响应
ms.assetid: f04caed8-8521-4dfa-9bfa-cf71ec7a658e
keywords:
- AVC_FUNCTION_SEND_RESPONSE 流式处理媒体设备
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
ms.openlocfilehash: 4e9b95a36e7703f247eaee1bb02f7e8168b42384
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520157"
---
# <a name="avcfunctionsendresponse"></a>AVC\_函数\_发送\_响应


## <span id="ddk_avc_function_send_response_ks"></span><span id="DDK_AVC_FUNCTION_SEND_RESPONSE_KS"></span>


**AVC\_函数\_发送\_响应**函数代码用于 AV/C 单元和子单元请求到响应。

### <a name="io-status-block"></a>I/O 状态块

如果成功，，AV/C 协议驱动程序可能会设置**Irp-&gt;IoStatus.Status**为：

状态\_自原始请求成功，如果由于一个或多个总线放弃响应重置或

状态\_PENDING 如果响应成功传递到*是 61883.sys* （意味着成功传送到请求发起方）。

可能其他返回值包括：

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

 

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>标头

### <a name="comments"></a>备注

此函数使用 AVC\_命令\_IRB 结构如下所示。

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

### <a name="span-idavccommandirbinputspanspan-idavccommandirbinputspanavccommandirb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC\_命令\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_发送\_响应**从 AVC\_函数枚举。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
设置为从获取的值**AVC\_函数\_获取\_请求**完成。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
忽略。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
忽略。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
忽略。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
忽略的响应。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
此成员必须设置为中的值之一**AvcResponseCode**枚举。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
设置为从获取的值**AVC\_函数\_获取\_请求**完成。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
忽略。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**超时**  
忽略。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**重试次数**  
忽略。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**Opcode**  
此文件必须包含适用于 （可能不同于原始请求中提供的操作码） 的响应的 AV/C 单元操作码。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
将设置为响应的操作数列表中的字节数。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**操作数**  
响应的操作数列表。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
原始请求的源的节点地址。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**生成**  
获取原始请求中的生成 ID。

GUID 的上下文中\_AVC\_类设备接口**AVC\_函数\_发送\_响应**函数代码用于 AV/C 单元请求只会响应。

在虚拟实例的情况下*avc.sys* (即，注册 GUID 的实例\_虚拟\_AVC\_类设备接口)，则**AVC\_函数\_发送\_响应**函数代码用于响应 AV/C 单元*和*子单元请求。

如果使用第一个响应**AVC\_响应\_过渡期间**响应代码 (从**AvcResponseType**枚举)，则预期后续处理。 **NodeAddress**并**代**成员，通过完成**AVC\_函数\_获取\_请求**在后续响应中，必须使用原始函数。 在任何情况下，下一步**AVC\_函数\_获取\_请求**函数应返回从初始之前提交**AVC\_函数\_发送\_响应**完成例程，因此可能会收到下一个单元请求。

此结构的建议的用法是使用原始请求的内容并更新**操作码**， **OperandLength**，并**操作数**成员作为适用于响应。

可能在 IRQL 调用此函数代码&lt;= 调度\_级别。

### <a name="see-also"></a>另请参阅

[**AVC\_FUNCTION\_GET\_REQUEST**](avc-function-get-request.md), [**AvcResponseCode**](https://msdn.microsoft.com/library/windows/hardware/ff554105), [**AVC\_FUNCTION**](https://msdn.microsoft.com/library/windows/hardware/ff554145)

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
<td>Avc.h （包括 Avc.h）</td>
</tr>
</tbody>
</table>

 

 





