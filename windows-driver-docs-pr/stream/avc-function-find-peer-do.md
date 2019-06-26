---
title: AVC\_函数\_查找\_对等方\_执行操作
description: AVC\_函数\_查找\_对等方\_执行操作
ms.assetid: a21dde69-f005-4782-97d9-095a57b2b1a5
keywords:
- AVC_FUNCTION_FIND_PEER_DO 流式处理媒体设备
topic_type:
- apiref
api_name:
- AVC_FUNCTION_FIND_PEER_DO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1fee2d0e0c39508038a39cabc28e1f63e80eaf6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386748"
---
# <a name="avcfunctionfindpeerdo"></a>AVC\_函数\_查找\_对等方\_执行操作


## <span id="ddk_avc_function_find_peer_do_ks"></span><span id="DDK_AVC_FUNCTION_FIND_PEER_DO_KS"></span>


**AVC\_函数\_查找\_对等方\_执行**函数代码查找非虚拟*avc.sys*实例。

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
<td><p>STATUS_UNSUCCESSFUL</p></td>
<td><p>非虚拟实例<em>avc.sys</em>找不到</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INVALID_GENERATION</p></td>
<td><p>总线重置发生之前找不到的设备对象引用。 获取新 NodeAddress，然后重试。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>备注

此函数使用**PeerLocator**成员的 AVC\_MULTIFUNC\_IRB 结构如下所示。

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

**标头：** 在中声明*avc.h*。 包括*avc.h*。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 输入

**Common**  
**函数**必须设置为此成员的子**AVC\_函数\_查找\_对等方\_执行**从 AVC\_函数枚举。

<span id="PeerLocator"></span><span id="peerlocator"></span><span id="PEERLOCATOR"></span>**PeerLocator**  
指定的非虚拟 （对等） 实例*avc.sys*。

此函数查找非虚拟*avc.sys*实例根据设备的节点地址它表示。 如果找不到实例，IRP 完成时的状态\_未成功。 调用方所在实例后，可能会提交任何 GUID\_AVC\_类设备接口请求通过对象。 调用方必须释放对此对象的引用 (通过**ObDereferenceObject**) 时已完成，但它。

可能在 IRQL 调用此函数代码&lt;= 调度\_级别。

### <a name="see-also"></a>请参阅

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb)， [ **AVC\_对等方\_执行\_定位器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_peer_do_locator)， [**AVC\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)， [ **ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)

 

 





