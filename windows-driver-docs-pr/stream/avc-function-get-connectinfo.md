---
title: AVC\_函数\_获取\_CONNECTINFO
description: AVC\_函数\_获取\_CONNECTINFO
ms.assetid: d4230024-a765-47f0-9958-9f71761f7b85
keywords:
- AVC_FUNCTION_GET_CONNECTINFO 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_CONNECTINFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 799b48657c5e03ccec5c538426d7d01ad68a3119
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845158"
---
# <a name="avc_function_get_connectinfo"></a>AVC\_函数\_获取\_CONNECTINFO


## <span id="ddk_avc_function_get_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_GET_CONNECTINFO_KS"></span>


AVC\_函数\_获取\_连接\_信息函数代码获取每个 pin ID 的 AVCPRECONNECTINFO 结构（与零偏移量）。

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

此函数使用 AVC\_MULTIFUNC\_IRB 结构的**PreConnectInfo**成员，如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PRECONNECT_INFO PreConnectInfo;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

AVC\_PRECONNECT\_INFO 结构的成员如下所示：

```cpp
typedef struct _AVC_PRECONNECT_INFO {
    IN ULONG PinId
    OUT AVCPRECONNECTINFO ConnectInfo;
} AVC_PRECONNECT_INFO, *PAVC_PRECONNECT_INFO;
```

### <a name="requirements"></a>要求

**标头：** 在*avc*中声明。 包括*avc*。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**常见问题解答**  
此成员的**函数**submember 必须设置为**AVC\_函数\_** 从 AVC\_函数枚举获取\_CONNECTINFO。

<span id="ConnectInfo"></span><span id="connectinfo"></span><span id="CONNECTINFO"></span>**ConnectInfo**  
指定 AV/C 设备的连接信息。

*Avc*的虚拟实例不支持此函数代码。

如果子单元驱动程序负责创建 KSPIN\_描述符结构中包含的数据范围，则它必须使用此函数。 AVCPRECONNECTINFO 结构将追加到 PC 外部连接的**DataRanges**成员。

此名称必须以 IRQL = 被动\_级别进行调用。

### <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC\_PRECONNECT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_preconnect_info)， [**AVCPRECONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)， [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

 





