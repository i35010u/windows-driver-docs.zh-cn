---
title: NDIS_STATUS_WWAN_PIN_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PIN_INFO 通知响应 OID 查询并设置 OID_WWAN_PIN 请求。 微型端口驱动程序不能使用此通知将发送未经请求的事件。此通知使用 NDIS_WWAN_PIN_INFO 结构。
ms.assetid: fa3c2467-2240-423b-b91b-f7e19d5be353
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PIN_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 95a72a9ede200294515e37a35bc790cd89447d96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541843"
---
# <a name="ndisstatuswwanpininfo"></a>NDIS\_状态\_WWAN\_PIN\_信息


微型端口驱动程序使用 NDIS\_状态\_WWAN\_PIN\_响应 OID 查询和设置的请求的信息通知[OID\_WWAN\_PIN](oid-wwan-pin.md)。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_PIN\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567911)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序应以响应查询请求返回信息有关的 MB 设备目前需要使用个人标识识别码 (PIN)。 微型端口驱动程序应返回以下各部分中的集请求的响应中所述填写状态通知。

**对 WwanPinOperationEnter 请求的响应**

当微型端口驱动程序使用 NDIS\_状态\_WWAN\_PIN\_信息通知以响应**WwanPinOperationEnter**请求时，它们应实现这些过程：

-   对于成功**WwanPinOperationEnter**查询请求，在 MB 设备不再需要 PIN 时，必须设置微型端口驱动程序**uStatus**到 WWAN\_状态\_成功和**PinType**到**WwanPinTypeNone**。

-   用于故障**WwanPinOperationEnter**请求时，必须设置微型端口驱动程序**uStatus**到 WWAN\_状态\_故障，包括适用的数据，根据以下详细信息：

    -   PIN 已禁用或不应出现的 PIN:有关**WwanPinOperationEnter** MB 设备微型端口驱动程序必须设置预期的集请求，或者禁用相应 PIN 后或当前不**PinType**到**WwanPinTypeNone**。 所有其他成员将被忽略。

    -   不支持的 PIN:如果在 MB 设备不支持给定的 PIN，微型端口驱动程序必须设置**uStatus**到 WWAN\_状态\_否\_设备\_支持。

    -   PIN Retrial:此模式下，在 MB 设备需要 PIN 必须重新输入作为**AttemptsRemaining**值是此特定类型的 PIN 使用非零仍。 微型端口驱动程序必须设置**PinType**到相同的值的**PinType**在 NDIS\_WWAN\_设置\_PIN。

    -   固定阻止：PIN 被禁用时**AttemptsRemaining**为零。 如果 PIN 解除锁定操作不可用，微型端口驱动程序必须设置**uStatus**到 WWAN\_状态\_失败并**PinType**到**WwanPinTypeNone**. 所有其他成员将被忽略。

        **请注意**  如果 MB 设备支持 PIN 取消阻止操作，微型端口驱动程序应执行解除锁定 PIN 的步骤来对请求进行响应。

         

    -   解除锁定 PIN:PIN 被禁用时**AttemptsRemaining**为零。 解除锁定 PIN，MB 设备可能会请求相应 PIN 解锁密钥 (PUK)，如果适用。 在这种情况下，必须设置微型端口驱动程序**PinType**到相应 WwanPinType*Xxx*PUK 具有相关详细信息。

    -   已阻止的 PUK:如果失败的试验的次数超出的预设的值用于输入 WwanPinType*Xxx*PUK，然后 PUK 被阻止。 微型端口驱动程序必须通过设置指示此**uStatus**到 WWAN\_状态\_失败并**PinType**到**WwanPinTypeNone**。 如果阻止 PUK1，微型端口驱动程序必须发送 NDIS\_状态\_WWAN\_准备\_信息**ReadyState**设置为**WwanReadyStateBadSim**.

**对 WwanPinOperationEnable、 WwanPinOperationDisable 或 WwanPinOperationChange 请求作出响应**

当微型端口驱动程序使用 NDIS\_状态\_WWAN\_PIN\_信息通知以响应**WwanPinOperationEnable**， **WwanPinOperationDisable**，并**WwanPinOperationChange**，它们应实现以下操作：

-   微型端口驱动程序必须设置对成功的请求**uStatus**到 WWAN\_状态\_成功。 WWAN_PIN_INFO 中的其他成员，请参阅在以下情况。

-   微型端口驱动程序必须设置**uStatus**到 WWAN\_状态\_PIN 启用和禁用 PIN 时 PIN 已处于请求的状态的操作的成功情况。 微型端口驱动程序必须设置**PinType**到**WwanPinTypeNone**。 其他成员将被忽略。

-   在 PIN 模式从禁用更改为启用，PIN 状态应当是 WwanPinStateNone。

-   如果启用了 PIN1，PIN 状态应成为 WwanPinStateEnter 时重启到 MB 设备。

-   对于所有其他 Pin，PIN 状态可以更改从 WwanPinStateNone 为 WwanPinStateEnter 根据 MB 设备的特定条件。

-   不支持的 PIN:如果在 MB 设备不支持固定操作，必须设置微型端口驱动程序**uStatus**到 WWAN\_状态\_否\_设备\_支持。 例如，启用和禁用 pin2 码是通常设备不支持 MB 因此必须返回上述错误代码。 所有其他成员将被忽略。

-   必须输入 PIN:如果 PIN 操作要求输入 PIN，必须将微型端口驱动程序**uStatus**到 WWAN\_状态\_PIN\_REQUIRED 和**PinType**到 WwanPinType*Xxx*。 其他成员将被忽略。

-   PIN 更改操作：如果 MB 设备限制的 PIN 值更改，仅当它处于启用状态时，若要更改处于禁用状态的请求必须返回其中 WWAN\_状态\_PIN\_禁用。

-   PIN Retrial:微型端口驱动程序必须在失败时，设置**uStatus**到 WWAN\_状态\_失败，并**PinType**到相同的值中指定的 NDIS\_WWAN\_设置\_PIN。 其他成员将忽略除**AttemptsRemaining**。 这可能不正确的 PIN 输入时。

-   固定阻止：PIN 被禁用时的数量**AttemptsRemaining**为零。 如果 PIN 解除锁定操作不可用，微型端口驱动程序必须设置**uStatus**到 WWAN\_状态\_失败并**PinType**到**WwanPinTypeNone**. **AttemptsRemaining**应设置为 0，将忽略所有其他成员。

    **请注意**  如果 MB 设备支持 PIN 取消阻止操作，微型端口驱动程序应执行解除锁定 PIN 的步骤来对请求进行响应。

     

-   解除锁定 PIN:PIN 被禁用时**AttemptsRemaining**为零。 解除锁定 PIN，MB 设备可能会请求相应 PUK，如果适用。 微型端口驱动程序在这种情况下，必须设置**uStatus**到 WWAN\_状态\_故障时， **PinType**到相应 WwanPinType*Xxx*PUK，**PinState**到**WwanPinStateEnter**，并**AttemptsRemaining**应具有允许输入有效的 puk 码的尝试次数。

    如果被阻塞，阻止在 MB 设备或 SIM 中的结果的 PIN，微型端口驱动程序必须发送一封包含事件通知**ReadyState**设置为**WwanReadyStateDeviceLocked**。

-   如果在 PIN1 阻塞的时间没有活动的 PDP 上下文，微型端口驱动程序必须停用 PDP 上下文和将通知发送到有关 PDP 停用操作系统并将链接状态更改。

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


[OID\_WWAN\_PIN](oid-wwan-pin.md)

[**NDIS\_状态\_WWAN\_PIN\_信息**](ndis-status-wwan-pin-info.md)

 

 




