---
title: AVC\_函数\_获取\_PIN\_计数
description: AVC\_函数\_获取\_PIN\_计数
ms.assetid: fb455843-c979-479c-ba7c-f84875a9ba6f
keywords:
- AVC_FUNCTION_GET_PIN_COUNT 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_PIN_COUNT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d71361da9d9c7675e0804f02f25e0ad8f2b35bad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386742"
---
# <a name="avcfunctiongetpincount"></a>AVC\_函数\_获取\_PIN\_计数


## <span id="ddk_avc_function_get_pin_count_ks"></span><span id="DDK_AVC_FUNCTION_GET_PIN_COUNT_KS"></span>


**AVC\_函数\_获取\_PIN\_计数**函数代码会获取 pin 基础的子单元设备支持的数目。

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

此函数使用**PinCount**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

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

**标头：** 在中声明*avc.h*。 包括*avc.h*。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_获取\_PIN\_计数**从 AVC\_函数枚举。

<span id="PinCount"></span><span id="pincount"></span><span id="PINCOUNT"></span>**PinCount**  
从函数返回时 AV/C 设备上指定的 pin 的数量。

个虚拟实例不支持此函数代码*avc.sys*。

这必须在调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb)， [ **AVC\_PIN\_计数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_pin_count)， [ **AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)

 

 





