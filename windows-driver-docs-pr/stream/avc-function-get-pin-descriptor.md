---
title: AVC \_ 函数 \_ 获取 \_ PIN \_ 描述符
description: AVC \_ 函数 \_ 获取 \_ PIN \_ 描述符
ms.assetid: 1a02c328-e908-4125-abe7-4db9970ac86a
keywords:
- AVC_FUNCTION_GET_PIN_DESCRIPTOR 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_PIN_DESCRIPTOR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47692d518d5e4966efd6b041b414276bcb6193e9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186635"
---
# <a name="avc_function_get_pin_descriptor"></a>AVC \_ 函数 \_ 获取 \_ PIN \_ 描述符


## <span id="ddk_avc_function_get_pin_descriptor_ks"></span><span id="DDK_AVC_FUNCTION_GET_PIN_DESCRIPTOR_KS"></span>


**AVC \_ 函数 \_ 获取 \_ pin \_ 描述符**函数代码获取每个 pin ID (从零) 偏移量的固定描述符。

### <a name="io-status-block"></a>I/o 状态块

如果成功，AV/C 协议驱动程序会将 **Irp &gt; IoStatus** 设置为状态 " \_ 成功"。

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
<td><p>STATUS_TIMEOUT</p></td>
<td><p>发出了请求，但在所有超时和重试处理完成之前未收到响应。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>当 IRP 完成状态为 STATUS_REQUEST_ABORTED 时立即中止。 这表明设备已被删除或在1394总线上不再可用。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_ *</p></td>
<td><p>任何其他返回代码指示出现超出 AV/C 协议范围的错误或警告。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>说明

此函数使用 AVC **PinDescriptor** \_ MULTIFUNC IRB 结构的 PinDescriptor 成员 \_ ，如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PIN_DESCRIPTOR PinDescriptor;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

### <a name="requirements"></a>要求

**标头：** 在 *avc*中声明。 包括 *avc*。

### <a name="avc_multifunc_irb-input"></a>AVC \_ MULTIFUNC \_ IRB 输入

**通用**  
此成员的 **函数** submember 必须设置为 AVC 函数从 AVC 函数的枚举 ** \_ \_ 获取 \_ PIN \_ 说明符** \_ 。

<span id="PinDescriptor"></span><span id="pindescriptor"></span><span id="PINDESCRIPTOR"></span>**PinDescriptor**  
指定 AV/C 子单位设备上的 pin 说明。

*avc.sys*的虚拟实例不支持此函数代码。

除了 pin 说明符以外，此函数还可能返回 intersect 处理程序的地址，以及与 intersect 处理程序关联的不透明的上下文值。 如果 intersect 处理程序成员为 **NULL**，则子单位驱动程序必须提供交集处理程序。 如果 intersect 处理程序成员不为 **NULL**，则将提供交集处理程序，并且驱动程序可以使用该处理程序。

*Avc.sys* 绝不会提供数据交集，但筛选器驱动程序 (例如， *avcstrm.sys*) 会在请求通过堆栈完成备份时填充该驱动程序。

此名称必须以 IRQL = 被动 \_ 级别调用。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC \_ 引脚 \_ 描述符**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_descriptor)， [**AVC \_ FUNCTION**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)， [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)， [**AV/C 交集处理程序**](/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)

 

