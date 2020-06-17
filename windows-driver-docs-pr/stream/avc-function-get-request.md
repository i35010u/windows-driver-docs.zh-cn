---
title: AVC \_ 函数 \_ GET \_ 请求
description: AVC \_ 函数 \_ GET \_ 请求
ms.assetid: b29df7a8-782b-4014-b47e-7cf917f8e99d
keywords:
- AVC_FUNCTION_GET_REQUEST 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_REQUEST
api_type:
- NA
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6ff4a57c1a3f97a7b0a9046481fba9c77b4ef2b8
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812449"
---
# <a name="avc_function_get_request"></a>AVC \_ 函数 \_ GET \_ 请求

**AVC \_ 函数 \_ GET \_ REQUEST**函数代码用于注册，以接收 AV/C 单元和子发送请求。

## <a name="io-status-block"></a>I/o 状态块

此函数始终将**Irp- &gt; IoStatus**设置为 "挂起" 状态 \_ 。

## <a name="comments"></a>注释

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

## <a name="requirements"></a>要求

**标头：** 在*avc*中声明。 包括*avc*。

## <a name="avc_command_irb-input"></a>AVC \_ 命令 \_ IRB 输入

**通用**
  
此成员的**函数**submember 必须设置为**AVC \_ 函数 \_ GET \_ REQUEST** from AVC \_ 函数枚举。

**SubunitAddrFlag**
  
仅在注册接收单元命令时使用。 将此项设置为1，并在**SubunitAddr**参数中提供单元地址。 请注意，对于子请求，在完成时，此参数设置为1， **SubunitAddr**参数指向包含此虚拟子实例实例的子地址的内存。 调用方可以访问此非分页内存，但不得尝试释放它。

**AlternateOpcodesFlag**
  
仅在注册接收单元命令时使用。 将此项设置为1，并在**AlternateOpcodes**参数中提供调用方支持的操作码列表。

**TimeoutFlag**
  
已忽略。

**RetryFlag**
  
已忽略。

**CommandType**
  
在输入中被忽略。 在输出时， **CommandType**成员设置为**AvcCommandType**枚举中的值之一。

**ResponseCode**
  
对于请求被忽略。

**SubunitAddr**
  
仅在注册接收单元命令时使用。 将此设置为非分页内存地址，该地址包含按**AV/C**数字接口命令集 "常规规范，Rev 3.0 （0xff）" 部分5.3.3 编码的单元地址。 可以在[1394 商业协会](https://1394ta.org/library-2/)网站上找到此规范。 请注意，对于子请求，在完成时，将指向包含此虚拟子实例的子地址的内存。 调用方可以访问此非分页内存，但不得尝试释放它。

**AlternateOpcodes**
  
仅在注册接收单元命令时使用。 将此设置为包含调用方支持的单元操作码列表的非分页内存的地址。 操作码列表的第一个字节是要跟踪的操作码的计数（相当于字节数）。 包含备用操作码列表的内存的总长度为**AlternateOpcodes** \[ 0 \] + 1。

**超时**
  
已忽略。

**重试**
  
已忽略。

**操作码**
  
输入时忽略。 输出时，这包含 AV/C 单元操作码。 这是通过**AlternateOpcodes**指定的操作码之一。

**OperandLength**
  
输入时忽略。 在输出上，此值设置为请求使用的操作数列表中的字节数。

**个数**
  
输入时忽略。 在输出时，此参数包含请求的操作数列表。

**NodeAddress**
  
输入时忽略。 在输出上，此设置为请求源的节点地址。 发送响应时使用此参数（有关详细信息，请参阅[**AVC \_ FUNCTION \_ SEND \_ response**](avc-function-send-response.md)）。

**代系**
  
输入时忽略。 在输出时，此项设置为在节点地址被视为有效时强制执行的生成计数。 发送响应时使用此参数（有关详细信息，请参阅[**AVC \_ FUNCTION \_ SEND \_ response**](avc-function-send-response.md)）。

在 GUID \_ AVC \_ 类设备接口的上下文中， **AVC \_ 函数 \_ GET \_ REQUEST**函数代码用于注册以仅接收 AV/C 单元请求（而不是子请求）。 此函数通常由的筛选器驱动程序（ *avc.sys* FDO）用于支持对等设备功能（也就是说，处理来自非虚拟堆栈的目标设备的单元请求）。 尽管不会阻止子工作区驱动程序注册来处理单元请求，但注册以支持相同单元操作码的子源驱动程序实例必须彼此合作，才能共享状态信息。 *Avc.sys*不直接支持对同一单元操作码进行多个注册。

此函数使用 AVC \_ 命令 \_ IRB 结构。 此结构定义 AV/C 命令请求的常用组件。 唯一有效的输入参数是**SubunitAddrFlag**、 **AlternateOpcodesFlag**、 **AlternateOpcodes**和**SubunitAddr**，都是必需的。 **AlternateOpcodes**必须指向包含调用方支持的单元操作码列表的缓冲区。 **SubunitAddr**必须指向包含单位地址（0xff）的缓冲区。

对于*avc.sys*的虚拟实例（即，注册 GUID \_ virtual \_ AVC \_ 类设备接口的实例） **AVC \_ 函数 \_ GET \_ 请求**用于注册以接收 AV/C 单元和子发送请求。 上层筛选器驱动程序（虚拟*avc.sys* FDO）通常注册来处理单元请求，而子单位驱动程序则注册来处理其特定类型的子单位的请求。 尽管不会阻止子工作区驱动程序注册来处理单元请求，但注册以支持相同单元操作码的子源驱动程序实例必须彼此合作，才能共享状态信息。 *Avc.sys*不直接支持对同一单元操作码进行多个注册。

在注册接收特定于子请求的请求时，子源驱动程序不会设置任何输入参数。

此函数始终返回 \_ "挂起" 状态，因此必须在完成例程中执行任何处理。 完成后，AVC \_ 命令 \_ IRB 结构将保存请求的操作码和操作数。 AV/C 协议要求在100ms 中发送响应。 这可以通过使用**AVC \_ 函数 \_ SEND \_ RESPONSE**函数在完成例程中完成。

如果第一个响应使用**AVC \_ 响应 \_ 过渡**代码（来自**AvcResponseType**枚举），则需要跟进处理。 在后续响应中，必须使用完成**AVC \_ 函数 \_ GET \_ 请求**原始函数时获得的**NodeAddress**和**生成**成员。 在任何情况下，都应在从初始**AVC \_ 函数 \_ 发送 \_ 响应**完成例程返回之前提交下一个**AVC \_ 函数 \_ GET \_ 请求**函数，以便可以收到下一个单位请求。

在填写参数之前，此结构的建议使用是结构（使用**RtlZeroMemory**）的第一个。

此函数代码可在 IRQL <= 调度级别调用 \_ 。

### <a name="see-also"></a>另请参阅

[**AVC \_ 函数 \_ 发送 \_ 响应**](avc-function-send-response.md)

[**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)

[**AVC \_ 函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

[**RtlZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)
