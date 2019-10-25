---
title: AVC\_函数\_查找\_对等\_DO
description: AVC\_函数\_查找\_对等\_DO
ms.assetid: a21dde69-f005-4782-97d9-095a57b2b1a5
keywords:
- AVC_FUNCTION_FIND_PEER_DO 流媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_FIND_PEER_DO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07c47c7665a154c4c404567403c3ad6768795056
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845160"
---
# <a name="avc_function_find_peer_do"></a>AVC\_函数\_查找\_对等\_DO


## <span id="ddk_avc_function_find_peer_do_ks"></span><span id="DDK_AVC_FUNCTION_FIND_PEER_DO_KS"></span>


**AVC\_函数\_FIND\_对等\_DO**函数代码查找非虚拟的*AVC*实例。

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
<td><p>STATUS_UNSUCCESSFUL</p></td>
<td><p>找不到<em>avc</em>的非虚拟实例</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INVALID_GENERATION</p></td>
<td><p>在找不到设备对象引用之前发生了总线重置。 获取新 NodeAddress，然后重试。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>备注

此函数使用 AVC\_MULTIFUNC\_IRB 结构的**PeerLocator**成员，如下所示。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PEER_DO_LOCATOR PeerLocator;
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
此成员的**函数**submember 必须设置为**AVC\_函数\_FIND\_对等\_** 从 AVC\_函数枚举。

<span id="PeerLocator"></span><span id="peerlocator"></span><span id="PEERLOCATOR"></span>**PeerLocator**  
指定*avc*的非虚拟（对等）实例。

此函数根据其表示的设备的节点地址，查找非虚拟*avc*实例。 如果找不到实例，则 IRP 完成，状态状态\_不成功。 定位实例后，调用方可以通过对象提交任何 GUID\_AVC\_类设备接口请求。 完成后，调用方必须释放对此对象的引用（通过**ObDereferenceObject**）。

此函数代码可在 IRQL &lt;= 调度\_级别调用。

### <a name="see-also"></a>另请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)， [**AVC\_对等\_DO\_定位器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_peer_do_locator)， [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)， [**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)

 

 





