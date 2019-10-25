---
title: NDIS_STATUS_WWAN_REGISTER_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_REGISTER_STATE 通知将对 MB 设备注册状态的更改传递到 MB 服务。
ms.assetid: 3da8489a-6ca3-4897-9794-86665ce10e81
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_REGISTER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c1474227e459d3045ecf2c04cd354a0cc770fb5c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844650"
---
# <a name="ndis_status_wwan_register_state"></a>WWAN\_REGISTER\_状态\_NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_注册\_状态通知，将对 MB 设备注册状态的更改传递到 MB 服务。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)结构。

<a name="remarks"></a>备注
-------

设备的注册状态发生变化时，微型端口驱动程序必须发送相应的指示，以便 MB 服务能够向用户反映正确的状态。

注册状态因多种原因而发生更改。 它可能会直接从来自 MB 服务的*设置*请求\_WWAN\_注册\_状态，例如从**WwanRegisterStateSearching**到**WwanRegisterStateHome**的暂时性状态转换。 在自动提供程序选择的情况下，微型端口驱动程序自动操作也可能会导致此情况。 最后，可能是因为网络可用性发生了变化，例如，丢失网络覆盖可能导致从**WwanRegisterStateHome**到**WwanRegisterStateDeregistered**的转换。

除了由 MB 服务 OID 引起的更改\_WWAN\_注册\_状态请求，当注册状态发生变化时，无论根本原因如何，微型端口驱动程序都应通知 MB 服务。

CDMA 设备不支持 MB 服务启动的注册和注销。 但是，必须将基于运营商网络可用性或非可用性的设备启动的注册状态更改通知发送到 MB 服务。 CDMA 设备必须执行自动注册。

对于在开机时自动注册的设备，无论当前注册模式是自动还是手动，微型端口驱动程序必须在成功注册后发送注册状态通知。

对于手动注册，MB 服务仅应在微型端口驱动程序指示**ReadyState**为**WwanReadyStateInitialized**后启动注册。

在响应*设置*请求时，微型端口驱动程序必须使用以下准则：

-   对于*集*请求，驱动程序不得以暂时性状态进行响应。 注册的暂时性状态为**WwanRegisterStateSearching**。

-   当**RegisterAction**设置为**WwanRegisterActionManual**时，如果提供程序在微型端口驱动程序收到请求时不可见，则微型端口驱动程序应返回错误代码 WWAN\_状态\_提供程序\_不\_可见。 设备不能切换到自动注册，因为在设置手动模式时出现故障。 如果先前将设备设置为手动注册到另一个网络，则此请求应将设备更改为向请求中指定的网络注册。 为了响应请求， **RegisterState**的值应设置为**WwanRegisterStateDeregistered**。

-   当**RegisterAction**设置为**WwanRegisterActionManual**时，如果微型端口驱动程序已注册到所请求的同一网络中，则它应\_成功的 WWAN\_状态进行响应。

-   驱动程序应尝试在设置 OID\_WWAN\_REGISTER 请求中注册到请求的数据类。 如果微型端口驱动程序无法注册到所请求的数据类，则应将其注册到可能的最佳数据类。 如果已使用其他一些数据类向提供程序（自动和手动注册模式）注册了设备，则此项也适用。 数据类中的任何更改还应导致 NDIS\_状态\_WWAN\_数据包\_服务通知。

-   如果将**RegisterAction**设置为**WwanRegisterActionManual**，并且无线电已关闭，微型端口驱动程序必须将设备编程为手动注册模式，并通过事务通知完成请求。 应将**RegisterState**设置为**WwanRegisterStateDeregistered**。 当无线电更改为 "开" 状态并且必须发送事件通知时，设备必须尝试手动注册。

-   如果将**RegisterAction**设置为**WwanRegisterActionAutomatic**，并且无线电已关闭，微型端口驱动程序必须将设备编程为自动注册模式，并且必须通过事务通知完成请求。 应将**RegisterState**设置为**WwanRegisterStateDeregistered**。 当无线电进入开机状态并且必须发送事件通知时，设备必须执行自动注册。

-   在紧急状态注册（ **WwanRegisterStateDenied**）的情况下，应将**USTATUS**设置为 WWAN\_状态\_成功，NDIS\_状态\_WWAN\_准备好\_信息通知必须与**EmergencyMode**设置为**WwanEmergencyModeOn**。

-   对于使用状态**WwanRegisterStateDeregistered** ，微型端口驱动程序必须使用以下准则：

    -   小型端口驱动程序使用**WwanRegisterStateDeregistered**向 MB 服务通知，无线电已关闭，但**RegisterAction**的请求已完成。

    -   **WwanRegisterStateDeregistered**由微型端口驱动程序用来通知 MB 服务网络启动的注销。

    -   由于没有网络覆盖，小型端口驱动程序使用**WwanRegisterStateDeregistered**通知 MB 服务网络断开连接。

-   GSM 和 CDMA 设备必须发送注册状态通知，以通知运营商是否有 PS 连接的可用性或不可用。 当 MB 设备检测到电信公司网络的可用性时，它必须发送事件通知，其中包含适当的注册状态之一-- **WwanRegisterStateHome**、 **WwanRegisterStateRoaming**或**WwanRegisterStatePartner**. 丢失运营商网络信号时，必须向 MB 服务指示包含**WwanRegisterStateDeregistered**的事件通知。

微型端口驱动程序根据以下规则返回查询结果：

-   当设备在注册期间尝试锁定到提供程序时，微型端口驱动程序应将**RegisterState**设置为**WwanRegisterStateSearching**。 **ProviderName**和**RoamingText**成员都应设置为**NULL**。 如果是手动注册模式，则必须用上一个手动注册集请求中的 ProviderId 填充**providerid** 。 如果是自动注册模式，则可以将**ProviderId**设置为**NULL** 。

-   这是暂时性的状态，因为微型端口驱动程序最终会在注册结束时转变为稳定状态，例如， **WwanRegisterStateHome**、 **WwanRegisterStatePartner**或**WwanRegisterStateRoaming**成功报名用于紧急状态注册的**WwanRegisterStateDenied** 。

-   如果设备未注册到任何提供程序，则微型端口驱动程序应返回**WwanRegisterStateDeregistered**。 **ProviderName**和**RoamingText**成员都应设置为**NULL**。 如果是手动注册模式，则必须用上一个手动注册集请求中的 ProviderId 填充**providerid** 。 如果是自动注册模式，则可以将**ProviderId**设置为**NULL** 。

-   如果向 home 提供商注册了设备，微型端口驱动程序应将**RegisterState**设置为**WwanRegisterStateHome**。 **ProviderId**成员应设置为 home 提供程序 ID。 **ProviderName**必须设置为家庭提供商网络的名称。 应将**RoamingText**成员设置为**NULL**。

-   如果设备已向漫游提供商注册，如果访问接口是首选漫游伙伴或只是漫游伙伴的**WwanRegisterStateRoaming** ，则微型端口驱动程序应将**RegisterState**设置为**WwanRegisterStatePartner** 。分别. 如果微型端口驱动程序不区分这两者，则它应将值设置为**WwanRegisterStateRoaming**。 **ProviderId**成员应设置为设备注册到的当前提供程序的提供程序 ID，而且必须用当前注册的提供程序名称填充**ProviderName** 。 如果存在，则应将**RoamingText**成员设置为特定于提供程序的字符串值，否则为**NULL** 。

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
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_注册\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_registration_state)

[OID\_WWAN\_注册\_状态](oid-wwan-register-state.md)

 

 




