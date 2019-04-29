---
title: MB 预配上下文操作
description: MB 预配上下文操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b472c9c19d2299ecb08f7df3999b9570e8328cec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353766"
---
# <a name="mb-provisioned-context-operations"></a>MB 预配上下文操作

预配是移动电话网络可连接的设备来说至关重要，因为每个移动运营商具有不同的 APN 配置其网络。 APN 配置通常将拆分为两个类别：

1. 由于应用程序或上面所需的这些连接的操作系统的客户端，因此已知于 OS 的 APN 配置。
2. 不会将已知的操作系统因为不供操作系统和其客户端的连接的调制解调器在内部使用的 APN 配置。

理想情况下，调制解调器应仅将存储操作系统无需知道的 APN 配置。 但是，IHV 和 OEM 合作伙伴传统上提供的 Internet 和采购 APNs，已知的 OS 中的调制解调器的配置。 在 Windows 10，版本 1703 的发行版之前 Windows 只能读取的 Internet 和采购 APN 配置从调制解调器建立 Internet 连接。 从 Windows 10，版本 1703，开始可能有其他情况下，在该调制解调器的 APN 配置必须由 Windows，尤其是当想要更改移动电话网络配置等用户设置的操作系统或 OMA DM 中的客户端。 这进而还可能会影响调制解调器的 APN 配置。 例如，可能有 IMS 堆栈中正在使用 IMS APN 适用于 SMS IMS 通过调制解调器。 通常情况下，对操作系统，但 IMS APN 配置可能需要更改某些情况下，不公开这些连接。 此更改无法通过 OS。 为了支持此功能，从 Windows 10，版本 1703 OS 可以配置不同类型的 APNs 插入调制解调器。

USB 论坛 MBIM 1.0 和 Microsoft NDIS 各有一个现有的 CID 和 OID 分别以允许操作系统来设置和查询中的调制解调器的 APN 配置。 MBIM 1.0 做到这一点通过 MBIM_CID_PROVISIONED_CONTEXT 时 ndis 做到这一点通过[OID_WWAN_PROVISIONED_CONTEXTS](https://msdn.microsoft.com/library/windows/hardware/ff569831)。 但是，现有的 CID 和 OID 的设计并未明确指导如何调制解调器的是预期行为在各种情况下，如电源周期或 SIM 交换。 需要的设备支持的 OS 配置和更新的调制解调器预配的上下文，今后将需要在 Windows 10，版本 1703年中实现的 CID 和 OID 的较新版本。 若要确保向后兼容性，为要在早于 1703年的 OS 版本上支持新硬件/Ihv Oem，他们将需要继续支持现有 MBIM_CID_PROVISIONED_CONTEXT 和 OID_WWAN_PROVISIONED_CONTEXTS。  从 Windows 10 开始，版本 1703，如果设备支持的 CID 和 OID 然后 OS 的新版本将仅使用较新版本的命令来查询和设置 APN 上下文配置调制解调器。 

## <a name="mb-interface-update-for-provisioned-context-operations"></a>预配的上下文操作 MB 界面更新

虽然 MBIM 用于检索和替换上下文存储在调制解调器的命令，它不具有"禁用"或"启用"配置文件的字段。  因此，现有 MBIM_CID_PROVISIONED_CONTEXT 必须更新适用于 Windows 10，版本 1703 引入此功能。 MBIM 没有版本控制机制，因为新的 MSFT 专有 CID 被指 MBIM_CID_MS_PROVISIONED_CONTEXT_V2。

服务名称 = **Basic 连接扩展**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID Value = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | 命令代码 | 最低 OS 版本 |
| --- | --- | --- |
| MBIM_CID_MS_PROVISIONED_CONTEXT_V2 | 1 | Windows 10 版本 1703 |

### <a name="mbimcidmsprovisionedcontextv2"></a>MBIM_CID_MS_PROVISIONED_CONTEXT_V2

#### <a name="description"></a>描述

尽管 MBIM 1.0 已定义 MBIM_CID_PROVISIONED_CONTEXT OS，其上限的客户端用来管理传统上预配的上下文中的调制解调器，Windows 仅查询的上下文中调制解调器，但未将其设置与操作系统。 从 Windows 10，版本 1703，开始没有操作系统能够在调制解调器中配置上下文的不断增长的需要。 例如，如果在对操作系统是不透明的调制解调器 IMS 堆栈，OS 应能够指定应使用调制解调器 IMS APN。 因为每个调制解调器 IHV 可以有其自己的专有方式将上下文存储在调制解调器，就无法管理 ContextId 级别 MBIM_CID_PROVISIONED_CONTEXT 可能会建议的方法上的配置文件的操作系统。 相反，从操作系统的角度来看是更重要，规定要用于每个上下文类型的上下文。 返回到 IMS 示例，而无需考虑如何许多现有的预配的上下文在调制解调器，如果 OS 设置的上下文中具有 MBIM_CONTEXT_TYPE = IMS 仅应在该上下文上尝试启动调制解调器的所有 IMS 通信。

MBIM 1.0 指定 MBIM_CID_PROVISIONED_CONTEXT 仅可以对与插入 SIM 卡的提供程序 ID （MCC/mnc 对） 匹配的上下文调用查询。 对于组请求 MBIM_CID_PROVISIONED_CONTEXT 可以指定上下文，其目的是要存储的提供程序 ID。  MBIM_CID_MS_PROVISIONED_CONTEXT_V2 指定从 MBIM 1.0 相似但不同行为。 为每个查询，OS 将继续期望调制解调器以便只返回插入 SIM 卡提供程序 ID 匹配的上下文。 对于集，该命令将不再启用与 SIM 卡中的当前提供程序 ID 不匹配的组上下文的操作系统。 应设置请求是要显示的 SIM 卡的当前提供程序 id 创建上下文。 例如，用户交换 SIM 1 为 SIM 2，然后再减少到 SIM 1。 应，第一个的 SIM 交换期间调制解调器应解析它的所有上下文之前为 SIM 2 加载上下文。 当用户交换回 SIM 1 时，应还原 SIM 1 工厂默认配置。  不需要的调制解调器，若要在 SIM 交换保存运行时配置。

下图说明了当用户从切换一个 SIM 到另一个，然后再减少到第一个示例流。

![预配 SIM 交换示例的调制解调器上下文](images/Context_Provision_modem_context_1.png "调制解调器上下文预配 SIM 交换示例")

Oem 和 Ihv 预先配置了调制解调器应保持原始配置，工厂，防止 OS 或用户想要在调制解调器将上下文设置还原为原始设置。 应还原仅的原始工厂上下文当前插入的 SIM 的提供程序 ID。 OS 的配置应永远不会覆盖原始出厂设置预配置的上下文。 在用户选择要恢复出厂设置时下, 图是为示例流：

![预配工厂的调制解调器上下文重置示例](images/Context_Provision_modem_context_2.png "预配工厂的调制解调器上下文重置示例")

期望的调制解调器，若要查询或一组请求失败时 SIM 是丢失、 被锁定，或无法访问提供程序 ID。 调制解调器应该具有每个上下文 _ 类型每个提供程序 id。 只能有一个上下文 如果 IHV 或 OEM 决定预配置调制解调器的调制解调器上下文，很重要，以确保为它选择为此，每个提供程序正确配置了上下文。 在这种情况中，插入的 SIM 卡没有 IHV 预配的上下文，调制解调器不应有任何上下文而无需操作系统的配置。 Ihv 和 Oem 必须进行确保 MBIM_MS_CONTEXT_SOURCE = MbimMsContextSourceModemProvisioned，因此操作系统将进行连接，请使用调制解调器的上下文，如果存在，并不会从 Windows 的 APN 数据库覆盖它。

调制解调器映射如何处理上下文并将其返回到现有 MBIM_CID_PROVISIONED_CONTEXT 呈现取决于每个 IHV，超出本文档讨论范围。

新 MBIM_CID_MS_PROVISONED_CONTEXT_V2 命令几乎等同于 MBIM 1.0 现有 MBIM_CID_PROVISIONED_CONTEXT 命令，但有几个新增功能。 第一个提供了启用或禁用与调制解调器中的上下文类型关联的上下文的功能的操作系统。 时上下文已禁用在调制解调器，调制解调器应不用于存储的上下文和网络，即使他们没有意识到 OS 的任何连接。 如果操作系统的请求匹配的调制解调器中的已禁用的上下文的连接，调制解调器应请求立即失败而无需信号传输到网络。 匹配过程应匹配 MBIM_MS_CONTEXT_V2 结构中的所有字段。

从 MBIM 1.0 MBIM_CONTEXT_IP_TYPE 结构仅用于 MBIM_CID_CONNECT。 在 MBIM_CID_MS_PROVISIONED_CONTEXT_V2，Microsoft 添加了 IP 类型作为为每个上下文参数之一。 如果不将其配置为给定的上下文，调制解调器应报告 MBIMContextIPTypeDefault。 

在 Windows 10 中，使用新的硬件支持 MBIM_CID_MS_PROVISIONED_CONTEXT_V2，版本 1703，旧 MBIM_CID_PROVISIONED_CONTEXT 将不使用从第一方组件。 如果向 MBIM_CID_PROVISIONED_CONTEXT 下发送其他旧的客户端 OS 组件，调制解调器需要像在早于 Windows 10，版本 1703年的 Windows 版本中返回的结果。

##### <a name="query"></a>查询

MBIM_MS_PROVISIONED_CONTEXTS_INFO InformationBuffer 中查询和设置完整的消息返回。 

对于查询，InformationBuffer 为 null。

##### <a name="set"></a>设置

对于集，InformationBuffer 包含 MBIM_MS_SET_PROVISIONED_CONTEXT_V2 结构。 在设置操作中，因为每个调制解调器 IHV 可以有管理上下文存储的专有方法不再操作系统指定的 ContextId 字段并需要调制解调器将映射到适当的插槽的上下文。 当 OS 集上下文，它预期要用于匹配给定上下文的 MBIM_CONTEXT_TYPE 的所有连接的调制解调器。 如果调制解调器不能识别 MBIM_CONTEXT_TYPE，它仍应将其存储即使它可能不能与其连接。

##### <a name="unsolicited-event"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_MS_PROVISIONED_CONTEXTS_INFO_V2 结构。 在某些情况下，预配的上下文的列表是由网络中更新任一无线 (OTA) 或通过短信服务 (SMS)，不需要通过 MBIM_CID_MS_PROVISIONED_CONTEXT_V2 命令从操作系统。 该函数必须更新预配的上下文中的列表，并标记 MBIM_MS_CONTEXT_SOURCE 相应地 = MbimMsContextSourceOperatorProvisioned。 此后，函数必须通知主机有关更新的更新列表中使用此事件。

#### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_MS_PROVISIONED_CONTEXT_V2 | 不适用 | 不适用 |
| 响应 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 | MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

InformationBuffer 应为 NULL，并且将 InformationBufferLength 应该为零。

##### <a name="set"></a>设置

应在 InformationBuffer 中使用以下 MBIM_SET_MS_PROVISIONED_CONTEXT_V2 数据结构。


| 偏移量 | 大小 |       字段        |              在任务栏的搜索框中键入               |                                                                                                                                                                                                                                                                                                   描述                                                                                                                                                                                                                                                                                                   |
|--------|------|--------------------|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |     操作      |   MBIM_MS_CONTEXT_OPERATIONS    |                                             指定的操作使用 SET 命令的类型。 如果设置为 MbimMsContextOperationDelete 则指定的上下文 MBIM_CONTEXT_TYPES 应被删除，应忽略 MBIM_SET_MS_PROVISIONED_CONTEXT_V2 中的所有其他字段。  如果设置为 MbimMsContextOperationRestoreFactory 则应删除所有 OS 创建或修改上下文时，应加载默认的工厂预配置上下文，并应忽略 MBIM_SET_MS_PROVISIONED_CONTEXT_V2 中的所有其他字段。                                              |
|   4    |  16  |    ContextType     |       MBIM_CONTEXT_TYPES        |                                                                                                                                                                                                指定要表示; 上下文的类型例如，Internet 连接、 VPN （到企业网络的连接） 或 IP 语音 (VOIP)。 有关详细信息，请参阅 MBIM_CONTEXT_TYPES 表。                                                                                                                                                                                                |
|   20   |  4   |       IPType       |      MBIM_CONTEXT_IP_TYPES      |                                                                                                                                                                                               指定要表示; 上下文的类型例如，Internet 连接、 VPN （到企业网络的连接） 或 IP 语音 (VOIP)。 有关详细信息，请参阅 MBIM_CONTEXT_IP_TYPES 表。                                                                                                                                                                                               |
|   24   |  4   |       启用       |     MBIM_MS_CONTEXT_ENABLE      |                                                                                                                                                                     指定上下文是否可以使用的调制解调器。 如果它设置为 MbimMsContextDisabled，应不到网络信号的情况下失败与上下文匹配任何 OS 连接请求。 有关详细信息，请参阅 MBIM_MS_CONTEXT_ENABLE 表。                                                                                                                                                                     |
|   28   |  4   |      Roaming       | MBIM_MS_CONTEXT_ROAMING_CONTROL |                                                                                                                                                                                                                                       指定是否允许漫游或不适用于此上下文中。 有关详细信息，请参阅 MBIM_MS_CONTEXT_ROAMING_CONTROL 表。                                                                                                                                                                                                                                        |
|   32   |  4   |     MediaType      |   MBIM_MS_CONTEXT_MEDIA_TYPE    |                                                                                                                                                                                                                                         指定上下文使用的媒体传输的类型。 有关详细信息，请参阅 MBIM_MS_CONTEXT_MEDIA_TYPE 表。                                                                                                                                                                                                                                         |
|   36   |  4   |       Source       |     MBIM_MS_CONTEXT_SOURCE      |                                                                                                                                                                                                                                                    指定上下文的创建源。 有关详细信息，请参阅 MBIM_MS_CONTEXT_SOURCE 表。                                                                                                                                                                                                                                                    |
|   40   |  4   | AccessStringOffset |             偏移量              | 在为一个字符串，AccessString，可以访问网络的数据缓冲区的偏移量。 对于基于 GSM 的网络，这将是"data.thephone company.com"等的访问点名称 (APN) 字符串。 对于基于 CDMA 的网络，这可能是一个特殊拨号代码，如"#777"或网络访问标识符 (NAI) 如"foo@thephone-company.com"。 此成员可以为 NULL，以请求网络分配默认 APN。 注意：并非所有网络都支持此 NULL APN 约定，因此引起的无效 APN 连接故障的可能结果。 字符串的大小不应超过 100 个字符。 |
|   44   |  4   |  AccessStringSize  |          SIZE(0..200)           |                                                                                                                                                                                                                                                                                           用于 AccessString 的大小。                                                                                                                                                                                                                                                                                           |
|   48   |  4   |   UserNameOffset   |             偏移量              |                                                                                                                                                                                                                         以字节为单位，此结构，从头计算为一个字符串，表示要进行身份验证的用户名的用户名的偏移量。 此成员可以为 NULL。                                                                                                                                                                                                                         |
|   52   |  4   |    UserNameSize    |          SIZE(0..510)           |                                                                                                                                                                                                                                                                                            用于用户名的大小。                                                                                                                                                                                                                                                                                             |
|   56   |  4   |   PasswordOffset   |             偏移量              |                                                                                                                                                                                                                           以字节为单位，计算为一个字符串，密码，此结构的开头的偏移量，它表示用户名的密码。 此成员可以为 NULL。                                                                                                                                                                                                                            |
|   60   |  4   |    PasswordSize    |          SIZE(0..510)           |                                                                                                                                                                                                                                                                                             用于密码的大小。                                                                                                                                                                                                                                                                                             |
|   64   |  4   |    压缩     |        MBIM_COMPRESSION         |                                                                                                                                                                         指定要使用的数据连接中的标头和数据的压缩。 此成员仅适用于基于 GSM 的设备。 主机为基于 CDMA 的设备将此成员设置为 MBIMCompressionNone。 有关详细信息，请参阅 MBIM_COMPRESSION 表。                                                                                                                                                                          |
|   68   |  4   |    AuthProtocol    |       MBIM_AUTH_PROTOCOL        |                                                                                                                                                                                                                                                   要用于 PDP 激活的身份验证类型。 有关详细信息，请参阅 MBIM_AUTH_PROTOCOL 表。                                                                                                                                                                                                                                                    |
|   72   |  4   |     DataBuffer     |           DATABUFFER            |                                                                                                                                                                                                                                                                       包含 AccessString、 用户名和密码的数据缓冲区。                                                                                                                                                                                                                                                                       |

前面的表中使用以下数据结构。

MBIM_MS_CONTEXT_ROAMING_CONTROL 指定每个上下文漫游策略。 操作系统可以指定在漫游时是否可启用给定的上下文。 如果漫游状态不符合指定的条件，调制解调器应自激活而无需 OS 干预的上下文。 在中的调制解调器不支持合作伙伴，则所有合作伙伴配置的情况下应被视为等效到主页。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MbimMsContextRoamingControlHomeOnly | 0 | 指示是否仅允许在上下文或不在家庭网络中使用。 |
| MbimMsContextRoamingControlPartnerOnly | 1 | 指示是否仅允许在上下文或不在合作伙伴漫游网络中使用。 |
| MbimMsContextRoamingControlNonPartnerOnly | 2 | 指示是否仅允许在上下文或不在非合作伙伴漫游网络中使用。 | 
| MbimMsContextRoamingControlHomeAndPartner | 3 | 指示上下文是否允许在家庭和合作伙伴漫游网络中使用。 |
| MbimMsContextRoamingControlHomeAndNonPartner | 4 | 指示上下文是否允许在家庭和非合作伙伴漫游网络中使用。 |
| MbimMsContextRoamingControlPartnerAndNonPartner | 5 | 指示上下文是否允许合作伙伴和非合作伙伴漫游网络中使用。 |
| MbimMsContextRoamingControlAllowAll | 6 | 指示上下文是否允许在任何漫游条件中使用。 |

添加了 MBIM_MS_CONTEXT_MEDIA_TYPE 能够指定是否为移动电话网络使用的上下文或 iWLAN Wi-fi 卸载时将成为受支持的将来平台。 例如，如果上下文设置为移动电话和调制解调器目前 Wi-fi 然后卸载它不应启动的连接使用该上下文。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MbimMsContextMediaTypeCellularOnly | 0 | 指示是否仅允许上下文用于注册通过移动电话网络。 |
| MbimMsContextMediaTypeWifiOnly | 1 | 指示是否仅允许上下文用于注册通过 iWLAN （Wi-fi 卸载）。 |
| MbimMsContextMediaTypeAll | 2 | 指示是否允许上下文用于注册通过移动电话或 Wi-fi。 |

MBIM_MS_CONTEXT_ENABLE 指定是启用还是禁用了上下文。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MbimMsContextDisabled | 0 | 禁用预配的上下文。 调制解调器不应启用此上下文从操作系统和本身上的激活。 |
| MbimMsContextEnabled | 1 | 启用预配的上下文。 如果满足其他条件; 可以启用上下文例如，如果漫游不允许则上下文应不启用漫游过程。 |

添加了 MBIM_MS_CONTEXT_SOURCE，以提供对调制解调器上下文的创建方式 OS 可见性。 这有助于在各种情况下，例如恢复出厂设置后正常运行的操作系统，因此它可以知道什么应保持不变并为默认状态基于各种运算符要求应返回的内容。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MbimMsContextSourceAdmin | 0 | 上下文已通过从操作系统的企业 IT 管理员。 |
| MbimMsContextSourceUser | 1 | 由用户通过 OS 设置已创建了上下文。 | 
| MbimMsContextSourceOperator | 2 | 上下文是由通过 OMA DM 或其他渠道运算符创建的。 |
| MbimMsContextSourceModem | 3 | 上下文是由 IHV 或 OEM 所包含的调制解调器固件创建的。 |
| MbimMsContextSourceDevice | 4 | 由 OS APN 数据库创建上下文。 |

MBIM_MS_CONTEXT_OPERATIONS 指定操作系统的操作可以执行在调制解调器中配置上下文。

| 在任务栏的搜索框中键入 | 值 | 描述 |
| --- | --- | --- |
| MbimMsContextOperationDefault | 0 | 默认操作包括添加或替换现有上下文在调制解调器。 |
| MbimMsContextOperationDelete | 1 | 删除操作需要删除现有上下文在调制解调器的调制解调器。 | 
| MbimMsContextOperationRestoreFactory | 2 | 还原当前插入 SIM 的提供程序 id 的工厂预配置的上下文。 替换还是由操作系统创建的所有上下文应删除和替换。 如果没有为当前插入 SIM 提供程序 ID，无默认值预先配置的 OS 上下文，则应删除调制解调器中预配的上下文。 |

MBIM 1.0 从原始 MBIM_CONTEXT_TYPES 仍然有效。 随着更多类型的上下文引入的自定义 MBIM 1.0 以来，Microsoft 将添加附加的上下文类型。 下表定义正在引入的新类型。 Ihv 和 Oem 可以定义其他唯一的 UUID 值不会由操作系统识别为其自身的用途与其他专有上下文类型。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMMsContextTypeAdmin | 5f7e4c2e-e80b-40a9-a239-f0abcfd11f4b | 上下文用于管理目的，例如设备管理。 |
| MBIMMSContextTypeApp | 74d88a3d-dfbd-4799-9a8c-7310a37bb2ee | 上下文用于通过移动运营商的特定应用程序加入允许列表。 |
| MBIMMsContextTypeXcap | 50d378a7-baa5-4a50-b872-3fe5bb463411 | XCAP 预配 IMS 服务上使用的上下文。 |
| MBIMMsContextTypeTethering | 5e4e0601-48dc-4e2b-acb8-08b4016bbaac | 上下文用于移动热点 tethering。 |
| MBIMMsContextTypeEmergencyCalling | 5f41adb8-204e-4d31-9da8-b3c970e360f2 | 上下文用于 IMS 拨打紧急电话。 |

##### <a name="response"></a>响应

应在 InformationBuffer 中使用以下 MBIM_MS_PROVISIONED_CONTEXT_INFO_V2 结构。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 按照中 DataBuffer MBIM_MS_CONTEXT_V2 计数结构。 |
| 4 | 8 * EC | MsProvisionedContextV2RefList | OL_PAIR_LIST | 该对的第一个元素是一个 4 字节偏移量以字节为单位，从一开始 （偏移量为 0） 的此 MBIM_MS_PROVISIONED_CONTEXTS_INFO_V2 结构，计算向 MBIM_MS_CONTEXT_V2 结构 （有关详细信息，请参阅 MBIM_MS_CONTEXT_V2 表）。 该对的第二个元素是指针的指向相应 MBIM_MS_CONTEXT_V2 结构的 4 字节大小。 |
| 4 + 8 * EC |  | DataBuffer | DATABUFFER | MBIM_MS_CONTEXT_V2 structuers 的数组。 |

MBIM_MS_CONTEXT_V2，使用在上表中，提供有关给定的上下文信息。


| 偏移量 | 大小 |       字段        |              在任务栏的搜索框中键入               |                                                                                                                                                                                                                                                                                                 描述                                                                                                                                                                                                                                                                                                  |
|--------|------|--------------------|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |     ContextId      |             UINT32              |                                                                                                                                                                                                                                                                                        此上下文的唯一 ID。                                                                                                                                                                                                                                                                                         |
|   4    |  16  |    ContextType     |       MBIM_CONTEXT_TYPES        |                                                                                                                                                      指定要表示; 上下文的类型例如，Internet 连接、 VPN （到企业网络的连接） 或 IP 语音 (VOIP)。 设备应为空或未设置上下文指定 MBIMContextTypeNone。 有关详细信息，请参阅 MBIM_CONTEXT_TYPES 表。                                                                                                                                                       |
|   20   |  4   |       IPType       |      MBIM_CONTEXT_IP_TYPES      |                                                                                                                                                                                                                                                                         有关详细信息，请参阅 MBIM_CONTEXT_IP_TYPES 表。                                                                                                                                                                                                                                                                          |
|   24   |  4   |       启用       |     MBIM_MS_CONTEXT_ENABLE      |                                                                                                                                                                   指定上下文是否可以使用的调制解调器。 如果它设置为 MbimMsContextDisabled，应不到网络信号的情况下失败与上下文匹配任何 OS 连接请求。 有关详细信息，请参阅 MBIM_MS_CONTEXT_ENABLE 表。                                                                                                                                                                    |
|   28   |  4   |      Roaming       | MBIM_MS_CONTEXT_ROAMING_CONTROL |                                                                                                                                                                                                                                      指定是否允许漫游或不适用于此上下文中。 有关详细信息，请参阅 MBIM_MS_CONTEXT_ROAMING_CONTROL 表。                                                                                                                                                                                                                                      |
|   32   |  4   |     MediaType      |   MBIM_MS_CONTEXT_MEDIA_TYPE    |                                                                                                                                                                                                                                       指定上下文使用的媒体传输的类型。 有关详细信息，请参阅 MBIM_MS_CONTEXT_MEDIA_TYPE 表。                                                                                                                                                                                                                                        |
|   36   |  4   |       Source       |     MBIM_MS_CONTEXT_SOURCE      |                                                                                                                                                                                                                                                  指定上下文的创建源。 有关详细信息，请参阅 MBIM_MS_CONTEXT_SOURCE 表。                                                                                                                                                                                                                                                   |
|   40   |  4   | AccessStringOffset |             偏移量              | 为一个字符串，AccessString，可以访问网络的数据缓冲区中的偏移量。 对于基于 GSM 的网络，这将是"data.thephone company.com"等的访问点名称 (APN) 字符串。 对于基于 CDMA 的网络，这可能是一个特殊拨号代码，如"#777"或网络访问标识符 (NAI) 如"foo@thephone-company.com"。 此成员可以为 NULL，以请求网络分配默认 APN。 注意：并非所有网络都支持此 NULL APN 约定，因此引起的无效 APN 连接故障的可能结果。 字符串的大小不应超过 100 个字符。 |
|   44   |  4   |  AccessStringSize  |          SIZE(0..200)           |                                                                                                                                                                                                                                                                                         用于 AccessString 的大小。                                                                                                                                                                                                                                                                                          |
|   48   |  4   |   UserNameOffset   |             偏移量              |                                                                                                                                                                                                                       以字节为单位，此结构，从头计算为一个字符串，表示要进行身份验证的用户名的用户名的偏移量。 此成员可以为 NULL。                                                                                                                                                                                                                        |
|   52   |  4   |    UserNameSize    |          SIZE(0..510)           |                                                                                                                                                                                                                                                                                           大小使用的用户名。                                                                                                                                                                                                                                                                                           |
|   56   |  4   |   PasswordOffset   |             偏移量              |                                                                                                                                                                                                                          以字节为单位，计算为一个字符串，密码，此结构的开头的偏移量，它表示用户名的密码。 此成员可以为 NULL。                                                                                                                                                                                                                          |
|   60   |  4   |    PasswordSize    |          SIZE(0..510)           |                                                                                                                                                                                                                                                                                           用于密码的大小。                                                                                                                                                                                                                                                                                            |
|   64   |  4   |    压缩     |        MBIM_COMPRESSION         |                                                                                                                                                                        指定要使用的数据连接中的标头和数据的压缩。 此成员仅适用于基于 GSM 的设备。 主机为基于 CDMA 的设备将此成员设置为 MBIMCompressionNone。 有关详细信息，请参阅 MBIM_COMPRESSION 表。                                                                                                                                                                        |
|   68   |  4   |    AuthProtocol    |       MBIM_AUTH_PROTOCOL        |                                                                                                                                                                                                                                                  要用于 PDP 激活的身份验证类型。 有关详细信息，请参阅 MBIM_AUTH_PROTOCOL 表。                                                                                                                                                                                                                                                  |
|   72   |      |     DataBuffer     |           DATABUFFER            |                                                                                                                                                                                                                                                                     包含 AccessString、 用户名和密码的数据缓冲区。                                                                                                                                                                                                                                                                      |

##### <a name="notification"></a>通知

有关详细信息，请参阅 MBIM_MS_PROVISIONED_CONTEXT_V2 表。

#### <a name="status-codes"></a>状态代码

对于查询和设置的操作：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | 操作失败，因为设备无法检索预配的上下文。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持该操作。 |

对于集合运算：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_WRITE_FAILURE | 操作失败，因为在更新请求未成功。 |


