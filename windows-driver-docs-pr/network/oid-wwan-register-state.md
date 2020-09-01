---
title: OID_WWAN_REGISTER_STATE
description: OID_WWAN_REGISTER_STATE 选择要向其注册的网络提供程序。
ms.assetid: 564de5bf-10d9-47fe-a4c1-3409d9b2aee8
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_REGISTER_STATE 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1ef4eb6ac7fba826178ce657cb68b6ac696b39fc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215815"
---
# <a name="oid_wwan_register_state"></a>OID \_ WWAN \_ 寄存器 \_ 状态


OID \_ WWAN \_ 注册 \_ 状态选择要向注册的网络提供程序。

微型端口驱动程序必须异步处理集和查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 寄存器 \_ 状态**](ndis-status-wwan-register-state.md) 通知，其中包含 [**ndis \_ WWAN \_ 注册 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state) 结构，以提供注册的网络提供程序的相关信息，而不考虑完成的集或查询请求。

请求设置要注册的网络提供程序的调用方使用适当的信息向微型端口驱动程序提供 [**NDIS \_ WWAN \_ 集 \_ 注册 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state) 结构。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN 注册操作](./mb-registration-operations.md)。

当处理查询或设置操作时，微型端口驱动程序可以访问提供程序网络，但不应 (SIM 卡) 访问订阅服务器标识模块。

MB 驱动程序模型支持两个注册方法--自动和手动。 对于基于 CDMA 的网络，MB 驱动程序模型仅支持自动注册。

支持手动注册的设备必须将[**wwan \_ 设备 \_ cap**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)结构中的**WwanControlCaps**成员设置为 wwan \_ CTRL + \_ \_ REG \_ 手册。 请注意，基于 GSM 的设备必须支持手动注册。

如果注册状态为自动，微型端口驱动程序必须指示其设备根据移动电话技术特定的选择算法选择网络提供程序，并继续进行注册。

RegisterAction 值的语义定义如下：

-   MB 服务使用 *WwanRegisterActionAutomatic* 标志来指示微型端口驱动程序将设备设置为自动注册模式，并让设备选择最佳的提供程序网络。 微型端口驱动程序必须忽略 **ProviderId** 参数。 此设置在无线电状态之间保持不变 (开启/关闭) 和设备电源循环，直到由 MB 服务显式更改。

-   MB 服务使用 *WwanRegisterActionManual* 标志来指示微型端口驱动程序向 **ProviderId** 参数标识的提供商网络注册。 **ProviderId**值应来自**ProviderId** \_ 一个可见提供程序的 WWAN 提供程序数据结构的 providerid 成员。 此设置在无线电状态之间保持不变 (开启/关闭) 和设备电源循环，直到由 MB 服务显式更改。

-   即使设备当前已注册到提供程序，也允许在不同 RegisterAction 值之间进行更改。 如果在自动注册模式和手动注册模式间切换之前设备需要取消注册，微型端口驱动程序必须确保在设置为新注册模式之前，将设备设置为 "注销"。

-   *手动*和*自动*注册模式仅影响网络选择模式。 当打开无线电设备时，MB 设备应尝试注册到选定的网络。

### <a name="windows-10-version-1903"></a>Windows 10 版本 1903

从 Windows 10 版本1903开始，支持此 OID 的新修订版本3。 此扩展使宿主可以通过微型端口驱动程序查询 (Rat) 的首选无线电访问技术。 

为了控制首选 RAT，主机设置了一个位掩码，表示[**WWAN_SET_REGISTER_STATE**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_set_register_state)结构的**WwanDataClass**成员中的 WWAN_DATA_CLASS 值。 此成员表示连接首选的数据访问技术。 如果此字段设置为 " **WWAN_DATA_CLASS_NONE**"，则调制解调器对于此参数应该不执行任何操作。

宿主还可以从微型端口驱动程序查询当前首选的数据类。 微型端口驱动程序使用[**WWAN_REGISTRATION_STATE**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_registration_state)结构的 " **PreferredDataClasses** " 字段来报告当前在调制解调器中设置的首选数据访问技术。

有关5G 数据类支持的详细信息，请参阅 [MB 5G 数据类支持](mb-5g-data-class-support.md)。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ WWAN \_ 设置 \_ 注册 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_register_state)

[**NDIS \_ 状态 \_ WWAN \_ 寄存器 \_ 状态**](ndis-status-wwan-register-state.md)

[WWAN 注册操作](./mb-registration-operations.md)

 

