---
title: AVC\_函数\_设置\_CONNECTINFO
description: AVC\_函数\_设置\_CONNECTINFO
ms.assetid: e97b525a-2236-44a9-9d49-dc0df760f21e
keywords:
- AVC_FUNCTION_SET_CONNECTINFO 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_SET_CONNECTINFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23d6016942535b915b4bd9654b80b4beee1d9f08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547062"
---
# <a name="avcfunctionsetconnectinfo"></a>AVC\_函数\_设置\_CONNECTINFO


## <span id="ddk_avc_function_set_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_SET_CONNECTINFO_KS"></span>


AVC\_函数\_设置\_CONNECT\_信息函数代码设置 AVCCONNECTINFO 结构为每个 pin ID （从零开始的偏移量）。

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

此函数使用**SetConnectInfo**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_SETCONNECT_INFO SetConnectInfo;
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
**函数**必须设置为此成员的子**AVC\_函数\_设置\_CONNECTINFO**从 AVC\_函数枚举。

<span id="SetConnectInfo"></span><span id="setconnectinfo"></span><span id="SETCONNECTINFO"></span>**SetConnectInfo**  
指定 C AV/设备的连接信息。

个虚拟实例不支持此函数代码*avc.sys*。

如果提供了一个处理程序，intersect 子单元驱动程序必须使用此函数。 AVCCONNECTINFO 结构 (包含在 AVC\_设置\_CONNECTINFO 结构) 追加到传递给 intersect 处理程序的数据范围的 AVCPRECONNECTINFO 结构中派生。

确定后，数据范围都兼容，intersect 处理程序生成 AVCCONNECTINFO 结构。 此结构将追加到生成的数据格式，并且也将发送到*avc.sys*。 并不重要如果建议的数据格式向上传递的一个更好更高版本，因为*avc.sys*只是缓存一个 AVCCONNECTINFO 结构。

这必须在调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177)， [ **AVC\_为表示\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff554192)， [ **AVCCONNECTINFO**](https://msdn.microsoft.com/library/windows/hardware/ff554101)， [ **AVC\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554145)， [ **AV/C 相交处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff556379)

 

 





