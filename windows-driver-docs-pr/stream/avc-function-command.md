---
title: AVC\_函数\_命令
description: AVC\_函数\_命令
ms.assetid: 5e1f7f93-83ef-4015-a952-f7efd93ccee5
keywords:
- AVC_FUNCTION_COMMAND 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_COMMAND
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b897d5afd7ef8d6c3de5b660e85aa5079e00c452
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386758"
---
# <a name="avcfunctioncommand"></a>AVC\_函数\_命令


## <span id="ddk_avc_function_command_ks"></span><span id="DDK_AVC_FUNCTION_COMMAND_KS"></span>


**AVC\_函数\_命令**函数代码用于发送 AV/C 请求和接收响应作为一个操作。

### <a name="io-status-block"></a>I/O 状态块

如果成功，AV/C 协议驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功。

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
<td><p>STATUS_TIMEOUT</p></td>
<td><p>发出请求，但未收到响应之前所有的超时和重试处理已完成。 如果仍在处理上一个请求，目标设备将忽略请求。 某些 AV/C 的设备不符合要求，且拒绝内 100 毫秒的超时值，即使在多次连续尝试后响应。 AVC_COMMAND_IRB 结构允许的默认值调整<strong>超时</strong>并<strong>重试</strong>成员 (100 毫秒和 9，分别)，但这些默认设置已经足够所有已知实现。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_PENDING</p></td>
<td><p>发出请求，并收到了临时的响应。 它可以负责完成例程来处理最终响应和释放的 IRP 和 IRB 资源。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>当提交的 AV C 请求时，立即中止 STATUS_REQUEST_ABORTED IRP 完成状态时。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_*</p></td>
<td><p>任何其他返回代码指示错误或警告发生了超出范围的 AV/C 协议。</p></td>
</tr>
</tbody>
</table>

 

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
**函数**必须设置为此成员的子**AVC\_函数\_命令**从 AVC\_函数枚举。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
设置到另一个用于重写子单元地址*avc.sys*子单元驱动程序相关联。 重写的原因包括： 子单元驱动程序表示单个实例; 中的多个子单元连接必须发送单元命令;或加载驱动程序，因为*avc.sys*无法确定子单元类型或 id。 如果此设置， **SubunitAddr**成员必须指向包含所需的子单元地址的非分页内存。

此属性必须设置为一个 (适当**SubunitAddr**提供) 如果调用方直接向正在提交请求*avc.sys* FDO。

注意：如果未在请求中，从成功的请求，响应上设置此标志设置此标志，并**SubunitAddr**成员指向子单元的实际地址。 不要尝试更改此内容或释放的内存： 它是父驱动程序的设备扩展的一部分。 这可能，当然，要将重新设为零，并且**SubunitAddr**指针清除可重复使用不同的子单元的结构。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
设置为一个 if 命令类型和操作码的此请求结果中具有不同的操作码的响应。 如果没有，接受仅具有匹配的操作码的响应。 如果此设置， **AlternateOpcodes**成员必须指向包含列表的备用操作码的非分页内存指针。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
将此设置为一个如果默认超时值不适合于子单元。 如果此设置，**超时**成员必须设置为所需的超时 （以 100 纳为单位）。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
设置为一种适用的默认重试次数不适合于子单元。 如果此设置，**重试**成员必须设置为所需的重试计数。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
在请求时，此成员必须设置为从枚举器之一**AvcCommandType**枚举。 这是一个必需的参数。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
在响应中，此成员设置为一个介于**AvcResponseCode**枚举。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
设置为包含所需的子单元地址是根据 5.3.3 节的 AV/C 数字接口命令设置常规规范 Rev 3.0 编码的非分页内存的地址。 此规范，请参阅[1394年贸易协会](https://go.microsoft.com/fwlink/p/?linkid=8728)网站。 没有长度限制是必要的因为子单元地址编码意味着这。 如果忽略此参数**SubunitAddrFlag**为零。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
设置为包含所需的备用操作码列表的非分页内存的地址。 操作码列表的第一个字节是操作码的计数遵循 （相当于的字节数）。 包含备用操作码列表的内存的总长度是 AlternateOpcodes\[0\]+ 1。 如果忽略此参数**AlternateOpcodesFlag**为零。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**超时**  
将此设置为以 100 纳为单位的所需的超时值。 例如，默认超时值为：**Timeout.QuadPart** = 1000000 （100ns 个单位 100 毫秒）。 如果忽略此参数**TimeoutFlag**为零。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**重试次数**  
将此设置为所需的时间数*avc.sys*应尝试在没有响应每个超时后重试请求。 请注意，重试计数为零意味着再次重试请求。 尝试处理命令而不获取响应所用的时间总量计算由以下公式：

***超时***  *\* (* * *<em>重试</em>* *  *+ 1)*

如果忽略此参数**RetryFlag**为零。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**Opcode**  
将此设置为所需的 AV/C 操作码 （适用于子单元类型）。 这是一个必需的参数。 在响应中，如果**AlternateOpcodesFlag**已设置，和一个备用操作码用于匹配响应，此值设置为该备用操作码。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
将此设置为用于存储操作数中的字节数**操作数**成员。 这是一个必需的参数。 在响应中，此参数设置为响应所使用的操作数列表中的字节数。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**操作数**  
设置为操作数列表适用于子单元类型和操作码。 这是一个必需的参数。 在响应中，此参数包含响应的操作数列表。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
保留。 这必须为零。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**生成**  
保留。 这必须为零。

**AVC\_函数\_命令**个虚拟实例不支持函数代码*avc.sys*。 如果调用方想要控制外部设备，该设备的非虚拟实例可位于通过私有机制或某些结合在一起的 AVC\_函数\_查找\_对等方\_执行操作，请**AVC\_函数\_对等方\_执行\_列表**并**AVC\_函数\_GET\_子单元\_信息**函数代码 IOCTL\_AVC\_类 I/O 控制代码。

此结构定义 AV/C 命令请求的常见组件。 它包含的操作码和请求和操作码的操作数和 （完成） 的响应的操作数。 在允许的最大操作数给定的单字节子单元地址数被固定操作数列表的大小。 如果以任何方式延长的子单元地址，则也将相应降低允许的最大操作数字节数。

此结构的建议的用法是第一次零结构 (使用**RtlZeroMemory**) 之前填写参数。

这必须在调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)， [ **AvcCommandType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavccommandtype)， [ **AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavcresponsecode)， [**AVC\_函数\_查找\_对等方\_执行**](avc-function-find-peer-do.md)， [ **AVC\_函数\_对等\_做\_列表**](avc-function-peer-do-list.md)， [ **AVC\_函数\_GET\_子单元\_信息**](avc-function-get-subunit-info.md)

 

 





