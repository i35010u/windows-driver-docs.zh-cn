---
title: AVC\_函数\_命令
description: AVC\_函数\_命令
ms.assetid: 5e1f7f93-83ef-4015-a952-f7efd93ccee5
keywords:
- AVC_FUNCTION_COMMAND 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_COMMAND
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ef1a5ed6a0d62bafbbadc55fd94ad76f0d245ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843558"
---
# <a name="avc_function_command"></a>AVC\_函数\_命令


## <span id="ddk_avc_function_command_ks"></span><span id="DDK_AVC_FUNCTION_COMMAND_KS"></span>


**AVC\_函数\_命令**函数代码用于发送 AV/C 请求，并作为一个操作接收响应。

### <a name="io-status-block"></a>I/O 状态块

如果成功，AV/C 协议驱动程序会将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS。

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
<td><p>STATUS_TIMEOUT</p></td>
<td><p>发出了请求，但在所有超时和重试处理完成之前未收到响应。 如果仍在处理以前的请求，则目标设备将忽略请求。 有些 AV/C 设备不相容，并拒绝在 100 ms 超时时间内做出响应，即使在若干次连续尝试之后也是如此。 AVC_COMMAND_IRB 结构允许调整默认的<strong>超时</strong>和<strong>重试</strong>成员（分别为100ms 和9），但这些默认设置已足以满足所有已知的实现要求。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_PENDING</p></td>
<td><p>发出了请求，但收到了过渡响应。 完成例程负责处理最终响应并释放 IRP 和 IRB 资源。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>提交 AV/C 请求时，当 IRP 完成状态为 "STATUS_REQUEST_ABORTED" 时立即中止。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_*</p></td>
<td><p>任何其他返回代码指示出现超出 AV/C 协议范围的错误或警告。</p></td>
</tr>
</tbody>
</table>

 

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
此成员的**函数**submember 必须设置为**AVC\_函数\_** AVC\_函数枚举中的命令。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
将此项设置为1，以替代*avc*与子单位驱动程序关联的子地址。 重写的原因包括：子单位驱动程序表示单个实例中的多个子单元连接;必须发送单元命令;或驱动程序已加载，因为*avc*无法确定子单位类型或 ID。 如果已设置此设置，则**SubunitAddr**成员必须指向包含所需的子地址的非分页内存。

如果调用方直接将请求提交到*avc* FDO，则必须将此项设置为1（以及提供的适当**SubunitAddr** ）。

注意：如果在请求时未设置此标志，则在对成功请求作出响应时，将设置此标志，并且**SubunitAddr**成员指向次级的实际地址。 请勿尝试更改内容或释放内存：它是父驱动程序的设备扩展的一部分。 当然，这可能会恢复为零，并且**SubunitAddr**指针将被清除，以便重复使用其他子单位的结构。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
如果此请求的命令类型和操作码导致响应具有不同的操作码，请将此项设置为1。 如果没有此条件，则只接受具有匹配操作码的响应。 如果已设置此设置， **AlternateOpcodes**成员必须指向包含备用操作码列表的非分页内存。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
如果默认超时值不适合于子单位，请将此项设置为1。 如果设置了此值，则必须将超时成员设置为所需的超时**值**（以 100-ns 单位为单位）。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
如果默认重试次数不适用于子单位，请将此项设置为1。 如果已设置此设置，则必须将**重**试成员设置为所需的重试次数。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
在请求时，必须将此成员设置为**AvcCommandType**枚举中的一个枚举器。 这是必需的参数。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
响应时，将此成员设置为**AvcResponseCode**枚举中的一个值。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
将此设置为非分页内存地址，其中包含根据 AV/C 数字接口命令集常规规范 Rev 3.0 的节5.3.3 进行编码的所需的子地址。 可以在[1394 商业协会](https://go.microsoft.com/fwlink/p/?linkid=8728)网站上找到此规范。 无需长度，因为子单位地址编码意味着这一点。 如果**SubunitAddrFlag**为零，则忽略此参数。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
将此设置为包含所需备用操作码列表的非分页内存地址。 操作码列表的第一个字节是要跟踪的操作码的计数（相当于字节数）。 包含备用操作码列表的内存的总长度为 AlternateOpcodes\[0\]+ 1。 如果**AlternateOpcodesFlag**为零，则忽略此参数。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**Timeout**  
将此项设置为 100-ns 单位中所需的超时。 例如，默认超时值为： **QuadPart** = 1000000 （100ms 以100ns 为单位）。 如果**TimeoutFlag**为零，则忽略此参数。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**重试**  
将此项设置为所需的次数， *avc*应在每次超时后尝试重试请求，而无需响应。 请注意，重试计数为零表示请求尝试一次。 尝试在不获取响应的情况下处理命令所花费的总时间由以下公式计算得出：

***超时*** *\* （* * *<em>重试</em>* *  *+ 1）*

如果**RetryFlag**为零，则忽略此参数。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**码**  
将此设置为所需的 AV/C 操作码（适用于子类型）。 这是必需的参数。 响应时，如果设置了**AlternateOpcodesFlag** ，并使用了某个备用操作码来匹配响应，则会将其设置为该备用操作码。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
将此项设置为用于在**操作数**成员中存储操作数的字节数。 这是必需的参数。 响应时，此参数设置为响应使用的操作数列表中的字节数。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**个数**  
将此设置为适用于子类型和操作码的操作数列表。 这是必需的参数。 响应时，此参数包含响应的操作数列表。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
保留。 此值必须为零。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**产生**  
保留。 此值必须为零。

*AVC*的虚拟实例不支持**AVC\_函数\_命令**函数代码。 如果调用方希望控制外部设备，则该设备的非虚拟实例可以通过专用机制定位，也可以通过 AVC\_函数的某种组合查找\_查找\_对等\_DO， **AVC\_函数\_对等\_执行\_列表**和**AVC\_函数\_获取**IOCTL\_AVC\_类 i/o 控制代码\_的信息函数代码。

此结构定义 AV/C 命令请求的常用组件。 它包含请求的操作码和操作数，以及响应的操作码和操作数（完成后）。 操作数列表的大小固定为指定了单字节子单位地址的操作数的最大允许数目。 如果以任何方式扩展了子单位地址，则会相应地减少允许的最大操作数字节数。

在填写参数之前，此结构的建议使用是结构（使用**RtlZeroMemory**）的第一个。

此名称必须以 IRQL = 被动\_级别进行调用。

### <a name="see-also"></a>另请参阅

[**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)， [**AvcCommandType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavccommandtype)， [**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)， [**AVC\_函数\_查找\_对等\_do**](avc-function-find-peer-do.md)， [**AVC\_函数\_对等\_执行\_列表**](avc-function-peer-do-list.md)，[**AVC\_函数\_获取\_子单位\_信息**](avc-function-get-subunit-info.md)

 

 





