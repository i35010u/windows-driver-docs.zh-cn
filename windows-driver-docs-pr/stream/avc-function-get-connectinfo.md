---
title: AVC\_函数\_获取\_CONNECTINFO
description: AVC\_函数\_获取\_CONNECTINFO
ms.assetid: d4230024-a765-47f0-9958-9f71761f7b85
keywords:
- AVC_FUNCTION_GET_CONNECTINFO 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_CONNECTINFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34574ad8c0a8528f750e9a5ce296564517dd540e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524486"
---
# <a name="avcfunctiongetconnectinfo"></a>AVC\_函数\_获取\_CONNECTINFO


## <span id="ddk_avc_function_get_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_GET_CONNECTINFO_KS"></span>


AVC\_函数\_获取\_CONNECT\_信息函数代码为每个 pin ID （从零开始的偏移量） 将获取 AVCPRECONNECTINFO 结构。

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

此函数使用**PreConnectInfo**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

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

成员的 AVC\_PRECONNECT\_信息结构如下所示：

```cpp
typedef struct _AVC_PRECONNECT_INFO {
    IN ULONG PinId
    OUT AVCPRECONNECTINFO ConnectInfo;
} AVC_PRECONNECT_INFO, *PAVC_PRECONNECT_INFO;
```

### <a name="requirements"></a>要求

**标头：** 在中声明*avc.h*。 包括*avc.h*。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_获取\_CONNECTINFO**从 AVC\_函数枚举。

<span id="ConnectInfo"></span><span id="connectinfo"></span><span id="CONNECTINFO"></span>**ConnectInfo**  
指定 C AV/设备的连接信息。

个虚拟实例不支持此函数代码*avc.sys*。

子单元驱动程序必须使用此函数，如果它是负责创建 KSPIN 中包含的数据范围\_描述符结构。 AVCPRECONNECTINFO 结构追加到**DataRanges**连接到 PC 外部的成员。

这必须在调用在 IRQL = 被动\_级别。

### <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177)， [ **AVC\_PRECONNECT\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff554190)， [ **AVCPRECONNECTINFO**](https://msdn.microsoft.com/library/windows/hardware/ff554103)， [ **AVC\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff554145)

 

 





