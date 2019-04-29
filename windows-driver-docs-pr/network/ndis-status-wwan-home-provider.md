---
title: NDIS_STATUS_WWAN_HOME_PROVIDER
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_HOME_PROVIDER 通知来告知 OID_WWAN_HOME_PROVIDER 完成 MB 服务 \ 160;查询请求。
ms.assetid: a5733c62-be4e-4f86-9639-6addd31baf0c
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_HOME_PROVIDER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2274f406304e95cbd6e30157ee7df839a6ea4001
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354168"
---
# <a name="ndisstatuswwanhomeprovider"></a>NDIS\_状态\_WWAN\_主页\_提供程序


微型端口驱动程序使用 NDIS\_状态\_WWAN\_主页\_关于完成的通知 MB 服务提供程序通知[OID\_WWAN\_主页\_提供程序](oid-wwan-home-provider.md) 查询请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_主页\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567909)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须符合以下规则时响应 OID\_WWAN\_主页\_提供程序查询请求：

-   基于 GSM 的设备：可以检索家庭的提供程序名称从订阅服务器上标识模块 (SIM) 配合使用几种方法，如 EFSPN SIM 中的基本文件 （EFSPN 中定义 3GPP TS 31.102 部分服务提供程序名称下），或从特定于运算符的扩展时 EFSPN 未预配。 应参考获取家庭的提供程序名称、 从 IMSI，提取 MCC mnc 和执行查看向上 GSMA SE.13 数据库中的特定于运算符的要求规范。 如果未设置 EFSPN 检索特定于运算符的家庭提供程序名称时，请联系操作员。 如果 SIM 未配有通过 EFSPN 或任何其他机制的家庭的提供程序名称，微型端口驱动程序应提供程序名称设置为**NULL**。

    SIM 卡的文件系统有关的详细信息，请参阅 3GPP TS 11.11 规范。 如果用户识别模块 （SIM 卡） 中未设置提供程序标识，微型端口驱动程序应返回 WWAN\_状态\_读取\_失败。

-   基于 CDMA 的设备：返回主提供程序名称是必需的。 建议 Ihv 提供此信息在其设备的网络个性化设置。 如果提供程序标识不可用，必须设置为基于 CDMA 的提供程序的微型端口驱动程序**Provider.ProviderId**成员的 NDIS\_WWAN\_主页\_WWAN到提供程序结构\_CDMA\_默认\_提供程序\_id。

微型端口驱动程序必须返回此信息时在设备就绪状态更改为**WwanReadyStateInitialized**并设置格式的 WWAN 的所有成员\_提供程序结构，根据需要。

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
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_主页\_提供程序](oid-wwan-home-provider.md)

[**NDIS\_WWAN\_HOME\_PROVIDER**](https://msdn.microsoft.com/library/windows/hardware/ff567909)

 

 




