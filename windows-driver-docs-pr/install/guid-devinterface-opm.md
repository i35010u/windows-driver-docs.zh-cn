---
title: GUID_DEVINTERFACE_OPM
description: GUID_DEVINTERFACE_OPM
ms.assetid: bd999b09-d531-4b89-a306-83e1ca7cac64
keywords:
- GUID_DEVINTERFACE_OPM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_OPM
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 554943cb78fa3690d74e5dae11538f048dc42210
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546511"
---
# <a name="guiddevinterfaceopm"></a>GUID_DEVINTERFACE_OPM


GUID_DEVINTERFACE_OPM[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)显示适配器驱动程序的上下文中运行，为定义[Windows Vista 显示器驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff570593)和支持输出保护监视子设备管理 (OPM)。

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
<td align="left"><p>GUID_DEVINTERFACE_OPM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{BF4672DE-6B4E-4BE4-A325-68A91EA49C09}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

驱动程序注册通知的操作系统和应用程序的 OPM 设备接口存在此设备接口类的实例。

如果显示微型端口驱动程序支持直接调用 OPM 接口的这[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)，内核模式组件可以通过调用微型端口驱动程序检索直接调用接口[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)函数并提供 GUID_DEVINTERFACE_OPM 指定接口类型。

OPM 有关的信息，请参阅[支持输出保护管理器](https://msdn.microsoft.com/library/windows/hardware/ff569879)。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Dispmprt.h （包括 Dispmprt.h）</td>
</tr>
</tbody>
</table>

 

 





