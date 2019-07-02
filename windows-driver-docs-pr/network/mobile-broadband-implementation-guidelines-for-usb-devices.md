---
title: USB 设备的移动宽带实施指南
description: 本主题提供了特定实现指南，以帮助为 Windows 生成符合的 USB 设备的移动宽带设备制造商。
ms.assetid: 1E8CBBCC-9E35-49AA-85A7-DFAD6772B164
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4b62c9d062d559c17366b3fec9d7e0d5f6d06dd
ms.sourcegitcommit: 2854c02cbe5b2c0010d0c64367cfe8dbd201d3f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67499803"
---
# <a name="mobile-broadband-implementation-guidelines-for-usb-devices"></a>USB 设备的移动宽带实施指南


本主题提供了特定实现指南，以帮助为 Windows 生成符合的 USB 设备的移动宽带设备制造商。 应结合[USB NCM 移动宽带接口模型 (MBIM) V1.0 规范](https://usb.org/document-library/mobile-broadband-interface-model-v10-errata-1-and-adopters-agreement)USB 发布-如果设备使用组。

本主题中的信息适用于：

-   Windows 8
-   Windows 8.1

## <a name="delaying-mbim-open"></a>延迟 MBIM 打开


MBIM 设备可能需要时间才能完成初始化，在从主机接收 MBIM 打开的邮件时。 设备应等待响应 MBIM 打开消息之前完成其初始化。 设备不应使用 MBIM 类似的错误状态消息响应\_状态\_繁忙和预期要轮询 MBIM 打开消息的设备的主机。 MBIM 打开到响应的状态不是 MBIM\_状态\_成功终止在主机上的初始化过程。

## <a name="multi-carriermulti-subscription"></a>多运营商\\多订阅


请参阅**实现支持多模式和多运营商的支持 MB 设备的 IHV 指导**有关详细信息。

**MBIM\_CID\_主页\_提供程序**

MBIM 设备必须成功设置 MBIM\_CID\_主页\_提到的情况下的以下列出的状态代码提供程序请求。 以下状态是有效的查询 MBIM\_CID\_主页\_提供程序请求，但不适用于 SET 请求。

-   **MBIM\_状态\_SIM\_不\_INSERTED** -MBIM 设备必须成功设置 MBIM\_CID\_主页\_提供程序请求且状态为 MBIM\_状态\_SIM\_不\_插入如果新的主提供程序 SIM 存在但不是插入 SIM 旧家庭提供程序。
-   **MBIM\_状态\_错误\_SIM** -MBIM 设备必须成功设置 MBIM\_CID\_主页\_MBIM 与提供程序请求\_状态\_错误\_SIM 如果新的主提供程序 SIM 很好，但旧家庭提供程序 SIM 不是错误。
-   **MBIM\_状态\_PIN\_REQUIRED** -MBIM 设备必须成功设置 MBIM\_CID\_主页\_MBIM 与提供程序请求\_状态\_PIN\_无论旧的或新 SIM 是锁定的 pin 所需。

**MBIM\_CID\_VISIBLE\_提供程序**

-   **MBIM\_状态\_SIM\_不\_INSERTED** -当 MBIM\_VISIBLE\_提供程序\_操作设置为 MBIMVisibleProvidersActionRestrictedScanMBIM 设备必须成功 MBIM\_CID\_VISIBLE\_提供程序请求与 MBIM\_状态\_SIM\_不\_插入，因为对于 SIM当前的主页提供程序不存在。
-   **MBIM\_状态\_PIN\_REQUIRED** -当 MBIM\_VISIBLE\_提供程序\_操作设置的 MBIMVisibleProvidersActionRestrictedScan MBIM 设备必须不为失败 MBIM\_CID\_VISIBLE\_提供程序请求与 MBIM\_状态\_PIN\_必需的因为当前的主页提供程序 SIM 是锁定的 PIN。

## <a name="responding-to-pin-operations"></a>对固定操作的响应


MBIM 设备必须响应时请遵循以下准则**MBIMPinOperationEnter**请求：

-   对于成功**MBIMPinOperationEnter**请求，当设备不再需要 PIN，设备必须将状态设置为 MBIM\_状态\_成功并**MBIM\_PIN\_INFO::Pin 类型**到**MBIMPinTypeNone。**
-   设备必须将状态设置为 MBIM\_状态\_PIN 启用和禁用 PIN 时 PIN 已处于请求的状态的操作的成功情况。 设备必须设置**MBIM\_PIN\_INFO::PinType**到**MBIMPinTypeNone**。 其他成员将被忽略。
-   如果 PIN 模式下从禁用更改为已启用，PIN 状态应**MBIMPinStateUnlocked**。
-   如果启用了 PIN1，PIN 状态将变为**MBIMPinStateLocked**该设备时关闭并重新打开。
-   对于所有其他 Pin，PIN 状态可以更改从**MBIMPinStateUnlocked**到**MBIMPinStateLocked**根据移动宽带设备特定的条件。
-   不支持的 PIN:如果设备不支持固定操作，设备必须将状态设置为 MBIM\_状态\_否\_设备\_支持。 例如，启用和禁用 pin2 码通常不可由移动宽带设备以便必须返回上述错误代码。 所有其他成员将被忽略。
-   必须输入 PIN:如果 PIN 操作需要输入 PIN，设备必须将状态设置为 MBIM\_状态\_PIN\_必需并**MBIM\_PIN\_INFO::PinType**到**MBIMPinTypeXxx**。 其他成员将被忽略。
-   PIN 更改操作：如果设备限制的 PIN 值更改，仅当它处于启用状态时，若要更改处于禁用状态的请求必须返回其中 MBIM\_状态\_PIN\_禁用。
-   PIN Retrial:在失败时，设备必须将状态设置为 MBIM\_状态\_失败，并**MBIM\_PIN\_INFO::PinType**为相同的值中指定**MBIM\_设置\_PIN**。 其他成员将忽略除**MBIM\_PIN\_INFO::RemainingAttempts**。 这可能不正确的 PIN 输入时。
-   固定阻止：PIN 被禁用时的数量**MBIM\_PIN\_INFO::RemainingAttempts**为零。 如果 PIN 解除锁定操作不可用，设备必须将状态设置为 MBIM\_状态\_失败并**MBIM\_PIN\_INFO::PinType**到**MBIMPinTypeNone**. **MBIM\_PIN\_INFO::RemainingAttempts**应设置为 0，将忽略所有其他成员。
    **请注意**  如果设备支持 PIN 取消阻止操作，设备应执行解除锁定 PIN 的步骤来对请求进行响应。

     

-   解除锁定 PIN:PIN 被禁用时**MBIM\_PIN\_INFO::RemainingAttempts**为零。 解除锁定 PIN，设备可能会请求相应 PUK，如果适用。 在这种情况下，设备必须将状态设置为 MBIM\_状态\_失败， **MBIM\_PIN\_INFO::PinType**到相应**MBIMPinTypeXxxPUK**， **PinState**到**MBIMPinStateLocked**，并**MBIM\_PIN\_INFO::RemainingAttempts**应具有数允许的尝试输入有效 PUK。
-   如果被阻塞，阻止在设备或 SIM 中的结果的 PIN，设备必须发送 MBIM\_CID\_订阅服务器\_准备\_包含的状态通知**ReadyState**设置为**MBIMSubscriberReadyStateDeviceLocked。**
-   如果在 PIN1 阻塞的时间没有活动的 PDP 上下文，设备必须停用 PDP 上下文并将通知发送到有关 PDP 停用的操作系统，链接状态更改。
-   对成功的请求，设备必须将状态设置为 MBIM\_状态\_成功。 其他成员将被忽略。
-   用于故障**MBIMPinOperationEnter**请求时，设备必须将状态设置为 MBIM\_状态\_故障，包括适用的数据，根据以下详细信息：
    -   PIN 已禁用或不应出现的 PIN:对于 MBIMPinOperationEnter 设置请求，如果禁用或当前未为设备所需的相应图钉，设备必须将**MBIM\_PIN\_INFO::PinType**到**MBIMPinTypeNone**。 所有其他成员将被忽略。
    -   不支持的 PIN:如果设备不支持给定的 PIN，设备必须将状态设置为 MBIM\_状态\_否\_设备\_支持。
    -   PIN Retrial:在此模式下，设备需要 PIN 必须重新输入作为**MBIM\_PIN\_INFO::RemainingAttempts**值是此特定类型的 PIN 使用非零仍。 设备必须设置**MBIM\_PIN\_INFO::PinType**到相同的值的**MBIM\_PIN\_INFO::PinType**中**MBIM\_设置\_PIN**。
    -   固定阻止：PIN 被禁用时**MBIM\_PIN\_INFO::RemainingAttempts**为零。 如果 PIN 解除锁定操作不可用，设备必须将状态设置为 MBIM\_状态\_失败并**MBIM\_PIN\_INFO::PinType**到**MBIMPinTypeNone**. 所有其他成员将被忽略。
        **请注意**  如果设备支持 PIN 取消阻止操作，设备应执行解除锁定 PIN 的步骤来对请求进行响应。

         

    -   解除锁定 PIN:PIN 被禁用时**MBIM\_PIN\_INFO::RemainingAttempts**为零。 解除锁定 PIN，设备可能会请求相应 PIN 解锁密钥 (PUK)，如果适用。 在这种情况下，设备必须设置**MBIM\_PIN\_INFO::PinType**到相应**MBIMPinTypeXxxPUK**具有相关详细信息。
    -   已阻止的 PUK:如果失败的试验的次数超过了用于输入的预设的值**MBIMPinTypeXxxPUK**，然后被阻塞，PUK。 设备必须指示这通过将状态设置为 MBIM\_状态\_失败并**MBIM\_PIN\_INFO::PinType**到**MBIMPinTypeNone**。 如果阻止 PUK1，设备必须发送 MBIM\_CID\_订阅服务器\_准备\_与状态**ReadyState**设置为**MBIMSubscriberReadyStateBadSim**.
    -   MBIM 设备必须响应时请遵循以下准则**MBIMPinOperationEnable**， **MBIMPinOperationDisable**，或**MBIMPinOperationChange**请求。

## <a name="auto-packet-service-attach"></a>自动数据包服务附加


支持自动数据包服务将附加的 MBIM 设备从移动网络自行管理附件和数据包服务分离。 主机仍可能会将附加请求发送到此类设备上用户请求。 当设备收到附加请求时从主机它应处理，如下所示：

- 如果设备未附加和不是在附加操作的中间，并且能够将附加它应启动新的附加过程与移动网络。
- 如果未附加设备，但正在自动附加操作然后它应等待自动附加操作完成，完成附加请求从具有自动附加操作的状态的主机。
- 如果已连接设备然后它应从主机附加请求成功完成。

## <a name="signal-strength-loss-and-data-connection-loss"></a>数据连接丢失和信号强度丢失


当设备丢失信号强度设备必须指明**MBIMActivationStateDeactivated**跟**MBIMPacketServiceStateDetached**跟**MBIMRegisterStateDeregistered**按该顺序。 如果设备丢失数据包服务时激活该设备上下文必须指明**MBIMActivationStateDeactivated**跟**MBIMPacketServiceStateDetached**按该顺序。 下面的序列图显示了主机和设备之间的交互。

![序列图显示了在主机和设备之间的交互。](images/mbimplementationguidelinesusb.png)

## <a name="dns-server-information"></a>DNS 服务器信息


当通过 MBIM 提供基本 IP 信息 （如在 MBIM 10.5.20.1 一节中定义）\_CID\_IP\_配置中，DNS 服务器信息 （如在 MBIM 10.5.20.1 一节中定义），也可以提供通过 MBIM\_CID\_IP\_配置。 当更新 DNS 服务器信息时，MBIM\_CID\_IP\_配置必须具有之前获取的完整基本 IP 信息。 DNS 服务器信息可以提供仅通过 MBIM\_CID\_IP\_配置即使基本 IP 信息未提供通过 MBIM\_CID\_IP\_配置。 这适用于 IPv4 和 IPv6。

## <a name="ipv6"></a>IPv6


（如 MBIM 10.5.20.1 一节中定义） 的基本 IP 信息，预期的 IP 层配置机制是从路由器公告 (RA)。 有关 DNS 服务器信息 （如 MBIM 10.5.20.1 一节中定义），预期的 IP 层配置机制是 DHCPv6。

-   **从远程协助的基本 IP 信息**-如果移动网络提供基本 IP 信息 （如在 MBIM 10.5.20.1 一节中定义） 通过远程协助，则 MBIM 设备必须允许远程协助数据包转发到主机，并且必须未截获 RA 数据包或提供基本的 IP中的远程协助数据包通过 MBIM 信息\_CID\_IP\_配置。
-   **远程协助的 DNS 服务器信息**-的唯一 IP 层配置机制的 DNS 服务器信息 （如在 MBIM 10.5.20.1 一节中定义） 受 Windows 是 DHCPv6。 MBIM 设备必须配置 DNS 服务器信息，即使存在在 RA，通过 MBIM\_CID\_IP\_配置。
-   **IP 的基本信息和 DNS 服务器信息从 DHCPv6** -如果移动网络提供基本 IP 信息和 DNS 服务器信息 （如在 MBIM 10.5.20.1 一节中定义） 从 DHCPv6，则 MBIM 设备必须允许转发 DHCPv6 数据包到主机并不能截获 DHCPv6 数据包或提供的基本 IP 信息和 DNS 服务器信息通过 MBIM 的 DHCPv6 数据包中存在\_CID\_IP\_配置。

## <a name="mbimcidradiostate"></a>MBIM\_CID\_RADIO\_STATE


MBIM 设备必须成功 MBIM\_CID\_单选\_状态的操作状态的 MBIM\_状态\_SIM\_不\_SIM 不存在时插入。 单选操作不必须由于 SIM 缺少失败。

## <a name="byte-ordering-requirements-for-authentication-cids"></a>字节排序要求身份验证的 Cid


下面列出的字节数组字段中的数据必须以主机字节顺序。

**MBIM\_CID\_SIM\_身份验证**

MBIM\_SIM\_AUTH\_REQ

1.  Rand1
2.  Rand2
3.  Rand3

**MBIM\_CID\_AKA\_AUTH**

MBIM\_AKA\_AUTH\_REQ

1.  rand
2.  Autn

MBIM\_AKA\_AUTH\_INFO

1.  res
2.  IK
3.  CK
4.  Auts

**MBIM\_CID\_AKAP\_AUTH**

MBIM\_AKAP\_AUTH\_REQ

1.  rand
2.  Autn

MBIM\_AKAP\_身份验证\_信息

1.  res
2.  IK
3.  CK
4.  Auts

## <a name="setting-link-mtu"></a>设置链接 MTU


Windows 支持仅在设备初始化配置链接最大传输单元 (MTU)。 Windows 不会更新基于报告使用 MBIM MTU 链接 MTU\_CID\_IP\_配置。 设备必须进行通信的受支持的网络链接 MTU 使用 MBIM\_功能\_DESCRIPTOR.wMaxSegmentSize。 在这种方式中报告的链接 MTU 值应至少 1280年且最多 1500年。

 

 





