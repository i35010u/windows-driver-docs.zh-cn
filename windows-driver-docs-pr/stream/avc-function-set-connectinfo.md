---
title: AVC \_ 函数 \_ 集 \_ CONNECTINFO
description: AVC \_ 函数 \_ 集 \_ CONNECTINFO
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
ms.openlocfilehash: f29bc564a2422ecc8a6a750850996e1edb781bf7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801237"
---
# <a name="avc_function_set_connectinfo"></a>AVC \_ 函数 \_ 集 \_ CONNECTINFO


## <span id="ddk_avc_function_set_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_SET_CONNECTINFO_KS"></span>


AVC \_ 函数 \_ 集 \_ 连接 \_ 信息函数代码为每个 pin ID 设置 AVCCONNECTINFO 结构， (从零开始) 偏移量。

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

此函数使用 AVC **SetConnectInfo** \_ MULTIFUNC IRB 结构的 SetConnectInfo 成员 \_ ，如下所示。

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

**标头：** 在 *avc* 中声明。 包括 *avc*。

### <a name="avc_multifunc_irb-input"></a>AVC \_ MULTIFUNC \_ IRB 输入

**通用**  
此成员的 **函数** submember 必须设置为 AVC 函数枚举中的 **AVC \_ 函数 \_ set \_ CONNECTINFO** \_ 。

<span id="SetConnectInfo"></span><span id="setconnectinfo"></span><span id="SETCONNECTINFO"></span>**SetConnectInfo**  
指定 AV/C 设备的连接信息。

*avc.sys* 的虚拟实例不支持此函数代码。

如果子单位驱动程序提供了交叉处理程序，则它必须使用此函数。 CONNECTINFO 结构中包含的 AVCCONNECTINFO 结构 (\_ \_) 派生自 AVCPRECONNECTINFO 结构，该结构追加到传递给交集处理程序的数据范围。

确定数据区域兼容后，相交处理程序会生成 AVCCONNECTINFO 结构。 此结构将追加到生成的数据格式，并且还将发送到 *avc.sys*。 如果以后再传递建议的数据格式，则不重要，因为 *avc.sys* 仅缓存一个 AVCCONNECTINFO 结构。

此名称必须以 IRQL = 被动 \_ 级别调用。

### <a name="see-also"></a>另请参阅

[**AVC \_MULTIFUNC \_ IRB**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC \_ SETCONNECT \_ INFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avc_setconnect_info)， [**AVCCONNECTINFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)， [**AVC \_ FUNCTION**](/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)， [**AV/C 交集处理程序**](/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)

 

