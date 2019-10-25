---
title: NDIS_STATUS_WWAN_PIN_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PIN_INFO 通知响应 OID 查询并设置 OID_WWAN_PIN 的请求。 微型端口驱动程序无法使用此通知发送未经请求的事件。此通知使用 NDIS_WWAN_PIN_INFO 结构。
ms.assetid: fa3c2467-2240-423b-b91b-f7e19d5be353
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PIN_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dce91e3403f90a928cb65706bea5409108c6257b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844788"
---
# <a name="ndis_status_wwan_pin_info"></a>\_WWAN\_PIN\_信息的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_PIN\_信息通知来响应 OID 查询，并将 Oid 的请求设置[\_WWAN\_PIN](oid-wwan-pin.md)。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_固定\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序应返回有关 MB 设备当前预期响应查询请求的个人标识号（PIN）的信息。 小型端口驱动程序应按照以下部分中所述的方式返回状态通知，以响应某个设置请求。

**响应 WwanPinOperationEnter 请求**

当微型端口驱动程序使用 NDIS\_状态\_WWAN\_PIN\_信息通知来响应**WwanPinOperationEnter**请求时，它们应该实现以下过程：

-   对于成功的**WwanPinOperationEnter**查询请求，当 MB 设备不再需要 PIN 时，微型端口驱动程序必须将**USTATUS**设置为 WWAN\_\_状态 "成功" 和 " **PinType** " 设置为 " **WwanPinTypeNone**"。

-   对于失败的**WwanPinOperationEnter**请求，微型端口驱动程序必须将**USTATUS**设置为 WWAN\_状态\_失败，并按照以下详细信息包括适用的数据：

    -   PIN 已禁用或不应 PIN：对于**WwanPinOperationEnter**集请求，当相应的 PIN 已禁用或当前不是 MB 设备的预期时，微型端口驱动程序必须将**PinType**设置为**WwanPinTypeNone**。 将忽略所有其他成员。

    -   不支持 PIN：如果 MB 设备不支持给定的 PIN，微型端口驱动程序必须将**uStatus**设置为 WWAN\_状态\_不\_设备\_支持。

    -   固定 Retrial：在此模式下，MB 设备需要重新输入 PIN，因为对于此特定类型的 PIN， **AttemptsRemaining**值仍然为非零。 微型端口驱动程序必须将**PinType**设置为与 NDIS\_WWAN\_集\_PIN**相同的值**。

    -   锁定锁定：当**AttemptsRemaining**为零时，会阻止 pin。 如果 PIN 解除阻止操作不可用，微型端口驱动程序必须将**uStatus**设置为 WWAN\_状态\_失败，并将**PinType**设置为**WwanPinTypeNone**。 将忽略所有其他成员。

        **请注意**  如果 MB 设备支持 PIN 取消阻止操作，微型端口驱动程序应按照 Pin 取消阻止步骤来响应请求。

         

    -   PIN 解除锁定：当**AttemptsRemaining**为零时，会阻止 pin。 若要解除锁定 PIN，MB 设备可能会请求相应的 PIN 解锁密钥（PUK）（如果适用）。 在这种情况下，微型端口驱动程序必须将**PinType**设置为相应的 WwanPinType*Xxx*PUK，并提供相关的详细信息。

    -   已阻止的 PUK：如果失败的试用次数超过了输入 WwanPinType*Xxx*PUK 的预设值，则 PUK 将被阻止。 微型端口驱动程序必须通过将**uStatus**设置为 WWAN\_状态\_失败，并将**PinType**设置为**WwanPinTypeNone**来指示这一点。 如果阻止 PUK1，则微型端口驱动程序必须将 NDIS\_状态\_WWAN\_就绪\_INFO，并将**ReadyState**设置为**WwanReadyStateBadSim**。

**响应 WwanPinOperationEnable、WwanPinOperationDisable 或 WwanPinOperationChange 请求**

当微型端口驱动程序使用 NDIS\_状态\_WWAN\_PIN\_信息通知以响应**WwanPinOperationEnable**、 **WwanPinOperationDisable**和**WwanPinOperationChange**时，它们应该实现以下操作：

-   对于成功的请求，微型端口驱动程序必须将**uStatus**设置为 WWAN\_状态\_成功。 对于 WWAN_PIN_INFO 中的其他成员，请参阅以下情况。

-   小型端口驱动程序必须将**uStatus**设置为 WWAN\_状态，以便 pin 启用和 pin 禁用操作在已处于请求状态时\_成功。 微型端口驱动程序必须将**PinType**设置为**WwanPinTypeNone**。 忽略其他成员。

-   当 PIN 模式从 "已禁用" 更改为 "已启用" 时，PIN 状态应为 WwanPinStateNone。

-   如果启用了 PIN1，则当电源重启到 MB 设备时，PIN 状态应变为 WwanPinStateEnter。

-   对于所有其他 Pin，PIN 状态可以从 WwanPinStateNone 更改为 WwanPinStateEnter，具体取决于 MB 设备特定的条件。

-   不支持 PIN：如果在 MB 设备上不支持 PIN 操作，微型端口驱动程序必须将**uStatus**设置为 WWAN\_状态\_不\_设备\_支持。 例如，启用和禁用 PIN2 通常不支持 MB 设备，因此必须返回上述错误代码。 将忽略所有其他成员。

-   必须输入 PIN：如果 PIN 操作要求输入 PIN，微型端口驱动程序必须将**uStatus**设置为 WWAN\_状态\_PIN\_REQUIRED，并将**PinType**设置为 WwanPinType*Xxx*。 忽略其他成员。

-   PIN 更改操作：如果仅当 MB 设备处于 "已启用" 状态时，它会限制 PIN 值的更改，则必须使用 WWAN\_状态返回处于禁用状态的请求\_PIN\_禁用。

-   PIN Retrial：出现故障时，微型端口驱动程序必须将**uStatus**设置为 WWAN\_状态\_失败，并将**PINTYPE**设置为 NDIS\_WWAN\_设置\_PIN 中指定的相同值。 除**AttemptsRemaining**之外，还将忽略其他成员。 输入错误的 PIN 时可能会发生这种情况。

-   锁定锁定：当**AttemptsRemaining**数为零时，会阻止 pin。 如果 PIN 解除阻止操作不可用，微型端口驱动程序必须将**uStatus**设置为 WWAN\_状态\_失败，并将**PinType**设置为**WwanPinTypeNone**。 应将**AttemptsRemaining**设置为0，并忽略所有其他成员。

    **请注意**  如果 MB 设备支持 PIN 取消阻止操作，微型端口驱动程序应按照 Pin 取消阻止步骤来响应请求。

     

-   解除锁定 PIN：当**AttemptsRemaining**为零时，会阻止 pin。 若要解除锁定 PIN，MB 设备可能会请求相应的 PUK （如果适用）。 在这种情况下，微型端口驱动程序必须将**uStatus**设置为 WWAN\_状态\_失败，将**PinType**设置为相应的 WwanPinType*Xxx*PUK、 **PinState**到**WwanPinStateEnter**和**AttemptsRemaining**应该允许尝试输入有效的 PUK 号。

    如果在 MB 设备或 SIM 被阻止的情况下出现 PIN 阻止结果，微型端口驱动程序必须发送事件通知，并将**ReadyState**设置为**WwanReadyStateDeviceLocked**。

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

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_PIN](oid-wwan-pin.md)

[ **\_WWAN\_PIN\_信息的 NDIS\_状态**](ndis-status-wwan-pin-info.md)

 

 




