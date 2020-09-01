---
title: AVC \_ 函数 \_ 发送 \_ 响应
description: AVC \_ 函数 \_ 发送 \_ 响应
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
ms.openlocfilehash: 77f261ea9a7711a6ea9c71e231a0b912861193a8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187473"
---
# <a name="avc_function_send_response"></a>AVC \_ 函数 \_ 发送 \_ 响应


## <span id="ddk_avc_function_send_response_ks"></span><span id="DDK_AVC_FUNCTION_SEND_RESPONSE_KS"></span>


**AVC \_ 函数 \_ SEND \_ RESPONSE**函数代码用于响应 AV/C 单元和子请求。

### <a name="io-status-block"></a>I/o 状态块

如果成功，AV/C 协议驱动程序可以将 **Irp &gt; IoStatus** 设置为：

\_如果由于自原始请求以来发生了一个或多个总线重置而放弃响应，则状态成功;

\_如果已成功将响应传递到*61883.sys* ，则状态为 "已挂起" (表示) 成功传递到请求发起方。

可能的其他返回值包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回值</th>
<th>说明</th>
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

### <a name="comments"></a>说明

此函数使用 AVC \_ 命令 \_ IRB 结构，如下所示。

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

### <a name="span-idavc_command_irb_inputspanspan-idavc_command_irb_inputspanavc_command_irb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC \_ 命令 \_ IRB 输入

**通用**  
此成员的 submember **函数** 必须设置为 **AVC \_ FUNCTION \_ SEND \_ RESPONSE** from AVC \_ 函数枚举。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
设置为从 **AVC \_ 函数 \_ GET \_ 请求** 完成获取的值。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
已忽略。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
已忽略。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
已忽略。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
对于响应已被忽略。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
此成员必须设置为 **AvcResponseCode** 枚举中的值之一。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
设置为从 **AVC \_ 函数 \_ GET \_ 请求** 完成获取的值。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
已忽略。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**Timeout**  
已忽略。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**重试**  
已忽略。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**码**  
此项必须包含适用于响应的 AV/C 单位操作码 (可能不同于原始请求) 中提供的操作码。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
设置为响应的操作数列表中的字节数。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**个数**  
响应的操作数列表。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
原始请求的源的节点地址。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**产生**  
从原始请求获取的生成 ID。

在 GUID \_ AVC \_ 类设备接口的上下文中， **AVC \_ 函数 \_ SEND \_ RESPONSE** 函数代码用于仅对 AV/C 单元请求做出响应。

对于 *avc.sys* 的虚拟实例 (即， \_ 将 GUID virtual \_ AVC \_ 类设备接口注册) 的实例， **AVC \_ 函数 \_ 发送 \_ 响应** 函数代码用于响应 AV/C 单元 *和* 子发送请求。

如果第一个响应使用 **AVC \_ 响应 \_ 过渡** 代码 (来自 **AvcResponseType** 枚举) ，则需要跟进处理。 在后续响应中，必须使用完成**AVC \_ 函数 \_ GET \_ 请求**原始函数时获得的**NodeAddress**和**生成**成员。 在任何情况下，都应在从初始**AVC \_ 函数 \_ 发送 \_ 响应**完成例程返回之前提交下一个**AVC \_ 函数 \_ GET \_ 请求**函数，以便可以收到下一个单位请求。

此结构的建议用法是使用原始请求的内容，并根据响应更新 **Opcode**、 **OperandLength**和 **操作数** 成员。

可以在 IRQL &lt; = 调度级别调用此函数代码 \_ 。

### <a name="see-also"></a>另请参阅

[**AVC \_函数 \_ GET \_ REQUEST**](avc-function-get-request.md)、 [**AvcResponseCode**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)、 [**AVC \_ 函数**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Avc (包含 Avc) </td>
</tr>
</tbody>
</table>

 

