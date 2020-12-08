---
title: USB 设备的移动宽带实施指南
description: 本主题提供了特定的实施指南，以帮助移动宽带设备制造商生成适用于 Windows 的兼容 USB 设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0553cacf0b8cf8c99443a5ce8e99f8b1af989de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818861"
---
# <a name="mobile-broadband-implementation-guidelines-for-usb-devices"></a>USB 设备的移动宽带实施指南


本主题提供了特定的实施指南，以帮助移动宽带设备制造商生成适用于 Windows 的兼容 USB 设备。 它应与 [USB NCM Mobile 宽带接口模型结合使用 (MBIM) v2.0 1.0 规范](https://usb.org/document-library/mobile-broadband-interface-model-v10-errata-1-and-adopters-agreement) 由 Usb 设备工作组发布。

本主题中的信息适用于：

-   Windows 8
-   Windows 8.1

## <a name="delaying-mbim-open"></a>延迟 MBIM 打开


MBIM 设备从主机收到打开的 MBIM 消息时，可能需要时间来完成初始化。 设备应等待其初始化完成，然后才能响应 MBIM 打开的消息。 设备不应响应具有错误状态的消息，如 MBIM \_ 状态 \_ 忙碌，并期望主机通过 MBIM 打开的消息来轮询设备。 对于状态不是 MBIM 状态的 MBIM 打开的响应，将 \_ \_ 终止主机上的初始化过程。

## <a name="multi-carriermulti-subscription"></a>多运营商 \\ 多订阅


有关详细信息 **，请参阅用于实现模式和多的 MB 设备的 IHV 指导** 。

**MBIM \_ CID \_ HOME \_ 提供程序**

在所述的情况下，MBIM 设备不能使 SET MBIM \_ CID \_ HOME \_ PROVIDER 请求失败，并显示以下列出状态代码。 以下状态对查询 MBIM \_ CID \_ HOME \_ 提供程序请求有效，但不适用于设置请求。

-   **MBIM \_状态 \_ SIM \_ 未 \_ 插入** -MBIM 设备不能使设置 MBIM \_ CID \_ HOME \_ PROVIDER 请求失败，状态为 \_ "未插入 MBIM 状态 SIM" （ \_ \_ \_ 如果存在新的主提供程序的 SIM，但不插入旧的 home 提供程序的 sim）。
-   **MBIM \_状态 \_ 错误的 \_ SIM** -MBIM 设备不得通过 \_ \_ \_ MBIM 状态错误的 MBIM CID HOME provider \_ 请求 \_ \_ 。如果新的主提供商的 SIM 良好，但旧 home 提供商的 sim 不正确。
-   **MBIM \_\_ \_ 需要状态 PIN** -MBIM 设备不得通过 \_ MBIM 状态 pin 设置 MBIM CID \_ HOME \_ PROVIDER 请求 \_ ， \_ \_ 不管是旧 SIM 还是新 SIM 锁定。

**MBIM \_ CID \_ 可见 \_ 提供程序**

-   **MBIM \_\_ \_ 未 \_ 插入状态 SIM** -将 MBIM \_ 可见 \_ 提供程序 \_ 操作设置为 MBIMVISIBLEPROVIDERSACTIONRESTRICTEDSCAN 时，MBIM 设备不得失败 MBIM \_ CID \_ visible \_ 提供程序请求， \_ 但 \_ 未插入 MBIM 状态 SIM， \_ \_ 因为当前 home 提供程序的 SIM 不存在。
-   **MBIM \_\_ \_ 要求提供状态 pin** -当 MBIM \_ 可见的 \_ 提供程序 \_ 操作设置为 MBIMVisibleProvidersActionRestrictedScan 时，MBIM 设备不能在 \_ \_ \_ \_ 需要 MBIM 状态 \_ PIN \_ 的情况 MBIM CID visible

## <a name="responding-to-pin-operations"></a>响应 Pin 操作


MBIM 设备在响应 **MBIMPinOperationEnter** 请求时必须遵循以下准则：

-   对于成功的 **MBIMPinOperationEnter** 请求，当设备不再需要 PIN 时，设备必须将状态设置为 " \_ 成功" \_ 和 " **MBIM \_ PIN \_ 信息：:P" 中的 "MBIM"** 设置为 " **MBIMPinTypeNone"。**
-   当 PIN 已处于请求状态时，设备必须将 "状态" 设置为 \_ \_ "pin 启用" 和 "pin 禁用" 操作的 MBIM 状态 "成功"。 设备必须将 **MBIM \_ PIN \_ 信息：:P 在** 设置为 **MBIMPinTypeNone**。 忽略其他成员。
-   当 PIN 模式从 "已禁用" 更改为 "已启用" 时，PIN 状态应为 **MBIMPinStateUnlocked**。
-   如果启用了 PIN1，当设备重启时，PIN 状态将变为 **MBIMPinStateLocked** 。
-   对于所有其他 Pin，PIN 状态可以从 **MBIMPinStateUnlocked** 更改为 **MBIMPinStateLocked** ，具体取决于移动宽带设备特定的条件。
-   不支持 PIN：如果设备不支持 PIN 操作，设备必须将状态设置为 MBIM \_ 状态 " \_ 无 \_ 设备 \_ 支持"。 例如，移动宽带设备通常不支持启用和禁用 PIN2，因此必须返回上述错误代码。 将忽略所有其他成员。
-   必须输入 PIN：如果 PIN 操作要求输入 PIN，则设备必须将 "状态" 设置为 "MBIM"，并将 " \_ \_ \_ **MBIM \_ PIN \_ 信息：:P 在** " 设置为 " **MBIMPinTypeXxx**"。 忽略其他成员。
-   PIN 更改操作：如果设备仅在处于已启用状态时限制 PIN 值的更改，则必须在禁用了 MBIM 状态 PIN 的情况下返回已禁用状态的更改请求 \_ \_ \_ 。
-   PIN Retrial：出错时，设备必须将 "状态" 设置为 "MBIM \_ \_ "，并将 " **MBIM \_ PIN \_ 信息：:P** " 设置为 **MBIM " \_ 设置 \_ PIN**" 中指定的相同值。 除 **MBIM \_ PIN \_ 信息：： RemainingAttempts** 外，还会忽略其他成员。 输入错误的 PIN 时可能会发生这种情况。
-   锁定锁定：当 **MBIM \_ pin \_ 信息：： RemainingAttempts** 的数量为零时，会阻止 pin。 如果 PIN 解除阻止操作不可用，则设备必须将状态设置为 MBIM \_ 状态 \_ 失败，并将 **MBIM \_ PIN \_ 信息：:P 在** 设置为 **MBIMPinTypeNone**。 **MBIM \_PIN \_ 信息：： RemainingAttempts** 应设置为0，并且所有其他成员均被忽略。
    **注意**  如果设备支持 PIN 取消阻止操作，则设备应遵循 PIN 取消阻止步骤来响应请求。

     

-   解除锁定 PIN： **MBIM \_ pin \_ 信息：： RemainingAttempts** 为零时，会阻止 pin。 若要解除锁定 PIN，设备可能会请求相应的 PUK （如果适用）。 在这种情况下，设备必须将 "状态" 设置为 "MBIM" \_ 状态 \_ "故障"，将 " **\_ PIN \_ 信息：:P 在** " 设置为相应的 **MBIMPinTypeXxxPUK**、 **PinState** 到 **MBIMPinStateLocked**， **MBIM \_ pin \_ 信息：： RemainingAttempts** 应具有允许输入有效 PUK 的尝试次数。
-   如果设备或 SIM 中的 PIN 阻止结果变为阻止状态，则设备必须发送 MBIM \_ CID \_ 订户 \_ 就绪 \_ 状态通知，并将 **ReadyState** 设置为 **MBIMSubscriberReadyStateDeviceLocked。**
-   如果 PIN1 阻止时存在活动的 PDP 上下文，则设备必须停用 PDP 上下文并将通知发送到操作系统，使其发生了 PDP 停用和链接状态更改。
-   对于成功的请求，设备必须将状态设置为 MBIM \_ 状态 " \_ 成功"。 忽略其他成员。
-   对于失败的 **MBIMPinOperationEnter** 请求，设备必须将状态设置为 "MBIM \_ 状态失败"， \_ 并根据以下详细信息包括适用的数据：
    -   PIN 已禁用或不应使用 PIN：对于 MBIMPinOperationEnter 集请求，当设备的相应 PIN 处于禁用状态或当前不需要时，设备必须将 **MBIM \_ PIN \_ 信息：:P 在** 设置为 **MBIMPinTypeNone**。 将忽略所有其他成员。
    -   不支持 PIN：如果设备不支持给定的 PIN，则设备必须将状态设置为 MBIM 状态 " \_ \_ 无 \_ 设备支持" \_ 。
    -   固定 Retrial：在此模式下，设备需要重新输入 PIN，因为 **MBIM \_ pin \_ 信息：： RemainingAttempts** 值对于此特定类型的 pin 仍为非零。 设备必须将 **MBIM \_ pin \_ 信息：:P 在** 设置为与 MBIM PIN 信息相同的值： **MBIM \_ 设置 \_ pin** 中的 **\_ \_ :P 在**。
    -   锁定锁定：当 **MBIM \_ pin \_ 信息：： RemainingAttempts** 为零时，会阻止 pin。 如果 PIN 解除阻止操作不可用，则设备必须将状态设置为 MBIM \_ 状态 \_ 失败，并将 **MBIM \_ PIN \_ 信息：:P 在** 设置为 **MBIMPinTypeNone**。 将忽略所有其他成员。
        **注意**  如果设备支持 PIN 取消阻止操作，则设备应遵循 PIN 取消阻止步骤来响应请求。

         

    -   PIN 解除锁定：当 **MBIM \_ pin \_ 信息：： RemainingAttempts** 为零时，会阻止 pin。 若要解除锁定 PIN，设备可能会请求相应的 PIN 解锁密钥 (PUK) （如果适用）。 在这种情况下，设备必须将 **MBIM \_ PIN \_ 信息：:P 在** 设置为相应的 **MBIMPinTypeXxxPUK** ，并提供相关的详细信息。
    -   已阻止的 PUK：如果失败的试验次数超过了输入 **MBIMPinTypeXxxPUK** 的预设值，则 PUK 将被阻止。 设备必须通过将 "状态" 设置为 "MBIM"，将 "状态" 设置为 " \_ \_ **\_ \_ :P MBIM** " **MBIMPinTypeNone**。 如果阻止 PUK1，则设备必须发送 MBIM \_ CID \_ 订户 \_ 就绪 \_ 状态，并将 **ReadyState** 设置为 **MBIMSubscriberReadyStateBadSim**。
    -   MBIM 设备在响应 **MBIMPinOperationEnable**、 **MBIMPinOperationDisable** 或 **MBIMPinOperationChange** 请求时必须遵循以下指导原则。

## <a name="auto-packet-service-attach"></a>自动数据包服务附加


支持自动数据包服务附加的 MBIM 设备会自行决定如何从移动网络管理数据包服务的附件和分离。 主机仍可能在用户请求时向此类设备发送附加请求。 当设备从主机收到附加请求时，它应按如下方式处理：

- 如果设备未连接而不是在附加操作中间并且能够附加，则它应使用移动网络启动新的附加过程。
- 如果设备未连接，但在自动附加操作中间，则它应等待自动附加操作完成，并使用自动附加操作的状态完成主机的附加请求。
- 如果设备已连接，则它应成功地从主机完成附加请求。

## <a name="signal-strength-loss-and-data-connection-loss"></a>信号强度丢失和数据连接丢失


当设备丢失信号强度时，设备必须指示 **MBIMActivationStateDeactivated** 后跟 **MBIMPacketServiceStateDetached** ，后跟 **MBIMRegisterStateDeregistered** 。 如果设备在上下文激活时丢失了数据包服务，则设备必须指示 **MBIMActivationStateDeactivated** 后跟 **MBIMPacketServiceStateDetached** 。 下面的序列图显示了主机与设备之间的交互。

![序列图显示了主机与设备之间的交互。](images/mbimplementationguidelinesusb.png)

## <a name="dns-server-information"></a>DNS 服务器信息


当 MBIM 部分 10.5.20.1) 中定义的基本 IP 信息 (通过 MBIM \_ CID \_ ip 配置提供时 \_ ，还可以通过 10.5.20.1 \_ CID \_ ip 配置提供 MBIM 部分中定义的 DNS 服务器信息 () \_ 。 当 DNS 服务器信息更新时，MBIM \_ CID \_ ip \_ CONFIGURAITON 必须具有以前获取的完整基本 IP 信息。 \_ \_ \_ 即使基本 ip 信息不是通过 MBIM \_ cid \_ ip 配置提供的 \_ ，也可以通过 MBIM cid ip 配置单独提供 DNS 服务器信息。 这同时适用于 IPv4 和 IPv6。

## <a name="ipv6"></a>IPv6


对于 "MBIM" 部分中的 ") 10.5.20.1" 部分中定义的基本 IP 信息 (，预期的 IP 层配置机制是从路由器播发 ("RA) "。 对于 MBIM 节 10.5.20.1) 中定义的 DNS 服务器信息 (，预期的 IP 层配置机制为 DHCPv6。

-   " **RA 中的基本 ip 信息**"-如果移动网络提供 MBIM 部分 10.5.20.1) via RA 中定义的基本 ip 信息 (，则 MBIM 设备必须允许将 ra 数据包转发到该主机，并且不得拦截 ra 数据包或通过 MBIM \_ CID \_ IP 配置提供 RA 数据包中提供的基本 ip 信息 \_ 。
-   **来自 RA 的 dns 服务器信息** -Windows 支持的 MBIM 节 10.5.20.1) 中定义的 dns 服务器 (信息的唯一 IP 层配置机制为 DHCPv6。 MBIM 设备必须配置 DNS 服务器信息，即使在 RA 中通过 MBIM \_ CID \_ IP 配置提供 \_ 。
-   **Dhcpv6 中的基本 ip 信息和 dns 服务器信息** -如果移动网络提供了基本 ip 信息和 dns 服务器信息 (如 MBIM 节 10.5.20.1) 中的 "DHCPv6" 中所定义），则 MBIM 设备必须允许将 dhcpv6 数据包转发到该主机，并且不得拦截 dhcpv6 数据包或通过 MBIM \_ CID \_ IP 配置提供 DHCPv6 数据包中提供的基本 ip 信息和 dns 服务器信息 \_ 。

## <a name="mbim_cid_radio_state"></a>MBIM \_ CID \_ 无线电 \_ 状态


MBIM 设备不得失败 MBIM \_ CID \_ 无线电 \_ 状态操作，其状态为 "未 \_ \_ \_ \_ 在 sim 中时插入 MBIM 状态 sim"。 由于 SIM 请假，收音机操作不得失败。

## <a name="byte-ordering-requirements-for-authentication-cids"></a>身份验证 Cid 的 Byte-Ordering 要求


下面列出的字节数组字段中的数据必须按主机字节顺序排列。

**MBIM \_ CID \_ SIM \_ 身份验证**

MBIM \_ SIM \_ 身份验证请求 \_

1.  Rand1
2.  Rand2
3.  Rand3

**MBIM \_ CID \_ 称为 \_ AUTH**

MBIM \_ 亦即 \_ 身份验证 \_ 要求

1.  Rand
2.  Autn

MBIM \_ 亦即 \_ 身份验证 \_ 信息

1.  响应
2.  IK
3.  CK
4.  Auts

**MBIM \_ CID \_ AKAP \_ AUTH**

MBIM \_ AKAP \_ AUTH \_ 请求

1.  Rand
2.  Autn

MBIM \_ AKAP \_ 身份验证 \_ 信息

1.  响应
2.  IK
3.  CK
4.  Auts

## <a name="setting-link-mtu"></a>设置链接 MTU


Windows 仅支持在设备初始化过程中配置链接最大传输单元 (MTU) 。 Windows 不会基于使用 MBIM \_ CID IP 配置报告的 mtu 更新链接 MTU \_ \_ 。 设备必须使用 MBIM 函数描述符将网络支持的链接 MTU 进行通信 \_ \_ 。 wMaxSegmentSize。 以这种方式报告的链接 MTU 值应该至少为1280，最多为1500。

 

 





