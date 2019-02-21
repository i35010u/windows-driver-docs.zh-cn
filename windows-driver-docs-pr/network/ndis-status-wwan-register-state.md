---
title: NDIS_STATUS_WWAN_REGISTER_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_REGISTER_STATE 通知传递到 MB 服务的 MB 设备的注册状态的更改。
ms.assetid: 3da8489a-6ca3-4897-9794-86665ce10e81
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_REGISTER_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 112703407a936bd52aa90f2e3c0921a0f5f4e368
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547337"
---
# <a name="ndisstatuswwanregisterstate"></a>NDIS\_状态\_WWAN\_注册\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_注册\_通信到 MB 服务的 MB 设备的注册状态更改的状态通知。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_注册\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567917)结构。

<a name="remarks"></a>备注
-------

作为设备更改的注册状态，微型端口驱动程序必须发送相应的指示，以便 MB 服务可以反映给用户的正确状态。

注册状态更改许多原因。 它可能会直接导致从*设置*来自 OID MB 服务请求\_WWAN\_注册\_状态从一个暂时性状态转换等**WwanRegisterStateSearching**到**WwanRegisterStateHome**。 它还可能会在自动提供程序选择的情况下微型端口驱动程序导致自动操作。 最后，可能引起的网络可用性更改，例如，丢失网络覆盖范围从转换中可能会导致**WwanRegisterStateHome**到**WwanRegisterStateDeregistered**。

MB 服务 OID 所导致的更改除外\_WWAN\_注册\_状态请求时，微型端口驱动程序应通知 MB 服务，每当注册状态更改而不考虑的基本原因。

CDMA 的设备，不要支持 MB 服务发起的注册和注销。 但是，在设备注册基于可用性或非可用性运营商网络通知必须发送到 MB 服务的状态更改。 CDMA 的设备必须执行自动注册。

不要在开机，而不考虑当前注册模式-auto 或 manual，自动注册的设备的微型端口驱动程序必须发送注册状态通知注册成功。

有关手动注册 MB 服务应仅注册后启动微型端口驱动程序指示**ReadyState**是**WwanReadyStateInitialized**。

微型端口驱动程序必须响应时使用以下指导原则*设置*请求：

-   驱动程序必须响应与暂时性状态*设置*请求。 暂时性状态为注册**WwanRegisterStateSearching**。

-   当**RegisterAction**设置为**WwanRegisterActionManual**，如果提供程序不可见时微型端口驱动程序收到请求时，微型端口驱动程序应会返回错误代码 WWAN\_状态\_提供程序\_不\_可见。 不，设备必须切换到自动注册设置手动模式下的失败。 如果设备是早期设置为手动注册到另一个网络，此请求应更改设备注册到请求中指定的网络。 值**RegisterState**对请求响应中应将它设置为**WwanRegisterStateDeregistered**。

-   当**RegisterAction**设置为**WwanRegisterActionManual**，如果微型端口驱动程序具有已注册到已请求时，它应使用 WWAN 进行响应的同一个网络\_状态\_成功。

-   该驱动程序应尝试注册到请求的数据类集中 OID\_WWAN\_注册请求。 如果微型端口驱动程序不能注册到请求的数据类，它应注册为最佳可能的数据类。 这一点也适用于设备与某个其他数据类已注册到提供程序 （自动和手动注册模式）。 数据类中的任何更改还应导致 NDIS\_状态\_WWAN\_数据包\_服务通知。

-   当**RegisterAction**设置为**WwanRegisterActionManual**，和无线电已关闭，微型端口驱动程序必须程序手动注册模式到设备并完成与事务请求通知。 **RegisterState**应设置为**WwanRegisterStateDeregistered**。 当状态更改为单选，并且必须发送事件通知时，设备必须尝试手动注册。

-   当**RegisterAction**设置为**WwanRegisterActionAutomatic**，和单选为 OFF，则微型端口驱动程序必须进行编程模式下自动注册到设备，并且必须完成与请求事务通知。 **RegisterState**应设置为**WwanRegisterStateDeregistered**。 单选将进入状态，并且必须发送事件通知时，设备必须执行的自动注册。

-   发生紧急状态注册时 ( **WwanRegisterStateDenied**)，则**uStatus**应设置为 WWAN\_状态\_成功和 NDIS\_状态\_WWAN\_准备好\_信息通知必须发送与**EmergencyMode**设置为**WwanEmergencyModeOn**。

-   有关使用状态**WwanRegisterStateDeregistered**微型端口驱动程序必须使用以下准则：

    -   **WwanRegisterStateDeregistered**通知 MB 服务无线电但的请求已关闭的微型端口驱动程序用于**RegisterAction**完成。

    -   **WwanRegisterStateDeregistered**由微型端口驱动程序通知 MB 服务网络发起的注销。

    -   **WwanRegisterStateDeregistered**由微型端口驱动程序用于通知 MB 到无网络覆盖范围由于网络连接中断的服务。

-   GSM 和 CDMA 的设备必须发送通知的可用性或非可用性 PS 连接的运营商的注册状态通知。 当 MB 设备检测到的运营商网络可用性时，它必须发送事件通知与相应的注册状态-之一**WwanRegisterStateHome**， **WwanRegisterStateRoaming**，或**WwanRegisterStatePartner**。 在丢失网络信号，使用事件通知的运营商**WwanRegisterStateDeregistered**必须指定给 MB 服务。

微型端口驱动程序返回查询结果根据以下规则：

-   当设备尝试锁定到提供程序注册期间时，应设置微型端口驱动程序**RegisterState**作为**WwanRegisterStateSearching**。 这两个**ProviderName**并**RoamingText**成员应设置为**NULL**。 对于手动注册模式**ProviderId**必须使用从最后一个手动注册集请求 ProviderId 填充。 **ProviderId**可以设置为**NULL**发生自动注册模式时。

-   这是暂时性的状态，如微型端口驱动程序最终都会迁移到稳定状态末尾的注册，例如， **WwanRegisterStateHome**， **WwanRegisterStatePartner**，或**WwanRegisterStateRoaming**成功的注册; 或**WwanRegisterStateDenied**的紧急状态注册。

-   如果不与任何提供程序注册该设备，应会返回微型端口驱动程序**WwanRegisterStateDeregistered**。 这两个**ProviderName**并**RoamingText**成员应设置为**NULL**。 对于手动注册模式**ProviderId**必须使用从最后一个手动注册集请求 ProviderId 填充。 **ProviderId**可以设置为**NULL**发生自动注册模式时。

-   如果设备注册到的家庭的提供程序后，应设置微型端口驱动程序**RegisterState**作为**WwanRegisterStateHome**。 **ProviderId**成员应设置为主页的提供程序 id。 **ProviderName**必须设置为主页的提供程序网络的名称。 **RoamingText**成员应设置为**NULL**。

-   如果使用漫游的提供程序注册设备时，应设置微型端口驱动程序**RegisterState**作为**WwanRegisterStatePartner**如果提供程序的首选漫游合作伙伴或只是**WwanRegisterStateRoaming**漫游的合作伙伴，分别。 如果微型端口驱动程序不能区分这两个，它应将值设置为**WwanRegisterStateRoaming**。 **ProviderId**成员应设置为当前提供程序的设备注册的提供程序 ID 和**ProviderName**必须填充当前已注册的提供程序名称。 **RoamingText**成员应设置为某个提供程序特定的字符串值，如果存在或设置为**NULL**否则为。

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
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_REGISTRATION\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567917)

[OID\_WWAN\_REGISTER\_STATE](oid-wwan-register-state.md)

 

 




