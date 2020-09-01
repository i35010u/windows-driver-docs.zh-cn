---
title: AVC \_ 函数 \_ 获取 \_ PIN \_ 计数
description: AVC \_ 函数 \_ 获取 \_ PIN \_ 计数
ms.assetid: fb455843-c979-479c-ba7c-f84875a9ba6f
keywords:
- AVC_FUNCTION_GET_PIN_COUNT 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_PIN_COUNT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a92bf97614242fecdf1f12ce92cb24428da1c7b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188475"
---
# <a name="avc_function_get_pin_count"></a>AVC \_ 函数 \_ 获取 \_ PIN \_ 计数


## <span id="ddk_avc_function_get_pin_count_ks"></span><span id="DDK_AVC_FUNCTION_GET_PIN_COUNT_KS"></span>


**AVC \_ 函数 \_ 获取 \_ PIN \_ 计数**函数代码获取底层子单位设备支持的 pin 数目。

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

此函数使用 AVC **PinCount** \_ MULTIFUNC IRB 结构的 PinCount 成员 \_ ，如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    AVC_PIN_COUNT PinCount;
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
此成员的 **函数** submember 必须设置为 AVC 函数从 AVC 函数枚举 ** \_ \_ 获取 \_ PIN \_ 计数** \_ 。

<span id="PinCount"></span><span id="pincount"></span><span id="PINCOUNT"></span>**PinCount**  
指定从函数返回时，AV/C 设备上的 pin 数目。

*avc.sys*的虚拟实例不支持此函数代码。

此名称必须以 IRQL = 被动 \_ 级别调用。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC \_ PIN \_ 计数**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_count)， [**AVC \_ 函数**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

