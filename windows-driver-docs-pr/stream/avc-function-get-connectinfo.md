---
title: AVC \_ 函数 \_ GET \_ CONNECTINFO
description: AVC \_ 函数 \_ GET \_ CONNECTINFO
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
ms.openlocfilehash: f76f6d783172baaf22245457f6d1977d168a1139
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830921"
---
# <a name="avc_function_get_connectinfo"></a>AVC \_ 函数 \_ GET \_ CONNECTINFO


## <span id="ddk_avc_function_get_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_GET_CONNECTINFO_KS"></span>


AVC \_ 函数 \_ 获取 \_ 连接 \_ 信息函数代码获取每个 pin ID 的 AVCPRECONNECTINFO 结构， (从零开始) 偏移量。

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
<td><p>当 IRP 完成状态为 STATUS_REQUEST_ABORTED 时立即中止。 这表明设备已被删除或在1394总线上不再可用。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_ *</p></td>
<td><p>任何其他返回代码指示出现超出 AV/C 协议范围的错误或警告。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>注释

此函数使用 AVC **PreConnectInfo** \_ MULTIFUNC IRB 结构的 PreConnectInfo 成员 \_ ，如下所示。

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

AVC \_ PRECONNECT INFO 结构的成员如下 \_ 所示：

```cpp
typedef struct _AVC_PRECONNECT_INFO {
    IN ULONG PinId
    OUT AVCPRECONNECTINFO ConnectInfo;
} AVC_PRECONNECT_INFO, *PAVC_PRECONNECT_INFO;
```

### <a name="requirements"></a>要求

**标头：** 在 *avc* 中声明。 包括 *avc*。

### <a name="avc_multifunc_irb-input"></a>AVC \_ MULTIFUNC \_ IRB 输入

**通用**  
此成员的 **函数** submember 必须设置为 **AVC \_ 函数 \_ GET \_ CONNECTINFO** from AVC \_ 函数枚举。

<span id="ConnectInfo"></span><span id="connectinfo"></span><span id="CONNECTINFO"></span>**ConnectInfo**  
指定 AV/C 设备的连接信息。

*avc.sys* 的虚拟实例不支持此函数代码。

如果子单元驱动程序负责创建 KSPIN 描述符结构中包含的数据范围，则它必须使用此函数 \_ 。 AVCPRECONNECTINFO 结构将追加到 PC 外部连接的 **DataRanges** 成员。

此名称必须以 IRQL = 被动 \_ 级别调用。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC \_ PRECONNECT \_ INFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_preconnect_info)， [**AVCPRECONNECTINFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)， [**AVC \_ FUNCTION**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

