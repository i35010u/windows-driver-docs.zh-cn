---
title: KSCATEGORY_BDA_RECEIVER_COMPONENT
description: KSCATEGORY_BDA_RECEIVER_COMPONENT
ms.assetid: f160662e-651c-444f-aa82-cfc73c19e41d
keywords:
- KSCATEGORY_BDA_RECEIVER_COMPONENT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_RECEIVER_COMPONENT
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 88003a671cda4c63eb9f076d50cd068fdb2990a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377331"
---
# <a name="kscategorybdareceivercomponent"></a>KSCATEGORY_BDA_RECEIVER_COMPONENT


KSCATEGORY_BDA_RECEIVER_COMPONENT[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 中为接收方的功能类别[广播驱动程序体系结构](https://msdn.microsoft.com/library/windows/hardware/ff556573) (BDA)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_BDA_RECEIVER_COMPONENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{FD0A5AF4-B41D-11d2-9C95-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BDA 设备的驱动程序注册 KSCATEGORY_BDA_RECEIVER_COMPONENT 向操作系统指示设备支持 BDA 接收方筛选器的实例。

详细了解 KS 功能类别 BDA 接收方筛选器，请参阅[常见控制节点和筛选器](https://msdn.microsoft.com/library/windows/hardware/ff557718)，[启动 BDA 微型驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff568223)，和[BDA 筛选器类别 Guid](https://msdn.microsoft.com/library/windows/hardware/ff556521).

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows XP、 DirectX 9.0 a 安装，Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

 

 





