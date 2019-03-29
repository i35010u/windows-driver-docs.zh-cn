---
title: OID_GEN_HD_SPLIT_PARAMETERS
description: 作为一组 NDIS 和基础驱动程序或用户模式应用程序使用 OID_GEN_HD_SPLIT_PARAMETERS OID 来设置当前的标头数据拆分微型端口适配器的设置。
ms.assetid: 1b33c601-4302-4f63-8265-b75889b42d42
ms.date: 08/08/2017
keywords: -OID_GEN_HD_SPLIT_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b593f58e8f3b110ece32602633eccd773de2540c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564985"
---
# <a name="oidgenhdsplitparameters"></a>OID\_GEN\_HD\_拆分\_参数


作为一组 NDIS 和基础驱动程序或用户模式应用程序使用 OID\_GEN\_HD\_拆分\_参数 OID，设置当前标头数据拆分微型端口适配器的设置。 NDIS 6.1 和更高版本的微型端口驱动程序提供标头数据拆分服务必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含[ **NDIS\_HD\_拆分\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565701)结构。

NDIS 可能设置 OID\_GEN\_HD\_拆分\_参数 OID 时 NDIS 5。*x*协议驱动程序将绑定到 NDIS 6.1 微型端口。 NDIS 然后再将它传递到微型端口驱动程序处理此 OID，并更新微型端口适配器 **\*HeaderDataSplit**关键字，如果需要进行标准化。 如果禁用了标头数据拆分，则 NDIS 不向微型端口适配器发送此 OID。

NDIS 将向此 OID 微型端口驱动程序仅当标头数据拆分已启用与的 NDIS\_HD\_拆分\_启用\_标头\_数据\_中的拆分标志[**NDIS\_HD\_拆分\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)在微型端口初始化过程中的结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>支持 NDIS 6.1 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_HD\_SPLIT\_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff565694)

[**NDIS\_HD\_SPLIT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff565701)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




