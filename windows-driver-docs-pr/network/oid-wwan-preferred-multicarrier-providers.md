---
title: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 用于设置或查询的首选多运营商网络提供商列表。 多运营商提供程序是一种是可以将设置为主页的提供程序。
ms.assetid: BA78E0B9-1B57-412C-83E7-328F8304C82D
ms.date: 08/08/2017
keywords: -OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 753dd6da2f49bc748e8d8f21949a162f32918746
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360761"
---
# <a name="oidwwanpreferredmulticarrierproviders"></a>OID\_WWAN\_PREFERRED\_多\_提供程序


OID\_WWAN\_PREFERRED\_多\_提供程序是用于*设置*或者*查询*首选多运营商网络提供程序的列表。 多运营商提供程序是指可以是*设置*作为主提供程序。

这两*设置*并*查询*支持请求。 微型端口驱动程序必须处理*设置*并*查询*请求一开始，以异步方式返回 NDIS\_状态\_指示\_所需的原始请求和更高版本发送[ **NDIS\_状态\_WWAN\_首选\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)状态通知包含[ **NDIS\_WWAN\_首选\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)结构。

微型端口驱动程序应设置**PreferredListHeader.ElementType**成员添加到**WwanStructProvider2**并**PreferredListHeader.ElementCount**成员添加到响应 OID 时在列表中的提供程序的数字\_WWAN\_PREFERRED\_提供程序*查询*请求。 在中返回的多运营商提供程序*查询*必须能够在首选多运营商列表返回到服务的时间设置为主页的提供程序。

微型端口驱动程序应设置**PreferredListHeader.ElementType**成员添加到**WwanStructProvider2**并**PreferredListHeader.ElementCount**到 0 时，成员响应的 OID\_WWAN\_PREFERRED\_提供程序*设置*请求。

微型端口应该设置出错**uStatus**成员的 NDIS\_WWAN\_首选\_多\_失败状态提供程序结构和**PreferredListHeader.ElementCount**为 0 和**PreferredLIstHeader.ElementType**到**WwanStructProvider2**。

**Rssi**并**ErrorRate** WWAN 成员\_如果可用，应设置 PROVIDER2 结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>版本：支持 Windows 8 和更高版本的 Windows 中。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_PREFERRED\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

[**NDIS\_状态\_WWAN\_PREFERRED\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)

[MB 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




