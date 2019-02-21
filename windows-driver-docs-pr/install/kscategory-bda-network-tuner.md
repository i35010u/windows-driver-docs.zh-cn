---
title: KSCATEGORY_BDA_NETWORK_TUNER
description: KSCATEGORY_BDA_NETWORK_TUNER
ms.assetid: d3f9d393-c8a1-4280-8796-a1de755f9508
keywords:
- KSCATEGORY_BDA_NETWORK_TUNER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_NETWORK_TUNER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 45ce647f797c85d59c883e262cba75015bf38260
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522880"
---
# <a name="kscategorybdanetworktuner"></a>KSCATEGORY_BDA_NETWORK_TUNER


KSCATEGORY_BDA_NETWORK_TUNER[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)为定义[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) 功能类别中的网络调谐器[广播驱动程序体系结构](https://msdn.microsoft.com/library/windows/hardware/ff556573) (BDA)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_BDA_NETWORK_TUNER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{71985F48-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BDA 设备的驱动程序注册 KSCATEGORY_BDA_NETWORK_TUNER 向操作系统指示设备支持 BDA 网络调谐器筛选器的实例。

有关如何在一个 INF 文件中注册此功能的类别的示例，请参阅 INF 文件*BDASwTunerATSC.inf*。 *BDASwTunerATSC.inf*附带 BDA 示例中的泛型调谐器*src\\swtuner\\BDAtuner\\gentuner* WDK 的子目录。

有关网络调谐器筛选器的 KS 功能类别的详细信息，请参阅[常见控制节点和筛选器](https://msdn.microsoft.com/library/windows/hardware/ff557718)并[BDA 筛选器类别 Guid](https://msdn.microsoft.com/library/windows/hardware/ff556521)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows XP、 DirectX 9.0 a 安装，Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

 

 





