---
title: OID_PD_OPEN_PROVIDER
description: NDIS 协议或筛选器驱动程序将 OID_PD_OPEN_PROVIDER 的对象标识符 (OID) 方法请求发送到 PD 支持的微型端口驱动程序来访问微型端口驱动程序的 PDPI 提供程序对象中的 PD 功能。
ms.assetid: B13E0FAC-A179-4785-9B39-CB498064947B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PD_OPEN_PROVIDER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aeb4fb1808bde918932b081e456df3254aa4718f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554748"
---
# <a name="oidpdopenprovider"></a>OID\_PD\_打开\_提供程序


NDIS 协议或筛选器驱动程序将发送对象标识符 (OID) 方法请求的 OID\_PD\_打开\_支持 PD 的微型端口驱动程序的提供程序来访问微型端口驱动程序的 PDPI 提供程序对象中的 PD 功能. 所有支持 PD 的微型端口驱动程序必须处理此 OID 请求。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向缓冲区的指针。 此缓冲区包含以下数据：

-   [ **NDIS\_PD\_打开\_提供程序\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn931842)结构

<a name="remarks"></a>备注
-------

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)

[**NDIS\_PD\_OPEN\_PROVIDER\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn931842)

[NDIS\_状态\_PD\_当前\_配置](https://msdn.microsoft.com/library/windows/hardware/dn931850)

[OID\_PD\_关闭\_提供程序](oid-pd-close-provider.md)

 

 




