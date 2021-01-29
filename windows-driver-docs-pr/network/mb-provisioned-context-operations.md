---
title: MB 预配上下文操作
description: MB 预配上下文操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f91847b22dd2c396686059a8e8d371cd062de84d
ms.sourcegitcommit: f9651a160d34124c4b6435983efd592074ac77bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2021
ms.locfileid: "98988770"
---
# <a name="mb-provisioned-context-operations"></a>MB 预配上下文操作

预配对于其网络具有不同的 APN 配置，因此对于移动设备可连接设备而言是至关重要的。 接入点配置通常可以分为两个类别：

1. 操作系统已知的接入点配置，因为操作系统上存在需要这些连接的应用程序或客户端。
2. 不是操作系统所熟知的接入点配置，因为它们由调制解调器在内部使用，用于不能由 OS 及其客户端使用的连接。

理想情况下，该调制解调器应该只存储该操作系统不需要知道的接入点配置。 但在传统上，IHV 和 OEM 合作伙伴在调制解调器中也提供了 Internet 和购买 APNs （操作系统已知的配置）。 在 Windows 10 版本1703的版本之前，Windows 只读取 Internet，并从调制解调器购买 APN 配置以建立 Internet 连接。 从 Windows 10 版本1703开始，可能会有一些其他情况，在这种情况下，必须由 Windows 管理调制解调器的接入点配置，特别是当操作系统中有客户端（如用户设置）或需要更改蜂窝配置的 OMA DM。 这反过来也可能影响调制解调器的接入点配置。 例如，在使用 ims over IMS 的 IMS 接入点的调制解调器中可能有 IMS 堆栈。 通常情况下，这些连接不会暴露给操作系统，但在某些情况下，可能必须更改 IMS 接入点配置。 此更改可以通过 OS 完成。 为了支持这一点，从 Windows 10 开始，版本1703，操作系统可将不同类型的 APNs 配置到调制解调器。

USB 论坛的 MBIM 1.0 和 Microsoft NDIS 分别有一个现有的 CID 和 OID，以允许 OS 设置和查询调制解调器中的 APN 配置。 对于 MBIM 1.0，它通过 MBIM_CID_PROVISIONED_CONTEXT 执行此过程，而 NDIS 则通过 [OID_WWAN_PROVISIONED_CONTEXTS](./oid-wwan-provisioned-contexts.md)完成此过程。 但是，现有的 CID 和 OID 并未设计清楚地指导如何在各种情况下使用调制解调器，如电源周期或 SIM 卡交换。 如果设备要支持操作系统的配置和更新，则需要在 Windows 10 版本1703中实现新版本的 CID 和 OID。 若要确保向后兼容性，适用于想要在1703以前的操作系统版本上支持新硬件的 Ihv/Oem，它们必须继续支持现有 MBIM_CID_PROVISIONED_CONTEXT 和 OID_WWAN_PROVISIONED_CONTEXTS。  从 Windows 10 版本1703开始，如果设备支持新版本的 CID 和 OID，则操作系统将只使用较新版本的命令来查询和设置调制解调器中的 APN 上下文配置。 

## <a name="mb-interface-update-for-provisioned-context-operations"></a>用于预配上下文操作的 MB 接口更新

尽管 MBIM 具有用于检索和替换存储在调制解调器中的上下文的命令，但它没有用于 "禁用" 或 "启用" 配置文件的字段。  因此，必须更新 Windows 10 版本1703中的现有 MBIM_CID_PROVISIONED_CONTEXT 以包含此功能。 由于 MBIM 没有版本控制机制，因此新的 MSFT 专用 CID 定义为 MBIM_CID_MS_PROVISIONED_CONTEXT_V2。

服务名称 = **基本连接扩展**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 值 = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_MS_PROVISIONED_CONTEXT_V2 | 1 | Windows 10 版本 1703 |

### <a name="mbim_cid_ms_provisioned_context_v2"></a>MBIM_CID_MS_PROVISIONED_CONTEXT_V2

#### <a name="description"></a>说明

尽管 MBIM 1.0 定义了 OS 的 MBIM_CID_PROVISIONED_CONTEXT 及其上层的客户端来管理调制解调器中预配的上下文，但 Windows 通常仅在调制解调器中查询了上下文，但没有从操作系统中进行设置。 从 Windows 10 版本1703开始，操作系统需要更多的需求才能在调制解调器中配置上下文。 例如，如果在调制解调器中有一个不透明的 IMS 堆栈，则 OS 应该能够指定调制解调器应使用的 IMS 接入点。 由于每个调制解调器 IHV 都可以有自己的专有方式来将上下文存储在调制解调器中，因此 OS 无法在 ContextId 级别管理配置文件，MBIM_CID_PROVISIONED_CONTEXT 可能会建议这样做。 相反，从操作系统的角度来看，更重要的是指出要用于每个上下文类型的上下文。 返回到 IMS 示例，无论在调制解调器的现有预配上下文有多少，如果 OS 设置的上下文都具有 MBIM_CONTEXT_TYPE = IMS，则只应在该上下文上尝试使用该上下文启动的所有 IMS 通信。

MBIM 1.0 指定 MBIM_CID_PROVISIONED_CONTEXT 只能调用与插入的 SIM 卡 (的) 对中的提供程序 ID 相匹配的上下文上的查询。 对于 Set 请求，MBIM_CID_PROVISIONED_CONTEXT 可以指定要存储的上下文的提供程序 ID。  MBIM_CID_MS_PROVISIONED_CONTEXT_V2 指定类似但不同于 MBIM 1.0 的行为。 对于每个查询，操作系统继续预期调制解调器只返回与插入的 SIM 卡的提供程序 ID 匹配的上下文。 对于 "设置" 命令，该命令将不再允许 OS 设置与 SIM 卡中当前提供程序 ID 不匹配的上下文。 此设置请求应为所提供的 SIM 卡的当前提供程序 ID 创建上下文。 例如，用户从 SIM 1 调换为 SIM 2，然后再切换回 SIM 1。 预期是在第一个 SIM 交换期间，调制解调器应在为 SIM 2 加载上下文之前解析其所有上下文。 当用户调换回 SIM 1 时，应还原 SIM 1 的出厂默认配置。  对于调制解调器，无需通过 SIM 交换保存运行时配置。

下图显示了用户从一个 SIM 切换到另一个 SIM 并返回第一个 SIM 的示例流。

![调制解调器上下文设置 SIM 交换示例](images/Context_Provision_modem_context_1.png "调制解调器上下文设置 SIM 交换示例")

预配置了调制解调器的 Oem 和 Ihv 应保留原始出厂配置，以防操作系统或用户要将调制解调器中的上下文设置还原为原始设置。 只应还原当前插入的 SIM 提供程序 ID 的原始工厂上下文。 原始出厂设置预配置上下文永远不会被操作系统配置覆盖。 下图是用户选择还原出厂设置时的示例流：

![调制解调器上下文预配出厂重置示例](images/Context_Provision_modem_context_2.png "调制解调器上下文预配出厂重置示例")

如果 SIM 丢失、锁定或提供程序 ID 不可访问，则调制解调器应该会使查询或设置请求失败。 对于每个提供程序 ID，该调制解调器的每个 CONTEXT_TYPE 应只有一个上下文。 如果 IHV 或 OEM 决定将调制解调器上下文预配置到调制解调器中，请务必确保正确地为其选择的每个提供程序配置上下文。 如果插入的 SIM 卡没有 IHV 预配置上下文，则调制解调器不应在没有操作系统配置的情况下提供任何上下文。 Ihv 和 Oem 必须确保 MBIM_MS_CONTEXT_SOURCE = MbimMsContextSourceModemProvisioned，以便操作系统使用调制解调器的连接上下文（如果存在），而不会从 Windows 的 APN 数据库覆盖它。

调制解调器映射如何处理上下文，并通过现有的 MBIM_CID_PROVISIONED_CONTEXT 使其返回给每个 IHV，并超出了本文档的范围。

New MBIM_CID_MS_PROVISONED_CONTEXT_V2 命令与 MBIM 1.0 的现有 MBIM_CID_PROVISIONED_CONTEXT 命令几乎完全相同，但有几个附加项。 第一种方式是使 OS 能够启用或禁用与调制解调器中的上下文类型相关联的上下文。 如果在调制解调器中禁用了上下文，则调制解调器应该不会将存储的上下文用于与网络的任何连接，即使它们不能识别操作系统。 如果 OS 请求与调制解调器中已禁用的上下文相匹配的连接，则调制解调器应立即导致请求失败，而不会向网络发出信号。 匹配过程应匹配 MBIM_MS_CONTEXT_V2 结构中的所有字段。

MBIM 1.0 中的 MBIM_CONTEXT_IP_TYPE 结构仅用于 MBIM_CID_CONNECT。 在 MBIM_CID_MS_PROVISIONED_CONTEXT_V2 中，Microsoft 已添加了 IP 类型作为每个上下文的参数之一。 如果没有为给定的上下文配置，则调制解调器应报告 MBIMContextIPTypeDefault。 

在 Windows 10 版本1703中，如果新硬件支持 MBIM_CID_MS_PROVISIONED_CONTEXT_V2，则不会在第一方组件中使用旧 MBIM_CID_PROVISIONED_CONTEXT。 如果有其他旧的客户端/OS 组件向下发送 MBIM_CID_PROVISIONED_CONTEXT，则调制解调器应返回比 Windows 10 版本1703之前的 Windows 版本中的结果。

##### <a name="query"></a>查询

MBIM_MS_PROVISIONED_CONTEXTS_INFO 在 InformationBuffer 中从查询和设置完整消息返回。 

对于 Query，InformationBuffer 为 null。

##### <a name="set"></a>设置

对于 Set，InformationBuffer 包含 MBIM_MS_SET_PROVISIONED_CONTEXT_V2 结构。 在设置操作中，因为每个调制解调器 IHV 都可以具有管理上下文存储的专有方法，所以 OS 不再指定 ContextId 字段，并期望调制解调器将上下文映射到相应的槽。 当 OS 设置上下文时，它需要调制解调器将其用于与给定上下文的 MBIM_CONTEXT_TYPE 匹配的所有连接。 如果调制解调器不能识别 MBIM_CONTEXT_TYPE，即使它可能无法与它进行连接，它仍应该存储。

##### <a name="unsolicited-event"></a>主动事件

事件 InformationBuffer 包含 MBIM_MS_PROVISIONED_CONTEXTS_INFO_V2 结构。 在某些情况下，已设置上下文的列表由网络通过无线 (OTA) 或短消息服务更新， (SMS) 不会从操作系统中执行 MBIM_CID_MS_PROVISIONED_CONTEXT_V2 命令。 函数必须相应地更新预配上下文和标记 MBIM_MS_CONTEXT_SOURCE = MbimMsContextSourceOperatorProvisioned 的列表。 之后，函数必须使用此事件以及更新后的列表通知宿主有关更新的信息。

#### <a name="parameters"></a>参数

| Operation | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_SET_MS_PROVISIONED_CONTEXT_V2 | 不适用 | 不适用 |
| 响应 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

InformationBuffer 应为 NULL，而 InformationBufferLength 应为零。

##### <a name="set"></a>设置

以下 MBIM_SET_MS_PROVISIONED_CONTEXT_V2 数据结构应在 InformationBuffer 中使用。


| Offset | 大小 |       字段        |              类型               |                                                                                                                                                                                                                                                                                                   说明                                                                                                                                                                                                                                                                                                   |
|--------|------|--------------------|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |     Operation      |   MBIM_MS_CONTEXT_OPERATIONS    |                                             指定使用 SET 命令的操作的类型。 如果设置为 MbimMsContextOperationDelete，则应删除指定 MBIM_CONTEXT_TYPES 的上下文，并忽略 MBIM_SET_MS_PROVISIONED_CONTEXT_V2 中的其他所有字段。  如果设置为 MbimMsContextOperationRestoreFactory，则应删除所有 OS 创建的或修改的上下文，应加载默认工厂预配置上下文，并且应忽略 MBIM_SET_MS_PROVISIONED_CONTEXT_V2 中的所有其他字段。                                              |
|   4    |  16  |    ContextType     |       MBIM_CONTEXT_TYPES        |                                                                                                                                                                                                指定正在表示的上下文的类型;例如，Internet 连接、VPN (与企业网络) 或 IP (VOIP) 的连接。 有关详细信息，请参阅 MBIM_CONTEXT_TYPES 表。                                                                                                                                                                                                |
|   20   |  4   |       IPType       |      MBIM_CONTEXT_IP_TYPES      |                                                                                                                                                                                               指定正在表示的上下文的类型;例如，Internet 连接、VPN (与企业网络) 或 IP (VOIP) 的连接。 有关详细信息，请参阅 MBIM_CONTEXT_IP_TYPES 表。                                                                                                                                                                                               |
|   24   |  4   |       启用       |     MBIM_MS_CONTEXT_ENABLE      |                                                                                                                                                                     指定该调制解调器是否可以使用该上下文。 如果将其设置为 MbimMsContextDisabled，则与上下文匹配的任何 OS 连接请求都应失败，而不会向网络发出信号。 有关详细信息，请参阅 MBIM_MS_CONTEXT_ENABLE 表。                                                                                                                                                                     |
|   28   |  4   |      漫游       | MBIM_MS_CONTEXT_ROAMING_CONTROL |                                                                                                                                                                                                                                       指定是否允许漫游。 有关详细信息，请参阅 MBIM_MS_CONTEXT_ROAMING_CONTROL 表。                                                                                                                                                                                                                                        |
|   32   |  4   |     MediaType      |   MBIM_MS_CONTEXT_MEDIA_TYPE    |                                                                                                                                                                                                                                         指定使用上下文的媒体传输类型。 有关详细信息，请参阅 MBIM_MS_CONTEXT_MEDIA_TYPE 表。                                                                                                                                                                                                                                         |
|   36   |  4   |       源       |     MBIM_MS_CONTEXT_SOURCE      |                                                                                                                                                                                                                                                    指定上下文的创建源。 有关详细信息，请参阅 MBIM_MS_CONTEXT_SOURCE 表。                                                                                                                                                                                                                                                    |
|   40   |  4   | AccessStringOffset |             OFFSET              | 数据缓冲区中的偏移量到字符串 AccessString （用于访问网络）。 对于基于 GSM 的网络，此名称应为接入点名称 (APN) string，如 "data.thephone-company.com"。 对于基于 CDMA 的网络，这可能是一种特殊的拨号代码，如 "#777" 或 (NAI) 的网络访问标识符，如 " foo@thephone-company.com "。 此成员可为空，请求网络分配默认 APN。 注意：并非所有网络都支持此 NULL APN 约定，因此无效的 APN 导致的连接失败是可能的结果。 字符串的大小不应超过100个字符。 |
|   44   |  4   |  AccessStringSize  |          大小 (0.. 200)            |                                                                                                                                                                                                                                                                                           用于 AccessString 的大小。                                                                                                                                                                                                                                                                                           |
|   48   |  4   |   UserNameOffset   |             OFFSET              |                                                                                                                                                                                                                         从该结构的开头算起的偏移量（以字节为单位），表示要进行身份验证的用户名。 此成员可以为 NULL。                                                                                                                                                                                                                         |
|   52   |  4   |    UserNameSize    |          大小 (0.. 510)            |                                                                                                                                                                                                                                                                                            用于用户名的大小。                                                                                                                                                                                                                                                                                             |
|   56   |  4   |   PasswordOffset   |             OFFSET              |                                                                                                                                                                                                                           从该结构的开头算起的偏移量（以字节为单位），表示该用户名的密码。 此成员可以为 NULL。                                                                                                                                                                                                                            |
|   60   |  4   |    PasswordSize    |          大小 (0.. 510)            |                                                                                                                                                                                                                                                                                             用于密码的大小。                                                                                                                                                                                                                                                                                             |
|   64   |  4   |    压缩     |        MBIM_COMPRESSION         |                                                                                                                                                                         指定要用于标头和数据的数据连接的压缩。 此成员仅适用于基于 GSM 的设备。 主机将此成员设置为基于 CDMA 的设备的 MBIMCompressionNone。 有关详细信息，请参阅 MBIM_COMPRESSION 表。                                                                                                                                                                          |
|   68   |  4   |    AuthProtocol    |       MBIM_AUTH_PROTOCOL        |                                                                                                                                                                                                                                                   用于 PDP 激活的身份验证类型。 有关详细信息，请参阅 MBIM_AUTH_PROTOCOL 表。                                                                                                                                                                                                                                                    |
|   72   |  4   |     DataBuffer     |           DATABUFFER            |                                                                                                                                                                                                                                                                       包含 AccessString、用户名和密码的数据缓冲区。                                                                                                                                                                                                                                                                       |

前面的表中使用了以下数据结构。

MBIM_MS_CONTEXT_ROAMING_CONTROL 指定每个上下文漫游策略。 OS 可以指定是否可以在漫游期间启用给定的上下文。 如果漫游状态不满足指定的条件，则调制解调器不应自行激活上下文，而无需 OS 干预。 如果调制解调器不支持合作伙伴，则所有伙伴配置应视为等效于 home。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MbimMsContextRoamingControlHomeOnly | 0 | 指示是否只允许在家庭网络中使用该上下文。 |
| MbimMsContextRoamingControlPartnerOnly | 1 | 指示是否只允许在合作伙伴漫游网络中使用该上下文。 |
| MbimMsContextRoamingControlNonPartnerOnly | 2 | 指示是否只允许在非合作伙伴漫游网络中使用该上下文。 | 
| MbimMsContextRoamingControlHomeAndPartner | 3 | 指示是否允许在家庭和合作伙伴漫游网络中使用该上下文。 |
| MbimMsContextRoamingControlHomeAndNonPartner | 4 | 指示是否允许在家庭和非合作伙伴漫游网络中使用该上下文。 |
| MbimMsContextRoamingControlPartnerAndNonPartner | 5 | 指示是否允许在合作伙伴和非合作伙伴漫游网络中使用该上下文。 |
| MbimMsContextRoamingControlAllowAll | 6 | 指示是否允许在任何漫游条件中使用该上下文。 |

添加了 MBIM_MS_CONTEXT_MEDIA_TYPE，以便在将来的平台中支持 Wi-Fi 卸载时，指定上下文是否用于蜂窝或 iWLAN。 例如，如果将某个上下文设置为手机网络，并且当前 Wi-Fi 卸载该调制解调器，则不应使用该上下文启动连接。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MbimMsContextMediaTypeCellularOnly | 0 | 指示是否只允许在通过手机网络注册时使用上下文。 |
| MbimMsContextMediaTypeWifiOnly | 1 | 指示是否仅在通过 iWLAN 注册 (Wi-fi 卸载) 时才允许使用上下文。 |
| MbimMsContextMediaTypeAll | 2 | 指示是否允许在通过手机网络或 Wi-fi 注册时使用上下文。 |

MBIM_MS_CONTEXT_ENABLE 指定是启用还是禁用上下文。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MbimMsContextDisabled | 0 | 已设置的上下文处于禁用状态。 调制解调器不应在此上下文中从操作系统和本身启用激活。 |
| MbimMsContextEnabled | 1 | 已启用设置的上下文。 如果满足其他条件，则可以启用上下文;例如，如果不允许漫游，则漫游期间不应启用上下文。 |

添加了 MBIM_MS_CONTEXT_SOURCE，以便为操作系统提供有关如何创建调制解调器上下文的可见性。 这有助于操作系统在各种情况下（如恢复出厂设置）正常运行，因此它可以根据各种操作员要求了解应保留哪些内容以及应返回到默认状态的内容。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MbimMsContextSourceAdmin | 0 | 上下文是由操作系统的企业 IT 管理员创建的。 |
| MbimMsContextSourceUser | 1 | 上下文是用户通过 OS 设置创建的。 | 
| MbimMsContextSourceOperator | 2 | 该上下文是由运算符通过 OMA DM 或其他通道创建的。 |
| MbimMsContextSourceModem | 3 | 上下文是由在调制解调器固件附带的 IHV 或 OEM 创建的。 |
| MbimMsContextSourceDevice | 4 | 上下文是由 OS APN 数据库创建的。 |

MBIM_MS_CONTEXT_OPERATIONS 指定 OS 可以执行的操作，以在调制解调器中配置上下文。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MbimMsContextOperationDefault | 0 | 默认操作，包括添加或替换调制解调器中现有的上下文。 |
| MbimMsContextOperationDelete | 1 | 删除操作要求调制解调器删除调制解调器中现有的上下文。 | 
| MbimMsContextOperationRestoreFactory | 2 | 为当前插入的 SIM 的提供程序 ID 还原工厂预配置上下文。 应删除并替换由 OS 替换或创建的所有上下文。 如果当前插入的 SIM 提供程序 ID 没有默认预配置的操作系统上下文，则应删除该调制解调器中预配的上下文。 |

MBIM 1.0 的原始 MBIM_CONTEXT_TYPES 仍有效。 由于定义了 MBIM 1.0，Microsoft 添加了更多的上下文类型。 下表定义了要引入的新类型。 Ihv 和 Oem 可以使用其他唯一 UUID 值定义其他专用的上下文类型，操作系统不能识别这些值来实现自己的目的。

| 类型 | 值 | 说明 |
| --- | --- | --- |
| MBIMMsContextTypeAdmin | 5f7e4c2e-e80b-40a9-a239-f0abcfd11f4b | 上下文用于管理目的，例如设备管理。 |
| MBIMMSContextTypeApp | 74d88a3d-dfbd-4799-9a8c-7310a37bb2ee | 上下文用于移动运营商 allowlisted 的某些应用程序。 |
| MBIMMsContextTypeXcap | 50d378a7-baa5-4a50-b872-3fe5bb463411 | 上下文用于 IMS 服务上的 XCAP 预配。 |
| MBIMMsContextTypeTethering | 5e4e0601-48dc-4e2b-acb8-08b4016bbaac | 上下文用于移动热点 tethering。 |
| MBIMMsContextTypeEmergencyCalling | 5f41adb8-204e-4d31-9da8-b3c970e360f2 | 上下文用于 IMS 紧急呼叫。 |

##### <a name="response"></a>响应

以下 MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 (EC)  | UINT32 | DataBuffer 中后面的 MBIM_MS_CONTEXT_V2 结构的计数。 |
| 4 | 8 * EC | MsProvisionedContextV2RefList | OL_PAIR_LIST | 该对的第一个元素是以字节表示的4字节偏移量（以字节为单位），该偏移量是从该 MBIM_MS_PROVISIONED_CONTEXTS_INFO_V2 结构的开始 (偏移量 0) 计算到 MBIM_MS_CONTEXT_V2 结构的 (MBIM_MS_CONTEXT_V2 有关详细信息，请参阅) 表。 对的第二个元素是指向相应 MBIM_MS_CONTEXT_V2 结构的指针的大小为4字节。 |
| 4 + 8 * EC |  | DataBuffer | DATABUFFER | MBIM_MS_CONTEXT_V2 structuers 的数组。 |

上表中使用的 MBIM_MS_CONTEXT_V2 提供有关给定上下文的信息。


| Offset | 大小 |       字段        |              类型               |                                                                                                                                                                                                                                                                                                 说明                                                                                                                                                                                                                                                                                                  |
|--------|------|--------------------|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |     ContextId      |             UINT32              |                                                                                                                                                                                                                                                                                        此上下文的唯一 ID。                                                                                                                                                                                                                                                                                         |
|   4    |  16  |    ContextType     |       MBIM_CONTEXT_TYPES        |                                                                                                                                                      指定正在表示的上下文的类型;例如，Internet 连接、VPN (与企业网络) 或 IP (VOIP) 的连接。 设备应为空或未预配的上下文指定 MBIMContextTypeNone。 有关详细信息，请参阅 MBIM_CONTEXT_TYPES 表。                                                                                                                                                       |
|   20   |  4   |       IPType       |      MBIM_CONTEXT_IP_TYPES      |                                                                                                                                                                                                                                                                         有关详细信息，请参阅 MBIM_CONTEXT_IP_TYPES 表。                                                                                                                                                                                                                                                                          |
|   24   |  4   |       启用       |     MBIM_MS_CONTEXT_ENABLE      |                                                                                                                                                                   指定该调制解调器是否可以使用该上下文。 如果将其设置为 MbimMsContextDisabled，则与上下文匹配的任何 OS 连接请求都应失败，而不会向网络发出信号。 有关详细信息，请参阅 MBIM_MS_CONTEXT_ENABLE 表。                                                                                                                                                                    |
|   28   |  4   |      漫游       | MBIM_MS_CONTEXT_ROAMING_CONTROL |                                                                                                                                                                                                                                      指定是否允许漫游。 有关详细信息，请参阅 MBIM_MS_CONTEXT_ROAMING_CONTROL 表。                                                                                                                                                                                                                                      |
|   32   |  4   |     MediaType      |   MBIM_MS_CONTEXT_MEDIA_TYPE    |                                                                                                                                                                                                                                       指定使用上下文的媒体传输类型。 有关详细信息，请参阅 MBIM_MS_CONTEXT_MEDIA_TYPE 表。                                                                                                                                                                                                                                        |
|   36   |  4   |       源       |     MBIM_MS_CONTEXT_SOURCE      |                                                                                                                                                                                                                                                  指定上下文的创建源。 有关详细信息，请参阅 MBIM_MS_CONTEXT_SOURCE 表。                                                                                                                                                                                                                                                   |
|   40   |  4   | AccessStringOffset |             OFFSET              | 数据缓冲区中的偏移量到字符串 AccessString （用于访问网络）。 对于基于 GSM 的网络，此名称应为接入点名称 (APN) string，如 "data.thephone-company.com"。 对于基于 CDMA 的网络，这可能是一种特殊的拨号代码，如 "#777" 或 (NAI) 的网络访问标识符，如 " foo@thephone-company.com "。 此成员可以为 NULL，以请求网络分配默认 APN。 注意：并非所有网络都支持此 NULL APN 约定，因此无效的 APN 导致的连接失败是可能的结果。 字符串的大小不应超过100个字符。 |
|   44   |  4   |  AccessStringSize  |          大小 (0.. 200)            |                                                                                                                                                                                                                                                                                         用于 AccessString 的大小。                                                                                                                                                                                                                                                                                          |
|   48   |  4   |   UserNameOffset   |             OFFSET              |                                                                                                                                                                                                                       从该结构的开头算起的偏移量（以字节为单位），表示要进行身份验证的用户名。 此成员可以为 NULL。                                                                                                                                                                                                                        |
|   52   |  4   |    UserNameSize    |          大小 (0.. 510)            |                                                                                                                                                                                                                                                                                           用于用户名的大小。                                                                                                                                                                                                                                                                                           |
|   56   |  4   |   PasswordOffset   |             OFFSET              |                                                                                                                                                                                                                          从该结构的开头算起的偏移量（以字节为单位），表示该用户名的密码。 此成员可以为 NULL。                                                                                                                                                                                                                          |
|   60   |  4   |    PasswordSize    |          大小 (0.. 510)            |                                                                                                                                                                                                                                                                                           用于密码的大小。                                                                                                                                                                                                                                                                                            |
|   64   |  4   |    压缩     |        MBIM_COMPRESSION         |                                                                                                                                                                        指定要用于标头和数据的数据连接的压缩。 此成员仅适用于基于 GSM 的设备。 主机将此成员设置为基于 CDMA 的设备的 MBIMCompressionNone。 有关详细信息，请参阅 MBIM_COMPRESSION 表。                                                                                                                                                                        |
|   68   |  4   |    AuthProtocol    |       MBIM_AUTH_PROTOCOL        |                                                                                                                                                                                                                                                  用于 PDP 激活的身份验证类型。 有关详细信息，请参阅 MBIM_AUTH_PROTOCOL 表。                                                                                                                                                                                                                                                  |
|   72   |      |     DataBuffer     |           DATABUFFER            |                                                                                                                                                                                                                                                                     包含 AccessString、用户名和密码的数据缓冲区。                                                                                                                                                                                                                                                                      |

##### <a name="notification"></a>通知

有关详细信息，请参阅 MBIM_MS_PROVISIONED_CONTEXT_V2 表。

#### <a name="status-codes"></a>状态代码

对于查询和设置操作：

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | 操作失败，因为设备无法检索预配的上下文。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持此操作。 |

仅适用于集操作：

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_WRITE_FAILURE | 操作失败，因为更新请求不成功。 |