---
title: OID_WWAN_CONNECT
description: OID_WWAN_CONNECT 激活或停用特定的数据包上下文和读取的激活状态的上下文。
ms.assetid: 51be35fe-750b-4c2b-aab3-a9df59711f7d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_CONNECT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f1982fce3fb60b3a19151a2a3ef50e5483ea0752
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544243"
---
# <a name="oidwwanconnect"></a>OID\_WWAN\_连接


OID\_WWAN\_CONNECT 激活或停用特定的数据包上下文和读取的激活状态的上下文。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_上下文\_状态**](ndis-status-wwan-context-state.md)状态通知包含[ **NDIS\_WWAN\_上下文\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567906)结构，它指示无论完成集或查询请求的 MB 设备的数据包数据协议 (PDP) 上下文状态。

调用方请求数据包数据协议 (PDP) 上下文状态的 MB 设备的设置提供[ **NDIS\_WWAN\_设置\_上下文\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567920)结构的相应信息的微型端口驱动程序。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 数据包上下文管理](https://msdn.microsoft.com/library/windows/hardware/ff559086)。

此对象会激活或停用特定的数据包上下文和读取的激活状态的上下文。 激活状态发生更改时，微型端口驱动程序必须发送相应的事件通知。

此对象称为微型端口驱动程序处于注册状态的才**WwanRegisterStateHome**， **WwanRegisterStatePartner**，或**WwanRegisterStateRoaming**。 如果数据包服务处于活动状态，设备还必须处于附加状态的**WwanPacketServiceStateAttached**。

二者都设置为查询支持和操作，此对象。

-   设置请求的处理要求的网络访问权限但不是能 SIM 访问。

-   查询请求的处理不需要访问网络或 SIM。

此 OID 的数据结构是 NDIS\_WWAN\_设置\_上下文\_状态。 微型端口驱动程序问题的状态指示的 NDIS\_状态\_WWAN\_上下文\_集和查询请求的状态。

在此版本的驱动程序模型，微型端口驱动程序将尝试上下文激活仅按 MB 服务的说明。 （微型端口驱动程序可能会激活由更高版本中的网络启动的上下文。）微型端口驱动程序必须自动激活上下文即使导致注册或信号丢失。 如果在激活请求中未提供访问字符串，微型端口驱动程序不应尝试提供默认字符串。 相反，它必须继续进行激活具有空白访问字符串的上下文。

另一方面，微型端口驱动程序可取消 MB 服务按照的说明激活上下文。 已超出阈值的信号，或作为正常关闭或状态清理的一部分暂时中断一段丢失网络连接可能会发生该错误。

由于只有一个激活上下文在此版本中，激活或停用特定的上下文相当于设置或关闭第 2 层 MB 连接支持。

在设置请求 MB 服务提供两**ConnectionId**并**ActivationCommand** WWAN 中的参数\_上下文\_状态数据结构。 它指示要激活或停用由标识数据包上下文的微型端口驱动程序**ConnectionId**根据**ActivationCommand**参数值*WwanActivationCommandActivate*或*WwanActivationCommandDeactivate*。

-   如果服务或订阅需要激活，微型端口驱动程序应返回错误代码 WWAN\_状态\_服务\_不\_已激活。 PDP 激活该服务之前可能不会发生或激活订阅。 所有紧急服务可能还会从设备和运算符的支持受可用。 操作系统可能会调用 OID\_WWAN\_服务\_激活与该错误代码的响应中。

-   如果另一个数据包上下文当前处于激活状态时，微型端口驱动程序将收到上下文激活请求，它将返回错误代码 WWAN\_状态\_最大\_ACTIVATED\_上下文。

-   如果微型端口驱动程序收到但由标识的上下文的上下文停用请求**ConnectionId**是当前未激活，则会返回错误代码 WWAN\_状态\_上下文\_不\_已激活。

微型端口驱动程序使用以下逻辑来确定从集请求 AccessString、 用户名和密码设置的有效性：

-   如果**ActivationCommand**是*WwanActivationCommandDeactivate*，微型端口驱动程序应忽略这三个参数的设置。 用例的其余部分只考虑这种情况时**ActivationCommand**是*WwanActivationCommandActivate*。

上下文激活会一直保持在用户登录和注销。 它不是每个登录用户。

在查询请求 MB 服务使用此对象以查找激活状态。

对查询请求的响应，微型端口驱动程序将发送 NDIS\_状态\_WWAN\_上下文\_状态通知。

**重要**  注意：

 

在很少见，但具体的情况下，Windows 7 上的 MB 服务可能会尝试自动连接到 Internet 的连接已确定预先存在的连接或暂时中断过程中的预先存在的 Internet 连接之前连接数。 这可能导致同时 MB 和 WLAN/以太网连接。 例如，这可能在系统启动期间时同时尝试 MB 和其他连接和网络列表管理器服务仍在尝试确定使用主动和被动方法的其他连接的 Internet 连接。 由于企业代理服务器或 ISP 网络等的网络基础结构中的临时服务中断，则可能还会发生。 因此，MB 服务可能会尝试自动连接到 internet 而不考虑是否选中"自动连接仅当没有备用的 Internet 连接是可用的"选项。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[WWAN 数据包上下文管理](https://msdn.microsoft.com/library/windows/hardware/ff559086)

 

 




