---
title: AVC\_函数\_获取\_请求
description: AVC\_函数\_获取\_请求
ms.assetid: b29df7a8-782b-4014-b47e-7cf917f8e99d
keywords:
- AVC_FUNCTION_GET_REQUEST 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_REQUEST
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 808b4220dfeaa1aba8a930d23fc16fa30224b67a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845082"
---
# <a name="avc_function_get_request"></a>AVC\_函数\_获取\_请求


## <span id="ddk_avc_function_get_request_ks"></span><span id="DDK_AVC_FUNCTION_GET_REQUEST_KS"></span>


**AVC\_函数\_获取\_请求**函数代码用于注册接收 AV/C 单元和子请求。

### <a name="io-status-block"></a>I/O 状态块

此函数始终将**Irp&gt;的 IoStatus**状态设置为 "状态\_挂起"。

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

### <a name="requirements"></a>要求

**标头：** 在*avc*中声明。 包括*avc*。

### <a name="span-idavc_command_irb_inputspanspan-idavc_command_irb_inputspanavc_command_irb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC\_命令\_IRB 输入

**常见问题解答**  
此成员的**函数**submember 必须设置为**AVC\_函数\_** 从 AVC\_函数枚举获取\_请求。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
仅在注册接收单元命令时使用。 将此项设置为1，并在**SubunitAddr**参数中提供单元地址。 请注意，对于子请求，在完成时，此参数设置为1， **SubunitAddr**参数指向包含此虚拟子实例实例的子地址的内存。 调用方可以访问此非分页内存，但不得尝试释放它。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
仅在注册接收单元命令时使用。 将此项设置为1，并在**AlternateOpcodes**参数中提供调用方支持的操作码列表。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
掉.

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
掉.

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
在输入中被忽略。 在输出时， **CommandType**成员设置为**AvcCommandType**枚举中的值之一。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
对于请求被忽略。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
仅在注册接收单元命令时使用。 将此设置为非分页内存地址，该地址包含按**AV/C**数字接口命令集 "常规规范，Rev 3.0 （0xff）" 部分5.3.3 编码的单元地址。 可以在[1394 商业协会](https://go.microsoft.com/fwlink/p/?linkid=8728)网站上找到此规范。 请注意，对于子请求，在完成时，将指向包含此虚拟子实例的子地址的内存。 调用方可以访问此非分页内存，但不得尝试释放它。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
仅在注册接收单元命令时使用。 将此设置为包含调用方支持的单元操作码列表的非分页内存的地址。 操作码列表的第一个字节是要跟踪的操作码的计数（相当于字节数）。 包含备用操作码列表的内存的总长度为**AlternateOpcodes**\[0\]+ 1。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**Timeout**  
掉.

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**重试**  
掉.

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**码**  
在输入时忽略。 输出时，这包含 AV/C 单元操作码。 这是通过**AlternateOpcodes**指定的操作码之一。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
在输入时忽略。 在输出上，此值设置为请求使用的操作数列表中的字节数。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**个数**  
在输入时忽略。 在输出时，此参数包含请求的操作数列表。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
在输入时忽略。 在输出上，此设置为请求源的节点地址。 发送响应时使用此参数（有关详细信息，请参阅[**AVC\_函数\_发送\_响应**](avc-function-send-response.md)）。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**产生**  
在输入时忽略。 在输出时，此项设置为在节点地址被视为有效时强制执行的生成计数。 发送响应时使用此参数（有关详细信息，请参阅[**AVC\_函数\_发送\_响应**](avc-function-send-response.md)）。

在 GUID\_AVC\_类设备接口的上下文中， **AVC\_函数\_获取\_请求**函数代码用于注册以仅接收 AV/C 单元请求（而不是子请求）。 此函数通常由高筛选器驱动程序（ *avc* FDO）用于支持对等设备功能（即，用于处理来自非虚拟堆栈的目标设备的单元请求）。 尽管不会阻止子工作区驱动程序注册来处理单元请求，但注册以支持相同单元操作码的子源驱动程序实例必须彼此合作，才能共享状态信息。 *Avc*不直接支持对同一单元操作码进行多个注册。

此函数使用 AVC\_命令\_IRB 结构。 此结构定义 AV/C 命令请求的常用组件。 唯一有效的输入参数是**SubunitAddrFlag**、 **AlternateOpcodesFlag**、 **AlternateOpcodes**和**SubunitAddr**，都是必需的。 **AlternateOpcodes**必须指向包含调用方支持的单元操作码列表的缓冲区。 **SubunitAddr**必须指向包含单位地址（0xff）的缓冲区。

对于*avc*的虚拟实例（即，将 GUID 注册\_VIRTUAL\_AVC\_类设备接口） **avc\_函数\_获取\_请求**用于注册接收 AV/C单元和子请求。 上层筛选器驱动程序（属于 virtual *avc* FDO）通常注册来处理单元请求，而子单元驱动程序则注册来处理其特定类型的子单位的请求。 尽管不会阻止子工作区驱动程序注册来处理单元请求，但注册以支持相同单元操作码的子源驱动程序实例必须彼此合作，才能共享状态信息。 *Avc*不直接支持对同一单元操作码进行多个注册。

在注册接收特定于子请求的请求时，子源驱动程序不会设置任何输入参数。

此函数始终返回状态\_"挂起"，因此必须在完成例程中执行任何处理。 完成后，AVC\_命令\_IRB 结构保存请求的操作码和操作数。 AV/C 协议要求在100ms 中发送响应。 这可以通过使用**AVC\_函数\_发送\_响应**功能来完成。

如果第一个响应使用**AVC\_响应\_了过渡**响应代码（来自**AvcResponseType**枚举），则需要跟进处理。 完成**AVC\_函数\_获取\_请求**原始函数时获得的**NodeAddress**和**代**成员必须在后续响应中使用。 在任何情况下，下一个**AVC\_函数\_获取\_请求**函数应在从初始 AVC\_函数返回之前提交\_**发送\_响应**完成例程，以便下一个单位可能收到请求。

在填写参数之前，此结构的建议使用是结构（使用**RtlZeroMemory**）的第一个。

此函数代码可在 IRQL &lt;= 调度\_级别调用。

### <a name="see-also"></a>另请参阅

[**AVC\_函数\_发送\_RESPONSE**](avc-function-send-response.md)、 [**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)、 [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、 [**RtlZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)

 

 





