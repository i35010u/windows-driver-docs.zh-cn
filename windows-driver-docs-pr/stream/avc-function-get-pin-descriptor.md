---
title: AVC\_函数\_获取\_PIN\_描述符
description: AVC\_函数\_获取\_PIN\_描述符
ms.assetid: 1a02c328-e908-4125-abe7-4db9970ac86a
keywords:
- AVC_FUNCTION_GET_PIN_DESCRIPTOR 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_PIN_DESCRIPTOR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f72b8c9b1a6cbfdbd8da0ca5fdbb52e77463ea0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576549"
---
# <a name="avcfunctiongetpindescriptor"></a>AVC\_函数\_获取\_PIN\_描述符


## <span id="ddk_avc_function_get_pin_descriptor_ks"></span><span id="DDK_AVC_FUNCTION_GET_PIN_DESCRIPTOR_KS"></span>


**AVC\_函数\_获取\_PIN\_描述符**函数代码为每个 pin ID （从零开始的偏移量） 将获取 pin 描述符。

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
<td><p>发出请求，但未收到响应之前所有的超时和重试处理已完成。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>立即中止 STATUS_REQUEST_ABORTED IRP 完成状态时。 这表示设备已删除或不再可用的 1394年总线上。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_*</p></td>
<td><p>任何其他返回代码指示错误或警告发生了超出范围的 AV/C 协议。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>备注

此函数使用**PinDescriptor**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

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

**标头：** 在中声明*avc.h*。 包括*avc.h*。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_获取\_PIN\_描述符**从 AVC\_函数的枚举。

<span id="PinDescriptor"></span><span id="pindescriptor"></span><span id="PINDESCRIPTOR"></span>**PinDescriptor**  
AV/C 子单元设备上指定的 pin 的描述。

个虚拟实例不支持此函数代码*avc.sys*。

除了 pin 描述符，此函数可返回 intersect 处理程序和不透明的上下文值与 intersect 处理程序关联的地址。 如果 intersect 处理程序成员**NULL**，子单元驱动程序必须提供 intersect 处理程序。 如果不是 intersect 处理程序成员**NULL**、 提供 intersect 处理程序和驱动程序可能会使用它。

*Avc.sys*永远不会提供数据重叠，但筛选器驱动程序 (例如， *avcstrm.sys*) 进行填充，因为正在通过堆栈中将在请求完成备份。

这必须在调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177)， [ **AVC\_PIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff554185)， [ **AVC\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554145)， [ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)， [ **AV/C 相交处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff556379)

 

 





