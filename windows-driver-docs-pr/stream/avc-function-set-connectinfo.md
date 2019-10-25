---
title: AVC\_函数\_集\_CONNECTINFO
description: AVC\_函数\_集\_CONNECTINFO
ms.assetid: e97b525a-2236-44a9-9d49-dc0df760f21e
keywords:
- AVC_FUNCTION_SET_CONNECTINFO 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_SET_CONNECTINFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27f3d40afa90e1a607b246731dcd1a6d67095c85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845070"
---
# <a name="avc_function_set_connectinfo"></a>AVC\_函数\_集\_CONNECTINFO


## <span id="ddk_avc_function_set_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_SET_CONNECTINFO_KS"></span>


AVC\_函数\_集\_连接\_信息函数代码为每个 pin ID 设置 AVCCONNECTINFO 结构（从零开始）。

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

此函数使用 AVC\_MULTIFUNC\_IRB 结构的**SetConnectInfo**成员，如下所示。

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

**标头：** 在*avc*中声明。 包括*avc*。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**常见问题解答**  
必须将此成员的**函数**submember 设置为**AVC\_函数\_** 通过 AVC\_函数枚举设置\_CONNECTINFO。

<span id="SetConnectInfo"></span><span id="setconnectinfo"></span><span id="SETCONNECTINFO"></span>**SetConnectInfo**  
指定 AV/C 设备的连接信息。

*Avc*的虚拟实例不支持此函数代码。

如果子单位驱动程序提供了交叉处理程序，则它必须使用此函数。 AVCCONNECTINFO 结构（包含在 AVC\_集\_CONNECTINFO 结构中）派生自 AVCPRECONNECTINFO 结构，该结构追加到传递给交集处理程序的数据范围。

确定数据区域兼容后，相交处理程序会生成 AVCCONNECTINFO 结构。 此结构将追加到生成的数据格式，并且还将发送到*avc*。 如果以后再传递建议的数据格式，则不重要，因为*avc*仅缓存一个 AVCCONNECTINFO 结构。

此名称必须以 IRQL = 被动\_级别进行调用。

### <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC\_SETCONNECT\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_setconnect_info)， [**AVCCONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)， [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)， [**AV/C 交集处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)

 

 





