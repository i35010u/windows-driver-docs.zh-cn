---
title: OID_WWAN_READY_INFO
description: OID_WWAN_READY_INFO 返回设备就绪状态，其中包括其用户识别模块 （SIM 卡）。
ms.assetid: 3e6f6cb7-14fc-4eee-b5d6-d5e0cad46ea2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_READY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4b34a8b706684b9b3871f6ae1f71d3ed20b4132a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368516"
---
# <a name="oidwwanreadyinfo"></a>OID\_WWAN\_准备\_信息


OID\_WWAN\_准备\_信息返回设备就绪状态，其中包括其用户识别模块 （SIM 卡）。 这通常发生在任何会话的开始处。

不支持组的请求。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_准备\_信息**](ndis-status-wwan-ready-info.md)状态通知包含[ **NDIS\_WWAN\_准备就绪\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff567916)结构，指示 MB 设备的就绪状态时完成查询请求。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[MB 设备准备情况](https://msdn.microsoft.com/library/windows/hardware/ff557164)。

微型端口驱动程序可以访问设备的内存或 SIM 卡处理时查询操作，但不是应访问提供程序网络。

微型端口驱动程序应等待，直到清除 PIN （如果需要），然后阅读订阅者的标识和电话号码 (TNs)，并将 NDIS ReadyInfo.ReadyState 成员\_WWAN\_准备\_信息WwanReadyStateInitialized 结构。

微型端口驱动程序必须永远不会失败 OID\_WWAN\_准备\_信息和必须始终返回正确的设备就绪状态。

设备就绪状态发生更改时，微型端口驱动程序必须始终通知 MB 服务。

微型端口驱动程序应遵循这些步骤提供良好的用户体验：

-   如果 PIN1 被锁定，微型端口驱动程序必须先准备状态事件，将通知发送**ReadyInfo.ReadyState**设置为*WwanReadyStateDeviceLocked*。 MB 服务然后发送微型端口驱动程序 OID 集请求的 OID\_WWAN\_PIN。 设备解锁然后微型端口驱动程序，必须将另一个就绪状态事件通知发送后**ReadyInfo.ReadyState**设置为*WwanReadyStateInitialized*。 直到 PIN1 成功解锁，微型端口驱动程序不得更改为设备就绪的状态*WwanReadyStateInitialized*。

-   微型端口驱动程序必须首先将发送一封包含事件通知**ReadyInfo.ReadyState**设置为*WwanReadyStateSimNotInserted* MB 服务加载时微型端口驱动程序如果没有 SIM 卡，则为 5 月与允许 SIM 卡插入或删除的设备出现这种情况。 如果设备具有此功能来检测 SIM 卡热插入，微型端口驱动程序必须发送另一个事件通知与**ReadyInfo.ReadyState**设置为*WwanReadyStateInitialized*时用户插入 SIM。

-   具有该功能来检测服务激活状态的设备必须设置**ReadyInfo.ReadyState**到*WwanReadyStateNotActivated*。 此外，如果微型端口驱动程序支持服务激活，微型端口驱动程序将接收 OID 集请求的 OID\_WWAN\_服务\_激活。 服务激活成功完成后，微型端口驱动程序必须另一个事件，将通知发送**ReadyInfo.ReadyState**设置为*WwanReadyStateInitialized*。

-   需要特定固件修订的微型端口驱动程序必须确保正确的固件修订版本可用。 如果固件修订版本不可用，微型端口驱动程序应通过设置完成事件通知事务**ReadyInfo.ReadyState**到*WwanReadyStateFailure*。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_READY\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567916)

[**NDIS\_状态\_WWAN\_准备\_信息**](ndis-status-wwan-ready-info.md)

[MB 设备准备情况](https://msdn.microsoft.com/library/windows/hardware/ff557164)

 

 




