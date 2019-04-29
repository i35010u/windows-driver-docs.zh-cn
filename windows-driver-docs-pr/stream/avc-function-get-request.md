---
title: AVC\_FUNCTION\_GET\_REQUEST
description: AVC\_FUNCTION\_GET\_REQUEST
ms.assetid: b29df7a8-782b-4014-b47e-7cf917f8e99d
keywords:
- AVC_FUNCTION_GET_REQUEST 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_REQUEST
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa191f6b7b0b54c562d6aecf2769d0961aeda4ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359084"
---
# <a name="avcfunctiongetrequest"></a>AVC\_FUNCTION\_GET\_REQUEST


## <span id="ddk_avc_function_get_request_ks"></span><span id="DDK_AVC_FUNCTION_GET_REQUEST_KS"></span>


**AVC\_函数\_获取\_请求**函数代码用于注册以接收 AV/C 单元和子单元请求。

### <a name="io-status-block"></a>I/O 状态块

此函数始终设置**Irp-&gt;IoStatus.Status**于状态\_PENDING。

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

### <a name="requirements"></a>要求

**标头：** 在中声明*avc.h*。 包括*avc.h*。

### <a name="span-idavccommandirbinputspanspan-idavccommandirbinputspanavccommandirb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC\_命令\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_获取\_请求**从 AVC\_函数枚举。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
仅当使用注册为接收单元命令。 将此项设置为 1，并提供中的单元地址**SubunitAddr**参数。 请注意，对于子单元的请求，在完成此设置为 1，并**SubunitAddr**参数指向包含此虚拟子单元实例的子单元地址的内存。 调用方可以访问此非分页的内存，但不能尝试将其释放。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
仅当使用注册为接收单元命令。 将此项设置为 1，并提供一系列由调用方中受支持的操作码**AlternateOpcodes**参数。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
忽略。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
忽略。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
在输入中被忽略。 在输出时， **CommandType**成员设置为从值中的一个**AvcCommandType**枚举。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
忽略请求。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
仅当使用注册为接收单元命令。 将此设置为包含根据 5.3.3 节的编码单元地址的非分页内存的地址**AV/C**数字接口命令设置常规规范、 Rev 3.0 (0xff)。 此规范，请参阅[1394年贸易协会](https://go.microsoft.com/fwlink/p/?linkid=8728)网站。 请注意，对于子单元的请求，在完成这指向包含此虚拟子单元实例的子单元地址的内存。 调用方可以访问此非分页的内存，但不能尝试将其释放。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
仅当使用注册为接收单元命令。 设置为包含列表的支持由调用方的单元操作码的非分页内存的地址。 操作码列表的第一个字节是操作码的计数遵循 （相当于的字节数）。 包含备用操作码列表的内存的总长度**AlternateOpcodes**\[0\]+ 1。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**超时**  
忽略。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**重试次数**  
忽略。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**Opcode**  
在输入时忽略。 在输出时，这包含 AV/C 单元操作码。 这是一个通过指定的操作码**AlternateOpcodes**。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
在输入时忽略。 在输出时，此值设置为使用请求的操作数列表中的字节数。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**操作数**  
在输入时忽略。 在输出时，此参数包含请求的操作数列表。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
在输入时忽略。 在输出时，此设置为请求的源的节点地址。 发送响应时，使用此参数 (有关详细信息，请参阅[ **AVC\_函数\_发送\_响应**](avc-function-send-response.md))。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**生成**  
在输入时忽略。 在输出时，此设置为强制生成计数时的节点地址被视为有效。 发送响应时，使用此参数 (有关详细信息，请参阅[ **AVC\_函数\_发送\_响应**](avc-function-send-response.md))。

GUID 的上下文中\_AVC\_类设备接口**AVC\_函数\_获取\_请求**函数代码用于注册以接收 AV/C 单元仅请求 （非子单元请求）。 使用此函数通常由上部的筛选器驱动程序 (的*avc.sys* FDO) 以支持对等设备功能 （也就是说，若要处理单元请求从目标设备从非虚拟堆栈）。 尽管执行任何操作阻止子单元驱动程序进行注册以处理单元请求，但子单元的驱动程序实例注册为支持的相同单元操作码必须共同协作来与其他共享状态信息。 *Avc.sys*不直接支持的相同单元操作码的多个注册。

此函数使用 AVC\_命令\_IRB 结构。 此结构定义 AV/C 命令请求的常见组件。 唯一有效的输入的参数是**SubunitAddrFlag**， **AlternateOpcodesFlag**， **AlternateOpcodes**并**SubunitAddr**，和全部是必需的。 **AlternateOpcodes**必须指向包含支持由调用方的单元操作码的列表的缓冲区。 **SubunitAddr**必须指向包含设备地址 (0xff) 的缓冲区。

在虚拟实例的情况下*avc.sys* (即，注册 GUID 的实例\_虚拟\_AVC\_类设备接口) **AVC\_函数\_获取\_请求**用于注册以接收 AV/C 单元和子单元请求。 上部的筛选器驱动程序 (虚拟*avc.sys* FDO) 通常注册以处理单元请求，而子单元驱动程序进行注册，以处理请求其特定类型的子单元。 尽管执行任何操作阻止子单元驱动程序进行注册以处理单元请求，但子单元的驱动程序实例注册为支持的相同单元操作码必须共同协作来与其他共享状态信息。 *Avc.sys*不直接支持的相同单元操作码的多个注册。

注册以接收特定于子单元的请求时，子单元驱动程序未设置任何输入的参数。

此函数始终返回状态\_PENDING，因此必须完成的例程中执行任何处理。 完成后，AVC\_命令\_IRB 结构保存的操作码和请求的操作数。 AV/C 协议要求响应发送 100 毫秒内。 这可能为了通过完成例程使用**AVC\_函数\_发送\_响应**函数。

如果使用第一个响应**AVC\_响应\_过渡期间**响应代码 (从**AvcResponseType**枚举)，则预期后续处理。 **NodeAddress**并**代**成员，通过完成**AVC\_函数\_获取\_请求**在后续响应中，必须使用原始函数。 在任何情况下，下一步**AVC\_函数\_获取\_请求**函数应返回从初始之前提交**AVC\_函数\_发送\_响应**完成例程，因此可能会收到下一个单元请求。

此结构的建议的用法是第一次零结构 (使用**RtlZeroMemory**) 之前填写参数。

可能在 IRQL 调用此函数代码&lt;= 调度\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_FUNCTION\_SEND\_RESPONSE**](avc-function-send-response.md), [**AvcResponseCode**](https://msdn.microsoft.com/library/windows/hardware/ff554105), [**AVC\_FUNCTION**](https://msdn.microsoft.com/library/windows/hardware/ff554145), [**RtlZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff563610)

 

 





