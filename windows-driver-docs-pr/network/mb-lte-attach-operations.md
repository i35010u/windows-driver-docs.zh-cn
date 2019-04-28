---
title: MB LTE 附加操作
description: MB LTE 附加操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e11ca811b7caea3538fcc6391ab2afaf78fdc77f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343336"
---
# <a name="mb-lte-attach-operations"></a>MB LTE 附加操作

## <a name="lte-attach-apn-configuration-for-mbim-modems"></a>LTE 附加 MBIM 调制解调器的 APN 配置

传统上，将附加 LTE 注册和 Windows 的一部分不直接参与了 LTE 认为附加过程。 但是，与典型的线路交换机网络注册，不同 LTE 是数据包仅限交换机的网络，需要为要维护 LTE 网络上的注册的设备启用默认 EPS 持有者。

若要建立与网络设备默认 EPS 持有者必须请求期间 LTE PDP 上下文激活附加过程中，这要求访问点名称 (APN) 规范。 3GPP 标准，每个设备在其中指定 APN 时它正在尝试 LTE 附加的四种方案：

1.  设备指定特定 LTE 附加 APN。
2.  设备指定特定 LTE 附加 APN 但网络决定让设备将连接上的另一个 APN 改为在漫游过程。
3.  设备未指定 LTE 附加 APN，并允许向设备分配一个后的网络。
4.  设备注册到 LTE 从 2g/3g 网络，已在最小的一个活动 PDP 上下文。 网络使用它 LTE 附加 APN。

现在，所有 LTE 都附加 APN 信息仅供由 Ihv 和 Oem 直接在调制解调器具有配置每个提供程序。 但是，它不是 Ihv 和 Oem 具有所有可能的 LTE 附加在全球范围内的所有运算符的 APN 设置为一个完全可扩展的模型。 从 Windows 10，版本 1703，开始新的接口定义为这两个 NDIS Oid 和 MBIM Microsoft 专有 Cid 以支持 LTE 连接 APN 配置从操作系统。 

从 Windows 10，版本 1703，如果基础硬件支持 LTE 附加 APN 配置从操作系统，则用户将能够配置 LTE 附加从设置 APN。 硬件具有默认 LTE 附加 APN 配置还必须使其配置由操作系统可用。

通过添加两个新的 Oid 和 Cid 中支持此功能。  对于实现 MBIM 的 IHV 合作伙伴，只会将 CID 版本必须受支持。

## <a name="mb-interface-update-for-lte-attach-operations"></a>LTE MB 接口更新附加操作

已创建两个新 MBIM Cid 以允许针对 LTE 连接 APN 配置和操作系统来检索最新 LTE 附加设备的状态。 如果 IHV 合作伙伴决定以支持操作系统默认 LTE 附加 APN 管理，则必须支持这两个命令。

服务名称 = **Basic 连接扩展**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID Value = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | 命令代码 | 最低 OS 版本 |
| --- | --- | --- |
| MBIM_CID_MS_LTE_ATTACH_CONFIG | 3 | Windows 10 版本 1703 |
| MBIM_CID_MS_LTE_ATTACH_STATUS | 4 | Windows 10 版本 1703 |

## <a name="mbimcidmslteattachconfig"></a>MBIM_CID_MS_LTE_ATTACH_CONFIG

### <a name="description"></a>描述

LTE 附加上下文可能会不同，具体取决于网络交互的方式与设备在运行时。 本文档的其余部分，LTE 附加上下文将引用到将附加当前正用于 LTE 的 PDP 上下文和默认 LTE 附加上下文会引用执行 LTE 在设备上配置的内容作为附加与任何其他异常时isting 启用 PDP 上下文。  MBIM_CID_MS_LTE_ATTACH_CONFIG 启用 OS 来查询和设置默认 LTE 附加插入的 SIM 的提供程序 （MCC/mnc 对） 的上下文。 

尽管 LTE 附加 APN 无法从技术上讲视为一个上下文，它不同于存储在调制解调器中的所有其他上下文。 对于所有其他上下文中激活注册后发生，并根据各种条件，操作系统可以决定其上下文是最适合连接。 但是，LTE 附加上下文已启用 LTE 网络上的设备注册过程。 操作系统不能检索注册; 完成之前将任何网络相关的状态鉴于此限制，OS 必须能够配置 LTE 不管漫游状态是 LTE 网络上注册的设备以确保设备的所有不同漫游条件可以附加上下文。

LTE 附加上下文激活与网络不需要的 OS 显式连接请求，因为操作系统并不知道任何调制解调器自行启动上下文激活。 默认 LTE 附加上下文归入此类别。 当操作系统发出 MBIM_CID_CONNECT 请求，以启用 PDP 上下文和给定的 PDP 上下文匹配以下所有时，调制解调器应完成成功的 CID 激活请求而不想打开新的无线持有者与网络：

1.  没有现有的已启用的 PDP 上下文，可启动的调制解调器不会提供给操作系统。
2.  PDP 上下文匹配 CID 请求中指定的 APN。
3.  已启用的 PDP 上下文的 IP 类型是与 CID 中请求的 IP 类型兼容。

这是非常重要，因为操作系统并不知道由调制解调器已启动的所有 PDP 上下文。 这将减少网络干扰并加载。 否则，调制解调器应显示新无线持有者匹配 OS APN 规范根据正常上下文激活请求。 此处指定的 IP 类型兼容性：

| 已启用 PDP 上下文内调制解调器的 IP 类型 | 与请求的 IP 兼容类型 | 与请求的 IP 类型不兼容 |
| --- | --- | --- |
| IPv4 | 默认设置;IPv4;IPv4v6;IPv4 和 v6 | IPv6 |
| IPv6 | 默认设置;IPv6;IPv4v6;IPv4 和 v6 | IPv4 |
| IPv4v6 | 默认设置;IPv4;IPv6;IPv4v6;IPv4 和 v6 | 无 |

> [!NOTE]
> 如果仅以无线方式启用的一个 IP 类型操作的第二个 PDP 上下文不会显示调制解调器。 例如，如果启用了 IPv4 和主机请求 IPv4 和 IPv6 然后调制解调器应而不想打开 IPv6 持有者完成激活请求。

当操作系统发出 MBIM_CID_CONNECT 请求停用 PDP 上下文然后调制解调器应检查以下内容：

1.  是否设备 LTE 附加并要停用的上下文是唯一启用 PDP 上下文维护 LTE 注册
2.  是否要停用的上下文还使用的调制解调器在内部不是任何服务公开给操作系统

如果其中任何一个为真，调制解调器应完成 CID 停用请求，但继续以保持与网络的无线持有者。 否则调制解调器应停用根据正常停用请求的上下文。

LTE 连接 APN 配置 OS 提供的所有默认值为每个提供程序，并且与插入的 SIM 卡的主页提供程序 ID （MCC/mnc 对） 匹配。 调制解调器只应提供配置的 LTE 当前插入 SIM 的提供程序 ID 进行查询时将附加上下文。 调制解调器应始终返回三个默认 LTE 附加插入的 SIM 的提供程序 ID，一个用于每个漫游条件 （主页/合作伙伴/非合作伙伴） 相匹配的上下文。

应跨 SIM 交换调制解调器应清除其默认 LTE 应用下一步的 SIM 卡的配置之前附加上下文。 如果新插入的 SIM 卡具有 LTE 无默认值附加到上下文配置，则设备应返回 NULL 空字符串的 LTE APN 保留启用的上下文时附加漫游的所有条件的上下文。 如果上下文处于禁用状态，则应为设备上 LTE 不要附加，因为没有可配置为 LTE 附加。 调制解调器时用户交换回之前已在设备配置的 SIM 卡，应还原其出厂默认设置 LTE 连接配置的 SIM 卡。 不需要运行的时配置，以在 SIM 交换中保持原样。 在任何时候，只能有一个默认 LTE 附加中每个漫游条件 （主页/合作伙伴/非合作伙伴） 调制解调器的 APN。  

操作系统将始终设置所有三个默认时发出 Set 命令时，一个用于每个漫游条件 LTE 附加上下文。 如果由操作系统提供的列表中不具有 3 Set 命令应被拒绝。 如果提供的默认 LTE 之一将附加上下文由操作系统漫游的条件匹配的当前注册状态，则调制解调器应从网络上分离并重新执行 LTE 附加与新指定 LTE 将上下文的附加配置。 否则，设备应使用指定的默认 LTE 附加上下文时漫游的条件匹配的下一个时间。  如果设备指定的默认 LTE 附加上下文无法 LTE 网络上注册，则设备应回退到 3g/2g 根据。 调制解调器无法区分合作伙伴和非合作伙伴网络，则调制解调器时应使用非合作伙伴默认 LTE 将上下文附加所有漫游方案。 如果在 OS 配置默认 LTE 附加上下文作为 IP 类型 = 默认值，则应为调制解调器分配最合适的 IP 类型为 LTE 附加上下文。  但是，操作系统需要的调制解调器仍会返回合作伙伴漫游条件和 LTE 的 IP 类型附加准确地反映了配置的上下文。

Ihv 和 Oem 可以预配置 LTE 附加上下文作为默认配置在调制解调器，但这些上下文必须标记为 MBIM_MS_CONTEXT_SOURCE = MbimMsContextSourceModemProvisioned。  

每个 3GPP 标准，LTE 附加的默认上下文可以分为两类：UE 启动和网络启动。 如果使用 NULL 空访问字符串配置该设备，设备应不提供任何 LTE 将上下文附加到网络，并等待要向设备分配一个后的网络。 MBIM 1.0 中规定的只是如果 LTE 附加上下文的 IP 类型配置为默认值，则调制解调器应选择最佳的 IP 类型基于其内部算法。

下图演示了一个示例流 LTE 附加配置。

![LTE 附加流配置示例](images/LTE_attach_1.png "LTE 附加流配置示例")

#### <a name="query"></a>查询

MBIM_MS_LTE_ATTACH_CONFIG_INFO InformationBuffer 中已完成的查询和设置消息返回。 对于查询，InformationBuffer 为 NULL。

#### <a name="set"></a>设置

对于集，InformationBuffer 包含 MBIM_MS_SET_LTE_ATTACH_CONFIG。

#### <a name="unsolicited-events"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_MS_LTE_ATTACH_CONFIG_INFO 结构。 在某些情况下，默认值 LTE 附加上下文是由网络中更新任一无线 (OTA) 或通过短信服务 (SMS)，不需要通过 MBIM_CID_MS_LTE_ATTACH_CONFIG 命令从操作系统。 该函数必须更新默认 LTE 附加上下文并将标记 MBIM_MS_CONTEXT_SOURCE 相应地 = MbimMsContextSourceOperatorProvisioned。 此后，函数必须通知主机有关更新列表使用此事件的更新。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_MS_LTE_ATTACH_CONFIG | 不适用 | 不适用 |
| 响应 | MBIM_MS_LTE_ATTACH_CONFIG_INFO | MBIM_MS_LTE_ATTACH_CONFIG_INFO | MBIM_MS_LTE_ATTACH_CONFIG_INFO |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询 

InformationBuffer 应为 NULL，并且将 InformationBufferLength 应该为零。

#### <a name="set"></a>设置

应在 InformationBuffer 中使用以下 MBIM_MS_SET_LTE_ATTACH_CONFIG 结构。 Set 命令才有效的列表包含的元素计数为 3，一个用于每个漫游条件 （主页/合作伙伴/非合作伙伴）。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 操作 | MBIM_MS_LTE_CONTEXT_OPERATIONS | 指定的操作使用 Set 命令的类型。 如果设置为 MbimMsLteAttachContextOperationRestoreFactory，则应忽略所有其他字段。 LTE 附加的 OS 创建或修改默认值应删除上下文和默认的工厂预配置 LTE 附加的默认加载上下文。 如果调制解调器不具有默认配置，则所有漫游条件默认 LTE 附加到上下文应设置为空的 APN 字符串和 IP 类型 = 默认值。 |
| 4 | 4 | ElementCount (EC) | UINT32 | 按照中 DataBuffer MBIM_MS_LTE_ATTACH_CONTEXT 计数结构。 此组件当前指定至 3，一个用于每个漫游条件 （主页/合作伙伴/非合作伙伴）。 |
| 8 | 8 * EC | MsLteAttachContextRefList | OL_PAIR_LIST | 该对的第一个元素是 4 字节的偏移量，从一开始 （偏移量为 0） 的此 MBIM_MS_LTE_ATTACH_CONFIG_INFO 结构，计算到 MBIM_MS_LTE_ATTACH_CONTEXT 结构 （有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_CONTEXT 表）。 该对的第二个元素是指针的指向相应 MBIM_MS_LTE_ATTACH_CONTEXT 结构的 4 字节大小。 |
| 8 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_LTE_ATTACH_CONTEXT 结构的数组。 |

前面的表中使用以下结构。

MBIM_MS_LTE_ATTACH_CONTEXT_OPERATIONS 介绍可以使用 Set 命令中的操作的类型。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MbimMsLteAttachContextOperationDefault | 0 | 覆盖现有默认 LTE 的默认操作将附加的上下文中调制解调器。 操作系统将始终替换所有三个默认 LTE 附加漫游条件的上下文。 |
| MbimMsLteAttachContextOperationRestoreFactory | 1 | 还原的工厂预配置的默认 LTE 的提供程序 ID 的附加上下文当前插入 SIM。 应删除并替换为 LTE 附加上下文替换或由操作系统创建的所有默认值。 如果没有默认 LTE 附加的预配置的默认值为当前上下文插入 SIM 提供程序 ID 与一个或多个漫游条件，则 LTE 附加的默认值应返回空 APN 字符串和 IP 类型 = 默认值。 |

MBIM_MS_LTE_ATTACH_CONTEXT 指定的上下文用于 LTE 附加配置。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | IPType | MBIM_CONTEXT_IP_TYPE | 有关详细信息，请参阅 MBIM_CONTEXT_IP_TYPE 表。 |
| 4 | 4 | Roaming | MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL | 指示应用于此默认设置的漫游条件 LTE 附加上下文。 有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL 表。 |
| 8 | 4 | Source | MBIM_MS_CONTEXT_SOURCE | 指定上下文的创建源。 有关详细信息，请参阅 MBIM_MS_CONTEXT_SOURCE 表。 |
| 12 | 4 | AccessStringOffset | 偏移量 | 为一个字符串，AccessString，可以访问网络的数据缓冲区中的偏移量。 对于基于 GSM 的网络，这将是"data.thephone company.com"等的访问点名称 (APN) 字符串。 字符串的大小不应超过 100 个字符。 如果 AccessString 为空，设备需要网络以将访问字符串分配回设备。 IP 类型仍必须在这种情况下指定。 |
| 16 | 4 | AccessStringSize | SIZE(0..200) | 用于 AccessString 的大小。 此值应为 0，如果设备需要网络以将访问字符串分配回设备为 LTE 附加。 |
| 20 | 4 | UserNameOffset | 偏移量 | 以字节为单位，此结构，从头计算为一个字符串，表示要进行身份验证的用户名的用户名的偏移量。 此成员可以为 NULL。 |
| 24 | 4 | UserNameSize | SIZE(0..510) | 用于用户名的大小。 |
| 28 | 4 | PasswordOffset | 偏移量 | 以字节为单位，计算为一个字符串，密码，此结构的开头的偏移量，它表示用户名的密码。 此成员可以为 NULL。 |
| 32 | 4 | PasswordSize | SIZE(0..510) | 用于密码的大小。 |
| 36 | 4 | 压缩 | MBIM_COMPRESSION | 指定要使用的数据连接中的标头和数据的压缩。 此成员仅适用于基于 GSM 的设备。 主机为基于 CDMA 的设备将此成员设置为 MBIMCompressionNone。 有关详细信息，请参阅 MBIM_COMPRESSION 表。 |
| 40 | 4 | AuthProtocol | MBIM_AUTH_PROTOCOL | 要用于 PDP 激活的身份验证类型。 有关详细信息，请参阅 MBIM_AUTH_PROTOCOL 表。 |
| 44 |  | DataBuffer | DATABUFFER | 包含 AccessString、 用户名和密码的数据缓冲区。 |

MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL 指示应用于此默认设置的漫游条件 LTE 附加上下文。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MbimMsLteAttachContextRoamingControlHome | 0 | 指示是否附加默认 LTE 上下文允许或不在家庭网络上使用。 |
| MbimMsLteAttachContextRoamingControlPartner | 1 | 指示上下文是否允许或不在合作伙伴漫游网络中使用。 |
| MbimMsLteAttachContextRoamingControlNonPartner | 2 | 指示上下文是否允许或不在非合作伙伴漫游网络中使用。 |

MBIM_MS_CONTEXT_SOURCE 指定上下文的创建源。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MbimMsContextSourceAdmin | 0 | 上下文已通过从操作系统的企业 IT 管理员。 |
| MbimMsContextSourceUser | 1 | 上下文是由通过 OS 设置的用户创建的。 |
| MbimMsContextSourceOperator | 2 | 上下文是由通过 OMA DM 或其他渠道运算符创建的。 | 
| MbimMsContextSourceModem | 3 | 上下文是由 IHV 或 OEM 创建的。 |
| MbimMsContextSourceDevice | 4 | 由 OS APN 数据库创建上下文。 |

#### <a name="response"></a>响应

应在 InformationBuffer 中使用以下 MBIM_MS_LTE_ATTACH_CONFIG_INFO 结构。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 按照中 DataBuffer MBIM_MS_LTE_ATTACH_CONTEXT 计数结构。 此组件当前指定至 3，一个用于每个漫游条件 （主页/合作伙伴/非合作伙伴）。 |
| 4 | 8 * EC | MsLteAttachContextRefList | OL_PAIR_LIST | 该对的第一个元素是 4 字节的偏移量，从一开始 （偏移量为 0） 的此 MBIM_MS_LTE_ATTACH_CONFIG_INFO 结构，计算到 MBIM_MS_LTE_ATTACH_CONTEXT 结构 （有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_CONTEXT 表）。 该对的第二个元素是指针的指向相应 MBIM_MS_LTE_ATTACH_CONTEXT 结构的 4 字节大小。 |
| 4 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_LTE_ATTACH_CONTEXT 结构的数组。 |

#### <a name="notification"></a>通知

有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_CONFIG_INFO 表。

### <a name="status-codes"></a>状态代码

对于查询和设置的操作：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | 操作失败，因为设备无法检索预配的上下文。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持该操作。 |

对于集合运算： 

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_WRITE_FAILURE  | 操作失败，因为在更新请求未成功。 |

## <a name="mbimcidmslteattachstatus"></a>MBIM_CID_MS_LTE_ATTACH_STATUS

### <a name="description"></a>描述

每个 3GPP 需求，尽管设备都可以指定 LTE 附加上下文 LTE 将附加到网络而无需任何启用 PDP 上下文时要使用的默认值可能有情况下，设备将 LTE 附加不同于默认 LTE PDP 上下文将附加在设备上配置的上下文。 下面是所有可能的方案的列表：

1.  UE 指定特定 LTE 附加 APN。
2.  UE 指定特定 LTE 附加 APN 但网络决定让设备将连接上的另一个 APN 改为在漫游过程。
3.  UE 不指定 LTE 附加 APN 并使网络分配一个可以返回到设备。
4.  UE 2g/3g 网络从注册到 LTE，已在最小的一个活动 PDP 上下文时。 网络使用它 LTE 附加 APN。

当设备默认值 LTE 附加时，它应将 MBIM_CID_MS_LTE_ATTACH_STATUS 的通知发送到操作系统最新的 LTE 附件提供的 PDP 上下文的详细信息。 默认 LTE 附加实现以下方案之一时，会发生：

1.  最初，设备将附加到 LTE 网络。
2.  设备手向上从 2g/3g LTE 到任何事先启用 PDP 上下文。

LTE 将从返回的上下文附加 MBIM_CID_LTE_ATTACH_STATUS 可能是以下值之一：

1.  默认 LTE 附加上下文存储在调制解调器。
2.  默认 LTE 附加已重新获得网络分配的上下文。

在运行时，操作系统还应该能够查询上次使用附加信息是针对 LTE 附加的默认值。 调制解调器应该返回最后一个已知默认 LTE 附加上下文。  如果设备已转交给从 LTE 2g/3g 网络，则应为调制解调器已用于以前 LTE 上下文返回附加。 它应为 APN 成为空设备注销从网络中，每次。

下图说明了示例消息流为 LTE 附加状态。

![LTE 附加状态示例流](images/LTE_attach_2.png "LTE 附加状态流示例")

#### <a name="query"></a>查询

MBIM_MS_LTE_ATTACH_STATUS InformationBuffer 中查询完成消息返回。 对于查询，InformationBuffer 为 NULL。

#### <a name="set"></a>设置 

不支持组操作。

#### <a name="unsolicited-events"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_MS_LTE_ATTACH_STATUS 结构。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | 不适用 | 不适用 |
| 响应 | 不适用 | MBIM_MS_LTE_ATTACH_STATUS | MBIM_MS_LTE_ATTACH_STATUS |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询

InformationBuffer 应为 NULL，并且将 InformationBufferLength 应该为零。

#### <a name="set"></a>设置

不支持组操作。

#### <a name="response"></a>响应

应在 InformationBuffer 中使用以下 MBIM_MS_LTE_ATTACH_STATUS 结构。


| 偏移量 | 大小 |       字段        |           在任务栏的搜索框中键入           |                                                                                                                                                                                                                                                                                                    描述                                                                                                                                                                                                                                                                                                     |
|--------|------|--------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |   LteAttachState   | MBIM_MS_LTE_ATTACH_STATE |                                                                                                                                                                                                                                    指示设备当前是否附加到 LTE 网络或不。  有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_STATE 表。                                                                                                                                                                                                                                     |
|   4    |  4   |       IPType       |  MBIM_CONTEXT_IP_TYPES   |                                                                                                                                                                                                                                                                             有关详细信息，请参阅 MBIM_CONTEXT_IP_TYPE 表。                                                                                                                                                                                                                                                                              |
|   8    |  4   | AccessStringOffset |          偏移量          | 为一个字符串，AccessString，可以访问网络的数据缓冲区中的偏移量。 对于基于 GSM 的网络，这将是"data.thephone company.com"等的访问点名称 (APN) 字符串。 对于基于 CDMA 的网络，这可能是一个特殊拨号代码，如"#777"或网络访问标识符 (NAI) 如"foo@thephone-company.com"。 此成员可以为 NULL，以请求网络分配默认 APN。 注意：并非所有网络都支持此 NULL APN 约定。 因此，引起无效 APN 连接失败是可能的结果。 字符串的大小不应超过 100 个字符。 |
|   12   |  4   |  AccessStringSize  |       SIZE(0..200)       |                                                                                                                                                                                                                                                                                        大小 （字节） 用于 AccessString。                                                                                                                                                                                                                                                                                        |
|   16   |  4   |   UserNameOffset   |          偏移量          |                                                                                                                                                                                                                          以字节为单位，此结构，从头计算为一个字符串，表示要进行身份验证的用户名的用户名的偏移量。 此成员可以为 NULL。                                                                                                                                                                                                                           |
|   20   |  4   |    UserNameSize    |       SIZE(0..510)       |                                                                                                                                                                                                                                                                                          大小 （字节） 使用的用户名。                                                                                                                                                                                                                                                                                          |
|   24   |  4   |   PasswordOffset   |          偏移量          |                                                                                                                                                                                                                             以字节为单位，计算为一个字符串，密码，此结构的开头的偏移量，它表示用户名的密码。 此成员可以为 NULL。                                                                                                                                                                                                                             |
|   28   |  4   |    PasswordSize    |       SIZE(0..510)       |                                                                                                                                                                                                                                                                                          大小 （字节） 使用的密码。                                                                                                                                                                                                                                                                                          |
|   32   |  4   |    压缩     |     MBIM_COMPRESSION     |                                                                                                                                                                           指定要使用的数据连接中的标头和数据的压缩。 此成员仅适用于基于 GSM 的设备。 主机为基于 CDMA 的设备将此成员设置为 MBIMCompressionNone。 有关详细信息，请参阅 MBIM_COMPRESSION 表。                                                                                                                                                                           |
|   36   |  4   |    AuthProtocol    |    MBIM_AUTH_PROTOCOL    |                                                                                                                                                                                                                                                     要用于 PDP 激活的身份验证类型。 有关详细信息，请参阅 MBIM_AUTH_PROTOCOL 表。                                                                                                                                                                                                                                                     |
|   40   |  4   |                    |        DataBuffer        |                                                                                                                                                                                                                                                                                                     DATABUFFER                                                                                                                                                                                                                                                                                                     |

前面的表中使用以下数据结构。

MBIM_MS_LTE_ATTACH_STATE 指示设备当前是否附加到 LTE 网络或不。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MbimMsLteAttachStateDetached | 0 | 指示设备未附加到 LTE 网络。 |
| MbimMsLteAttachStateAttached | 1 | 指示设备已连接至 LTE 网络。 |

#### <a name="notification"></a>通知

有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_STATUS 表。

### <a name="status-codes"></a>状态代码

对于查询和设置的操作：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | 操作失败，因为设备无法检索预配的上下文。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持该操作。 |
