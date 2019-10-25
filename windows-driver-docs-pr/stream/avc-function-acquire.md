---
title: AVC\_函数\_获取
description: AVC\_函数\_获取
ms.assetid: c250d800-1777-44c0-8902-09017eb46c78
keywords:
- AVC_FUNCTION_ACQUIRE 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_ACQUIRE
api_type:
- NA
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1c791ee2fed6aeb71aadd6cdb3f47b51ef4cfda2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845162"
---
# <a name="avc_function_acquire"></a>AVC\_函数\_获取

**AVC\_函数\_获取**函数代码会导致*AVC*建立缓存的 AVCCONNECTINFO 值建议的任何连接。

## <a name="io-status-block"></a>I/O 状态块

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

## <a name="comments"></a>备注

此函数使用 AVC\_MULTIFUNC\_IRB 结构的**PinId**成员，如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PIN_ID PinId;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

## <a name="requirements"></a>要求

**标头：** 在*avc*中声明。 包括*avc*。

## <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**常见问题解答**  

此成员的**函数**submember 必须设置为**AVC\_函数\_** 从 AVC\_函数枚举获取。

**PinId**  

指定要为其获取连接的 pin 的偏移量（或 ID）。

*Avc*的虚拟实例不支持此函数代码。

当 pin 变为活动状态时，子单位驱动程序必须使用此函数。

此名称必须以 IRQL = 被动\_级别进行调用。

## <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)

[**AVC\_PIN\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_id)

[**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)
