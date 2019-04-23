---
title: OID_WWAN_REGISTER_STATE
description: OID_WWAN_REGISTER_STATE 选择网络提供商注册。
ms.assetid: 564de5bf-10d9-47fe-a4c1-3409d9b2aee8
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_REGISTER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a4eb8530c35d537061fd8e7b138efd5f6bec4127
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903491"
---
# <a name="oidwwanregisterstate"></a>OID\_WWAN\_REGISTER\_STATE


OID\_WWAN\_注册\_状态选择网络提供商注册。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_注册\_状态**](ndis-status-wwan-register-state.md)状态通知包含[ **NDIS\_WWAN\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567917)结构，以便提供有关已注册的网络提供程序而不考虑完成组的信息或查询请求。

设置网络提供商，以将注册请求的调用方提供[ **NDIS\_WWAN\_设置\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567926)结构微型端口驱动程序的相应信息。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 注册操作](https://msdn.microsoft.com/library/windows/hardware/ff559116)。

微型端口驱动程序可以访问提供程序网络时处理查询或设置操作，但不是应访问用户识别模块 （SIM 卡）。

MB 驱动程序模型支持两种注册方法-自动和手动。 为基于 CDMA 的网络，MB 驱动程序模型支持仅自动注册。

支持手动注册的设备必须设置**WwanControlCaps**中的成员[ **WWAN\_设备\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff571204) WWAN结构\_CTRL\_CAPS\_REG\_手动。 请注意，基于 GSM 的设备必须支持手动注册。

当注册状态为自动，微型端口驱动程序必须指示要选择网络提供商基于特定于移动电话技术选择算法并继续注册其设备。

RegisterAction 值的语义定义，如下所示：

-   *WwanRegisterActionAutomatic* MB 服务使用标志以指示要将设备设置为自动注册模式让设备选择最佳的提供程序网络的微型端口驱动程序。 微型端口驱动程序必须忽略**ProviderId**参数。 跨单选状态 （开/关），此设置是持久和设备电源周期，直到显式更改 MB 服务。

-   *WwanRegisterActionManual* MB 服务使用标志以指示要注册到标识提供程序网络的微型端口驱动程序**ProviderId**参数。 **ProviderId**值应来自**ProviderId** WWAN 成员\_一个可见的提供程序的提供程序数据结构。 此设置是在单选状态 （开/关） 和设备电源周期持久性的直到显式更改 MB 服务。

-   即使该设备当前已注册到提供程序允许不同的 RegisterAction 值之间的更改。 如果需要自动和手动注册模式之间切换之前取消注册设备，必须确保微型端口驱动程序的设备设置为在设置为新注册模式之前注销。

-   *手动*并*自动*注册模式只会影响网络选择模式。 MB 设备应尝试注册到所选网络，只要启用单选。

### <a name="windows-10-version-1903"></a>Windows 10，版本 1903

在 Windows 10，版本 1903年开始支持此 OID 的新修订版本 3。 此扩展使宿主能够查询首选的无线访问技术 (Rat) 从微型端口驱动程序。 

若要控制首选的 RAT，主机设置了位掩码，表示在 WWAN_DATA_CLASS 值**WwanDataClass**的成员[ **WWAN_SET_REGISTER_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_set_register_state)结构. 此成员表示首选分发点的连接的数据访问技术。 如果此字段设置为**WWAN_DATA_CLASS_NONE**，则调制解调器应不采取任何操作，此参数。

主机还可以查询中的微型端口驱动程序的当前首选的数据类。 微型端口驱动程序将使用**PreferredDataClasses**字段[ **WWAN_REGISTRATION_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_registration_state)结构报告是首选的数据访问技术调制解调器中当前设置。

5 G 数据类支持的详细信息，请参阅[MB 5g 数据类支持](mb-5g-data-class-support.md)。

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


[**NDIS\_WWAN\_SET\_REGISTER\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567926)

[**NDIS\_状态\_WWAN\_注册\_状态**](ndis-status-wwan-register-state.md)

[WWAN 注册操作](https://msdn.microsoft.com/library/windows/hardware/ff559116)

 

 




