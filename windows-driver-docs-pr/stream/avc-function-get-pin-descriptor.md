---
title: AVC\_函数\_获取\_PIN\_描述符
description: AVC\_函数\_获取\_PIN\_描述符
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
ms.openlocfilehash: e5f83d98c9ae7493dd6a557554b12dc55c5c0ed5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845084"
---
# <a name="avc_function_get_pin_descriptor"></a>AVC\_函数\_获取\_PIN\_描述符


## <span id="ddk_avc_function_get_pin_descriptor_ks"></span><span id="DDK_AVC_FUNCTION_GET_PIN_DESCRIPTOR_KS"></span>


**AVC\_函数\_获取\_pin\_描述符**函数代码获取每个 pin ID 的固定描述符（从零开始）。

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
<td><p>发出了请求，但在所有超时和重试处理完成之前未收到响应。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>当 IRP 完成状态为 "STATUS_REQUEST_ABORTED" 时立即中止。 这表明设备已被删除或在1394总线上不再可用。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_*</p></td>
<td><p>任何其他返回代码指示出现超出 AV/C 协议范围的错误或警告。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>备注

此函数使用 AVC\_MULTIFUNC\_IRB 结构的**PinDescriptor**成员，如下所示。

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

**标头：** 在*avc*中声明。 包括*avc*。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**常见问题解答**  
必须将此成员的**函数**submember 设置为 AVC\_函数，\_从 AVC\_函数枚举**获取\_PIN\_说明符**。

<span id="PinDescriptor"></span><span id="pindescriptor"></span><span id="PINDESCRIPTOR"></span>**PinDescriptor**  
指定 AV/C 子单位设备上的 pin 说明。

*Avc*的虚拟实例不支持此函数代码。

除了 pin 说明符以外，此函数还可能返回 intersect 处理程序的地址，以及与 intersect 处理程序关联的不透明的上下文值。 如果 intersect 处理程序成员为**NULL**，则子单位驱动程序必须提供交集处理程序。 如果 intersect 处理程序成员不为**NULL**，则将提供交集处理程序，并且驱动程序可以使用该处理程序。

*Avc*绝不会提供数据交集，但筛选器驱动程序（例如*avcstrm*）会在请求通过堆栈完成备份时将其填充。

此名称必须以 IRQL = 被动\_级别进行调用。

### <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC\_PIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_descriptor)， [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)， [**KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)， [**AV/C 交集处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)

 

 





