---
title: NDIS_STATUS_WWAN_PIN_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PIN_INFO 通知来响应 OID 查询并设置 OID_WWAN_PIN 的请求。 微型端口驱动程序无法使用此通知发送未经请求的事件。此通知使用 NDIS_WWAN_PIN_INFO 结构。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PIN_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d72940036620fbc86d95941c3d9df342abc66691
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825479"
---
# <a name="ndis_status_wwan_pin_info"></a>NDIS \_ 状态 \_ WWAN \_ PIN \_ 信息


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ pin \_ 信息通知来响应 Oid 查询并设置 [oid \_ WWAN \_ pin](oid-wwan-pin.md)的请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ PIN \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info) 结构。

<a name="remarks"></a>备注
-------

小型端口驱动程序应返回 (PIN) 的个人标识号的信息，MB 设备当前需要该请求来响应查询请求。 小型端口驱动程序应按照以下部分中所述的方式返回状态通知，以响应某个设置请求。

**响应 WwanPinOperationEnter 请求**

当微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ PIN \_ 信息通知来响应 **WwanPinOperationEnter** 请求时，它们应该实现以下过程：

-   对于成功的 **WwanPinOperationEnter** 查询请求，当 MB 设备不再需要 PIN 时，微型端口驱动程序必须将 **USTATUS** 设置为 WWAN \_ 状态 \_ 成功，并将 **PinType** 设置为 **WwanPinTypeNone**。

-   对于失败的 **WwanPinOperationEnter** 请求，微型端口驱动程序必须将 **USTATUS** 设置为 WWAN \_ 状态 \_ 失败，并按照以下详细信息包括适用的数据：

    -   PIN 已禁用或不应 PIN：对于 **WwanPinOperationEnter** 集请求，当相应的 PIN 已禁用或当前不是 MB 设备的预期时，微型端口驱动程序必须将 **PinType** 设置为 **WwanPinTypeNone**。 将忽略所有其他成员。

    -   不支持 PIN：如果 MB 设备不支持给定的 PIN，微型端口驱动程序必须将 **uStatus** 设置为 WWAN \_ 状态 " \_ 无 \_ 设备支持" \_ 。

    -   固定 Retrial：在此模式下，MB 设备需要重新输入 PIN，因为对于此特定类型的 PIN， **AttemptsRemaining** 值仍然为非零。 微型端口驱动程序必须将 **PinType** 设置为与 NDIS **PinType** \_ WWAN \_ 集 PIN 中的 PinType 相同的值 \_ 。

    -   锁定锁定：当 **AttemptsRemaining** 为零时，会阻止 pin。 如果 PIN 解除阻止操作不可用，微型端口驱动程序必须将 **uStatus** 设置为 WWAN \_ 状态 \_ 失败，并将 **PinType** 设置为 **WwanPinTypeNone**。 将忽略所有其他成员。

        **注意**  如果 MB 设备支持 PIN 取消阻止操作，微型端口驱动程序应遵循 PIN 取消阻止步骤来响应请求。

         

    -   PIN 解除锁定：当 **AttemptsRemaining** 为零时，会阻止 pin。 为了解除锁定 PIN，MB 设备可能会请求相应的 PIN 解锁密钥 (PUK) （如果适用）。 在这种情况下，微型端口驱动程序必须将 **PinType** 设置为相应的 WwanPinType *Xxx* PUK，并提供相关的详细信息。

    -   已阻止的 PUK：如果失败的试用次数超过了输入 WwanPinType *Xxx* PUK 的预设值，则 PUK 将被阻止。 微型端口驱动程序必须通过将 **uStatus** 设置为 WWAN \_ 状态 \_ 失败，并将 **PinType** 设置为 **WwanPinTypeNone** 来指示这一点。 如果阻止 PUK1，微型端口驱动程序必须发送 NDIS \_ 状态 \_ WWAN \_ 就绪信息， \_ 并将 **ReadyState** 设置为 **WwanReadyStateBadSim**。

**响应 WwanPinOperationEnable、WwanPinOperationDisable 或 WwanPinOperationChange 请求**

当微型端口驱动程序使用 \_ NDIS 状态 \_ WWAN \_ PIN \_ 信息通知来响应 **WwanPinOperationEnable**、 **WwanPinOperationDisable** 和 **WwanPinOperationChange** 时，它们应该实现以下操作：

-   对于成功的请求，微型端口驱动程序必须将 **uStatus** 设置为 WWAN \_ 状态 "成功" \_ 。 有关 WWAN_PIN_INFO 中的其他成员，请参阅下列情况。

-   如果 pin 已经处于请求状态，微型端口驱动程序必须将 **uStatus** 设置为 WWAN \_ 状态 " \_ 成功" 和 "pin 禁用" 操作。 微型端口驱动程序必须将 **PinType** 设置为 **WwanPinTypeNone**。 忽略其他成员。

-   当 PIN 模式从 "已禁用" 更改为 "已启用" 时，PIN 状态应为 WwanPinStateNone。

-   如果启用了 PIN1，则当电源重启到 MB 设备时，PIN 状态应变为 WwanPinStateEnter。

-   对于所有其他 Pin，PIN 状态可以从 WwanPinStateNone 更改为 WwanPinStateEnter，具体取决于 MB 设备特定的条件。

-   不支持 PIN：如果在 MB 设备上不支持 PIN 操作，微型端口驱动程序必须将 **uStatus** 设置为 WWAN \_ 状态 " \_ 无 \_ 设备支持" \_ 。 例如，启用和禁用 PIN2 通常不支持 MB 设备，因此必须返回上述错误代码。 将忽略所有其他成员。

-   必须输入 PIN：如果 PIN 操作要求输入 PIN，微型端口驱动程序必须将 **uStatus** 设置为 \_ REQUIRED，并将 \_ \_ **PinType** 设置为 WwanPinType *Xxx*。 忽略其他成员。

-   PIN 更改操作：如果仅当 MB 设备处于 "已启用" 状态时，它会限制 PIN 值的更改，则必须在禁用了 WWAN 状态 PIN 的情况下返回 "已禁用" 状态的请求 \_ \_ \_ 。

-   PIN Retrial：失败时，微型端口驱动程序必须将 **uStatus** 设置为 WWAN \_ 状态 \_ 失败，并将 **PinType** 设置为 NDIS \_ WWAN \_ 设置 \_ PIN 中指定的相同值。 除 **AttemptsRemaining** 之外，还将忽略其他成员。 输入错误的 PIN 时可能会发生这种情况。

-   锁定锁定：当 **AttemptsRemaining** 数为零时，会阻止 pin。 如果 PIN 解除阻止操作不可用，微型端口驱动程序必须将 **uStatus** 设置为 WWAN \_ 状态 \_ 失败，并将 **PinType** 设置为 **WwanPinTypeNone**。 应将 **AttemptsRemaining** 设置为0，并忽略所有其他成员。

    **注意**  如果 MB 设备支持 PIN 取消阻止操作，微型端口驱动程序应遵循 PIN 取消阻止步骤来响应请求。

     

-   解除锁定 PIN：当 **AttemptsRemaining** 为零时，会阻止 pin。 若要解除锁定 PIN，MB 设备可能会请求相应的 PUK （如果适用）。 在这种情况下，微型端口驱动程序必须将 **uStatus** 设置为 WWAN \_ 状态 \_ 失败，将 **PinType** 设置为相应的 WwanPinType *Xxx* PUK，将 **PinState** 设置为 **WwanPinStateEnter**，并且 **AttemptsRemaining** 应具有允许输入有效 PUK 的尝试次数。

    如果在 MB 设备或 SIM 被阻止的情况下出现 PIN 阻止结果，微型端口驱动程序必须发送事件通知，并将 **ReadyState** 设置为 **WwanReadyStateDeviceLocked**。

-   如果 PIN1 阻止时存在活动的 PDP 上下文，微型端口驱动程序必须停用 PDP 上下文，并将通知发送到操作系统，使其发生了 PDP 停用和链接状态更改。

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

## <a name="see-also"></a>请参阅


[OID \_ WWAN \_ PIN](oid-wwan-pin.md)

[**NDIS \_ 状态 \_ WWAN \_ PIN \_ 信息**](ndis-status-wwan-pin-info.md)

 

