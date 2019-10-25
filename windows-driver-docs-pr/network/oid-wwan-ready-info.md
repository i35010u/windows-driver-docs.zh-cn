---
title: OID_WWAN_READY_INFO
description: OID_WWAN_READY_INFO 返回设备就绪状态，其中包括其订户标识模块（SIM 卡）。
ms.assetid: 3e6f6cb7-14fc-4eee-b5d6-d5e0cad46ea2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_READY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f9b442eb56e0d1577ef8cd3dd27c030e636c3eff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843800"
---
# <a name="oid_wwan_ready_info"></a>OID\_WWAN\_就绪\_信息


OID\_WWAN\_就绪\_信息返回设备就绪状态，其中包括其订户标识模块（SIM 卡）。 这通常发生在任何会话的开头。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后将[**ndis\_状态\_WWAN\_就绪\_信息**](ndis-status-wwan-ready-info.md)状态通知，其中包含一个[**NDIS\_WWAN\_就绪\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)结构，该结构指示在完成查询请求时的设备就绪状态。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[MB 设备准备情况](https://docs.microsoft.com/windows-hardware/drivers/network/mb-device-readiness)。

当处理查询操作时，微型端口驱动程序可以访问设备内存或 SIM 卡，但不应访问提供程序网络。

小型端口驱动程序应等待，直到清除 PIN （如果需要），然后读取订阅服务器的标识和电话号码（TNs），然后将 NDIS\_WWAN\_\_的 ReadyState 成员设置为，以WwanReadyStateInitialized.

微型端口驱动程序绝不能\_WWAN\_就绪\_信息，并且必须始终返回正确的设备就绪状态。

当设备就绪状态发生变化时，微型端口驱动程序必须始终通知 MB 服务。

微型端口驱动程序应遵循以下步骤来提供良好的用户体验：

-   如果 PIN1 已锁定，微型端口驱动程序必须首先将**ReadyInfo**设置为*WwanReadyStateDeviceLocked*。 然后，MB 服务向微型\_WWAN\_PIN 的 oid 集请求发送微型端口驱动程序。 设备解锁后，微型端口驱动程序必须发送另一个就绪状态事件通知，并将**ReadyState**设置为*WwanReadyStateInitialized*。 在成功解锁 PIN1 之前，微型端口驱动程序不得将设备就绪状态更改为*WwanReadyStateInitialized*。

-   当 MB 服务加载微型端口驱动程序时，微型端口驱动程序必须首先将**ReadyInfo**设置为*WwanReadyStateSimNotInserted* ，如果不存在 sim 卡，则可能会出现这样的情况：允许使用 sim 卡的设备插入或删除。 如果设备能够检测到热插入 SIM 卡，则当用户插入 SIM 时，微型端口驱动程序必须将**ReadyState**设置为 WwanReadyStateInitialized 的其他事件通知发送到 。

-   能够检测服务激活状态的设备必须将 ReadyState 设置为*WwanReadyStateNotActivated*。 **ReadyInfo** 此外，如果微型端口驱动程序支持服务激活，微型端口驱动程序将收到 oid\_WWAN\_SERVICE\_激活的 oid 设置请求。 成功完成服务激活后，微型端口驱动程序必须发送另一个事件通知，并将**ReadyInfo ReadyState**设置为*WwanReadyStateInitialized*。

-   需要具体固件修订版本的微型端口驱动程序必须确保正确的固件版本可用。 如果固件版本不可用，微型端口驱动程序应通过将**ReadyInfo**设置为*WwanReadyStateFailure*来完成事件通知事务。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_准备好\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ready_info)

[**NDIS\_状态\_WWAN\_就绪\_信息**](ndis-status-wwan-ready-info.md)

[MB 设备准备情况](https://docs.microsoft.com/windows-hardware/drivers/network/mb-device-readiness)

 

 




