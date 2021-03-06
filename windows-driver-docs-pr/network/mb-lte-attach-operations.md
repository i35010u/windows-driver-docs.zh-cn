---
title: MB LTE 附加操作
description: MB LTE 附加操作
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: e9b4341d0adc5a78fd7cc99124fd12b42038aaf7
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248002"
---
# <a name="mb-lte-attach-operations"></a>MB LTE 附加操作

## <a name="lte-attach-apn-configuration-for-mbim-modems"></a>适用于 MBIM 调制解调器的 LTE 附加 APN 配置

传统上，已将 LTE 附加视为注册的一部分，并且 Windows 未直接加入到 LTE 附加过程中。 但是，与典型线路交换机网络注册不同，LTE 是一种仅限数据包交换机的网络，需要为设备启用默认 EPS 持有者，以维护 LTE 网络上的注册。

若要通过网络建立默认 EPS 持有者，设备必须在 LTE 附加过程期间请求 PDP 上下文激活，这需要访问点名称 (APN) 规范。 根据3GPP 标准，在以下四种情况下，设备在尝试 LTE 连接时可以指定 APN：

1.  设备指定特定的 LTE 附加接入点。
2.  设备指定特定的 LTE 附加接入点，但网络决定允许设备在漫游时改为在另一个 APN 上附加。
3.  设备不指定 LTE 附加 APN，并允许网络将其分配给设备。
4.  从 2G/3G 网络注册到 LTE 的设备，并且已经有至少一个活动的 PDP 上下文。 网络使用该网络作为 LTE 附加 APN。

如今，所有 LTE 附加 APN 信息由 Ihv 和 Oem 直接在调制解调器中为其配置的每个提供程序提供。 但是，它并不是一个完全可缩放的模型，因此对于所有全球的操作员，其所有可能的 LTE 附加 APN 设置都是完全可缩放的。 从 Windows 10 1703 版开始，为 NDIS Oid 和 MBIM Microsoft 专用 Cid 定义了新的接口，以支持来自 OS 的 LTE 附加接入点配置。 

从 Windows 10 版本1703开始，如果基础硬件支持从操作系统连接到 LTE 附加 APN，则用户将能够从设置配置 LTE 附加 APN。 具有默认 LTE 附加 APN 配置的硬件还必须使其配置可供操作系统使用。

通过添加两个新的 Oid 和 Cid，支持此功能。  对于实现 MBIM 的 IHV 合作伙伴，只需要支持 CID 版本。

## <a name="mb-interface-update-for-lte-attach-operations"></a>用于 LTE 附加操作的 MB 接口更新

创建了两个新的 MBIM Cid，以允许 LTE 附加 APN 配置和 OS 检索设备的最新 LTE 附加状态。 如果 IHV 合作伙伴决定支持 OS 默认的 LTE 附加 APN 管理，则必须支持这两个命令。

服务名称 = **基本连接扩展**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 值 = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_MS_LTE_ATTACH_CONFIG | 3 | Windows 10 版本 1703 |
| MBIM_CID_MS_LTE_ATTACH_STATUS | 4 | Windows 10 版本 1703 |

## <a name="mbim_cid_ms_lte_attach_config"></a>MBIM_CID_MS_LTE_ATTACH_CONFIG

### <a name="description"></a>描述

LTE 附加上下文可能不同，具体取决于网络在运行时如何与设备交互。 在本文档的其余部分中，LTE 附加上下文将称为当前用于 LTE 附加的 PDP 上下文，默认的 LTE 附加上下文将被称为当没有其他已启用的 PDP 上下文时，在执行 LTE 附加的设备上配置的内容。  MBIM_CID_MS_LTE_ATTACH_CONFIG 使 OS 能够查询和设置插入的 SIM 提供程序的默认 LTE 附加上下文 (MCC/MNC 对) 。 

虽然在技术上可以将 LTE 附加 APN 视为上下文，但它与存储在调制解调器中的所有其他上下文不同。 对于在注册后进行的所有其他上下文激活，操作系统可以根据各种条件确定最适合连接的上下文。 但是，在 LTE 网络上，在设备注册过程中启用了 LTE 附加上下文。 在完成注册之前，操作系统无法检索任何与网络相关的状态;由于此限制，操作系统必须能够为设备的所有不同漫游条件配置 LTE 附加上下文，以确保设备可以在 LTE 网络上注册，而不考虑漫游状态。

使用网络的 LTE 附加上下文激活不需要操作系统显式连接请求，因为 OS 不知道调制解调器自行启动的上下文激活。 默认 LTE 附加上下文属于此类别。 当 OS 发出 MBIM_CID_CONNECT 请求以启用 PDP 上下文并且给定的 PDP 上下文与以下所有内容匹配时，该调制解调器应完成该 CID 激活请求并取得成功，而不会通过网络引入新的无线持有者：

1.  有一个已启用的现有 PDP 上下文，该上下文由调制解调器启动，而不会提供给操作系统。
2.  PDP 上下文与 CID 请求中的指定 APN 匹配。
3.  启用的 PDP 上下文的 IP 类型与 CID 中请求的 IP 类型兼容。

这一点很重要，因为 OS 不能识别调制解调器启动的所有 PDP 上下文。 这会减少网络干扰和负载。 否则，该调制解调器应根据普通上下文激活请求，打开一个新的无线持有者匹配操作系统接入点规范。 IP 类型兼容性在此处指定：

| 调制解调器内启用的 PDP 上下文的 IP 类型 | 与请求的 IP 类型 () 兼容 | 与请求的 IP 类型不兼容 |
| --- | --- | --- |
| IPv4 | 缺省值IPv4IPv4v6;IPv4 和 v6 | IPv6 |
| IPv6 | 缺省值IPv6IPv4v6;IPv4 和 v6 | IPv4 |
| IPv4v6 | 缺省值IPv4IPv6IPv4v6;IPv4 和 v6 | 无 |

> [!NOTE]
> 如果无线上仅启用了一个 IP 类型，则调制解调器不应显示第二个 PDP 上下文。 例如，如果启用了 IPv4 并且主机请求 IPv4 和 IPv6，则调制解调器应完成激活请求，而不会启动 IPv6 持有者。

当 OS 发出 MBIM_CID_CONNECT 请求停用 PDP 上下文时，调制解调器应检查以下各项：

1.  设备是否已连接到 LTE 并且要停用的上下文是唯一启用的 PDP 上下文来维护 LTE 注册
2.  对于未向操作系统公开的任何服务，调制解调器是否也在内部使用要停用的上下文

如果这两个条件都为 true，则调制解调器应完成 CID 停用请求，但继续维护网络的无线持有者。 否则，调制解调器应根据正常的停用请求停用上下文。

OS 提供的所有默认 LTE 附加 APN 配置均为每个提供程序，并与插入的 SIM 卡的主提供程序 ID (MCC/MNC 对) 。 查询时，该调制解调器应该只为当前插入的 SIM 的提供程序 ID 提供配置的 LTE 附加上下文。 调制解调器应始终返回三个默认的 LTE 附加上下文，它们与插入的 SIM 卡的提供程序 ID 相匹配，每个漫游条件 (home/partner/非合作伙伴) 。

预计在进行 SIM 交换时，调制解调器应在为下一个 SIM 卡应用配置之前清除其默认的 LTE 附加上下文。 如果新插入的 SIM 卡没有默认的 LTE 附加上下文配置，则设备应为 LTE 附加上下文的 APN 返回空字符串，以便在保持上下文启用的情况下进行所有漫游条件。 如果上下文处于禁用状态，则设备不会附加到 LTE，因为没有适用于 LTE 附加的可用配置。 当用户调换回先前在设备上配置的 SIM 卡时，调制解调器应为 SIM 卡还原其出厂默认的 LTE 附加配置。 不应在每个 SIM 交换间持久保存运行时配置。 在任何时候，在调制解调器中，每个漫游条件下只能有一个默认的 LTE 附加 APN (home/partner/非合作伙伴) 。  

发出 Set 命令后，操作系统将始终设置所有三个默认 LTE 附加上下文，每个漫游条件对应一个。 如果操作系统提供的列表不是正好三个，则应拒绝 Set 命令。 如果某个提供的默认 LTE 附加上下文是由操作系统中的漫游条件与当前注册状态匹配的，则调制解调器应与网络分离，并使用新指定的 LTE 附加上下文重新执行 LTE 附加。 否则，在下次漫游条件匹配时，设备应使用指定的默认 LTE 附加上下文。  如果设备指定的默认 LTE 附加上下文无法在 LTE 网络上注册，则设备应视情况退回到 3G/2G。 如果调制解调器无法区分伙伴网络和非合作伙伴网络，则调制解调器应为所有漫游方案使用非合作伙伴默认 LTE 附加上下文。 如果 OS 将默认 LTE 附加上下文配置为 IP type = default，则调制解调器应为 LTE 附加上下文分配最适当的 IP 类型。  但是，操作系统期望调制解调器仍返回合作伙伴漫游条件和正确反映配置的 LTE 附加上下文的 IP 类型。

Ihv 和 Oem 可以将 LTE 附加上下文预配置为调制解调器中的默认配置，但这些上下文必须标记为 MBIM_MS_CONTEXT_SOURCE = MbimMsContextSourceModemProvisioned。  

根据3GPP 标准，可将默认的 LTE 附加上下文拆分为两个类别： "UE 启动" 和 "网络启动"。 如果使用空的空访问字符串对设备进行配置，则设备将不会向网络提供任何 LTE 附加上下文，并等待网络将其分配给设备。 正如 MBIM 1.0 规定的，如果将 LTE 附加上下文的 IP 类型配置为默认值，则调制解调器应根据其内部算法选择最佳 IP 类型。

下图说明了 LTE 附加配置的示例流。

![LTE 附加配置示例流](images/LTE_attach_1.png "LTE 附加配置示例流")

#### <a name="query"></a>查询

从已完成的查询返回 MBIM_MS_LTE_ATTACH_CONFIG_INFO，并在 InformationBuffer 中设置消息。 对于 Query，InformationBuffer 为 NULL。

#### <a name="set"></a>设置

对于 Set，InformationBuffer 包含 MBIM_MS_SET_LTE_ATTACH_CONFIG。

#### <a name="unsolicited-events"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_MS_LTE_ATTACH_CONFIG_INFO 结构。 在某些情况下，默认的 LTE 附加上下文由网络通过无线 (OTA) 或短消息服务更新， (SMS) 不会从操作系统中执行 MBIM_CID_MS_LTE_ATTACH_CONFIG 命令。 函数必须相应地更新默认的 LTE 附加上下文和标记 MBIM_MS_CONTEXT_SOURCE = MbimMsContextSourceOperatorProvisioned。 之后，函数必须通知宿主有关将此事件与更新的列表一起使用的更新。

### <a name="parameters"></a>参数

| Operation | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_MS_LTE_ATTACH_CONFIG | 不适用 | 不适用 |
| 响应 | MBIM_MS_LTE_ATTACH_CONFIG_INFO | MBIM_MS_LTE_ATTACH_CONFIG_INFO | MBIM_MS_LTE_ATTACH_CONFIG_INFO |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询 

InformationBuffer 应为 NULL，而 InformationBufferLength 应为零。

#### <a name="set"></a>设置

以下 MBIM_MS_SET_LTE_ATTACH_CONFIG 结构应在 InformationBuffer 中使用。 仅当列表中包含三个元素计数时，Set 命令才有效，其中每个漫游条件 (home/partner/非合作伙伴) 。

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Operation | MBIM_MS_LTE_CONTEXT_OPERATIONS | 指定使用 Set 命令的操作的类型。 如果设置为 MbimMsLteAttachContextOperationRestoreFactory，则应忽略所有其他字段。 应删除 OS 创建的或修改的默认 LTE 附加上下文，并且应加载默认的工厂预配置默认 LTE 附加上下文。 如果调制解调器没有默认配置，则所有漫游条件默认 LTE 附加上下文都应设置为空的 APN 字符串，IP 类型为默认值。 |
| 4 | 4 | Elementcount 多于 (EC)  | UINT32 | DataBuffer 中后面的 MBIM_MS_LTE_ATTACH_CONTEXT 结构的计数。 此组件当前指定为三个，每个漫游条件 (home/partner/非合作伙伴) 。 |
| 8 | 8 * EC | MsLteAttachContextRefList | OL_PAIR_LIST | 该对的第一个元素为4字节的偏移量，该偏移量是从该 MBIM_MS_LTE_ATTACH_CONFIG_INFO 结构的开头 (偏移量 0) 计算到 MBIM_MS_LTE_ATTACH_CONTEXT 结构的 (MBIM_MS_LTE_ATTACH_CONTEXT 有关详细信息，请参阅) 表。 对的第二个元素是指向相应 MBIM_MS_LTE_ATTACH_CONTEXT 结构的指针的大小为4字节。 |
| 8 + (8 * EC)  |  | DataBuffer | DATABUFFER | MBIM_MS_LTE_ATTACH_CONTEXT 结构的数组。 |

前面的表中使用了以下结构。

MBIM_MS_LTE_ATTACH_CONTEXT_OPERATIONS 描述可在 Set 命令中使用的操作的类型。

| 类型 | 值 | 描述 |
| --- | --- | --- |
| MbimMsLteAttachContextOperationDefault | 0 | 用于在调制解调器中覆盖现有默认 LTE 附加上下文的默认操作。 操作系统将始终将所有三个默认 LTE 附加上下文替换为漫游条件。 |
| MbimMsLteAttachContextOperationRestoreFactory | 1 | 为当前插入的 SIM 的提供程序 ID 还原工厂预配置默认 LTE 附加上下文。 应删除并替换 OS 替换或创建的所有默认 LTE 附加上下文。 如果当前插入的包含一个或多个漫游条件的 SIM 提供程序 ID 没有默认预配置的默认 LTE 附加上下文，则默认的 LTE 附加应返回空的 APN 字符串，IP 类型 = 默认值。 |

MBIM_MS_LTE_ATTACH_CONTEXT 指定用于 LTE 附加配置的上下文。

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | IPType | MBIM_CONTEXT_IP_TYPE | 有关详细信息，请参阅 MBIM_CONTEXT_IP_TYPE 表。 |
| 4 | 4 | 漫游 | MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL | 指示哪种漫游条件适用于此默认 LTE 附加上下文。 有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL 表。 |
| 8 | 4 | 源 | MBIM_MS_CONTEXT_SOURCE | 指定上下文的创建源。 有关详细信息，请参阅 MBIM_MS_CONTEXT_SOURCE 表。 |
| 12 | 4 | AccessStringOffset | OFFSET | 数据缓冲区中的偏移量到字符串 AccessString （用于访问网络）。 对于基于 GSM 的网络，此名称应为接入点名称 (APN) string，如 "data.thephone-company.com"。 字符串的大小不应超过100个字符。 如果 AccessString 为空，则设备要求网络将访问字符串分配回设备。 在这种情况下，仍必须指定 IP 类型。 |
| 16 | 4 | AccessStringSize | 大小 (0.. 200)  | 用于 AccessString 的大小。 如果设备希望网络将访问字符串分配回设备进行 LTE 连接，此值应为0。 |
| 20 | 4 | UserNameOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），表示要进行身份验证的用户名。 此成员可以为 NULL。 |
| 24 | 4 | UserNameSize | 大小 (0.. 510)  | 用于用户名的大小。 |
| 28 | 4 | PasswordOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），表示该用户名的密码。 此成员可以为 NULL。 |
| 32 | 4 | PasswordSize | 大小 (0.. 510)  | 用于密码的大小。 |
| 36 | 4 | 压缩 | MBIM_COMPRESSION | 指定要用于标头和数据的数据连接的压缩。 此成员仅适用于基于 GSM 的设备。 主机将此成员设置为基于 CDMA 的设备的 MBIMCompressionNone。 有关详细信息，请参阅 MBIM_COMPRESSION 表。 |
| 40 | 4 | AuthProtocol | MBIM_AUTH_PROTOCOL | 用于 PDP 激活的身份验证类型。 有关详细信息，请参阅 MBIM_AUTH_PROTOCOL 表。 |
| 44 |  | DataBuffer | DATABUFFER | 包含 AccessString、用户名和密码的数据缓冲区。 |

MBIM_MS_LTE_ATTACH_CONTEXT_ROAMING_CONTROL 指示哪种漫游条件适用于此默认 LTE 附加上下文。

| 类型 | 值 | 描述 |
| --- | --- | --- |
| MbimMsLteAttachContextRoamingControlHome | 0 | 指示是否允许在家庭网络上使用默认 LTE 附加上下文。 |
| MbimMsLteAttachContextRoamingControlPartner | 1 | 指示是否允许在伙伴漫游网络上使用上下文。 |
| MbimMsLteAttachContextRoamingControlNonPartner | 2 | 指示是否允许在非合作伙伴漫游网络上使用上下文。 |

MBIM_MS_CONTEXT_SOURCE 指定上下文的创建源。

| 类型 | 值 | 描述 |
| --- | --- | --- |
| MbimMsContextSourceAdmin | 0 | 上下文是由操作系统的企业 IT 管理员创建的。 |
| MbimMsContextSourceUser | 1 | 上下文是用户通过 OS 设置创建的。 |
| MbimMsContextSourceOperator | 2 | 该上下文是由运算符通过 OMA DM 或其他通道创建的。 | 
| MbimMsContextSourceModem | 3 | 上下文是由 IHV 或 OEM 创建的。 |
| MbimMsContextSourceDevice | 4 | 上下文是由 OS APN 数据库创建的。 |

#### <a name="response"></a>响应

以下 MBIM_MS_LTE_ATTACH_CONFIG_INFO 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 (EC)  | UINT32 | DataBuffer 中后面的 MBIM_MS_LTE_ATTACH_CONTEXT 结构的计数。 此组件当前指定为三个，每个漫游条件 (home/partner/非合作伙伴) 。 |
| 4 | 8 * EC | MsLteAttachContextRefList | OL_PAIR_LIST | 该对的第一个元素为4字节的偏移量，该偏移量是从该 MBIM_MS_LTE_ATTACH_CONFIG_INFO 结构的开头 (偏移量 0) 计算到 MBIM_MS_LTE_ATTACH_CONTEXT 结构的 (MBIM_MS_LTE_ATTACH_CONTEXT 有关详细信息，请参阅) 表。 对的第二个元素是指向相应 MBIM_MS_LTE_ATTACH_CONTEXT 结构的指针的大小为4字节。 |
| 4 + (8 * EC)  |  | DataBuffer | DATABUFFER | MBIM_MS_LTE_ATTACH_CONTEXT 结构的数组。 |

#### <a name="notification"></a>通知

有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_CONFIG_INFO 表。

### <a name="status-codes"></a>状态代码

对于查询和设置操作：

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | 操作失败，因为设备无法检索预配的上下文。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持此操作。 |

仅适用于集操作： 

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效，操作失败。 |
| MBIM_STATUS_WRITE_FAILURE  | 操作失败，因为更新请求不成功。 |

## <a name="mbim_cid_ms_lte_attach_status"></a>MBIM_CID_MS_LTE_ATTACH_STATUS

### <a name="description"></a>描述

根据3GPP 的要求，虽然设备可以指定在没有任何启用的 PDP 上下文的情况下连接到网络时要使用的默认 LTE 附加上下文，但在某些情况下，设备将在与设备上配置的默认 LTE 附加上下文不同的 PDP 上下文上进行连接。 下面列出了所有可能的方案：

1.  UE 指定特定的 LTE 附加接入点。
2.  UE 指定特定的 LTE 附加接入点，但网络决定让设备在漫游时改为在另一个 APN 上附加。
3.  UE 不指定 LTE 附加 APN，并允许网络将其分配给设备。
4.  从 2G/3G 网络注册到 LTE 并且已经有至少一个活动的 PDP 上下文的 UE。 网络使用该网络作为 LTE 附加 APN。

当设备默认 LTE 附加时，它应将 MBIM_CID_MS_LTE_ATTACH_STATUS 的通知发送到 OS，以提供最新的 LTE 附件的 PDP 上下文的详细信息。 如果满足以下任一方案，则会发生默认的 LTE 附加：

1.  设备最初会附加到 LTE 网络。
2.  设备无需任何先前启用的 PDP 上下文即可从 2G/3G 到 LTE。

从 MBIM_CID_LTE_ATTACH_STATUS 返回的 LTE 附加上下文可能是以下项之一：

1.  存储在调制解调器中的默认 LTE 附加上下文。
2.  从网络分配回来的默认 LTE 附加上下文。

在运行时，操作系统还应该能够查询上次使用的附加信息对于默认的 LTE 附加的信息。 该调制解调器应返回上一个已知的默认 LTE 附加上下文。  如果将设备从 LTE 移交到 2G/3G 网络，则调制解调器应返回用于上一条 LTE 连接的上下文。 每次设备从网络注销时，接入点都应为空。

下图显示了用于 LTE 附加状态的示例消息流。

![LTE 附加状态示例流](images/LTE_attach_2.png "LTE 附加状态示例流")

#### <a name="query"></a>查询

InformationBuffer 中的查询完成消息返回 MBIM_MS_LTE_ATTACH_STATUS。 对于 Query，InformationBuffer 为 NULL。

#### <a name="set"></a>设置 

不支持设置操作。

#### <a name="unsolicited-events"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_MS_LTE_ATTACH_STATUS 结构。

### <a name="parameters"></a>参数

| Operation | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | 不适用 | 不适用 |
| 响应 | 不适用 | MBIM_MS_LTE_ATTACH_STATUS | MBIM_MS_LTE_ATTACH_STATUS |

### <a name="data-structures"></a>数据结构

#### <a name="query"></a>查询

InformationBuffer 应为 NULL，而 InformationBufferLength 应为零。

#### <a name="set"></a>设置

不支持设置操作。

#### <a name="response"></a>响应

以下 MBIM_MS_LTE_ATTACH_STATUS 结构应在 InformationBuffer 中使用。


| Offset | 大小 |       字段        |           类型           |                                                                                                                                                                                                                                                                                                    描述                                                                                                                                                                                                                                                                                                     |
|--------|------|--------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   0    |  4   |   LteAttachState   | MBIM_MS_LTE_ATTACH_STATE |                                                                                                                                                                                                                                    指示设备当前是否已连接到 LTE 网络。  有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_STATE 表。                                                                                                                                                                                                                                     |
|   4    |  4   |       IPType       |  MBIM_CONTEXT_IP_TYPES   |                                                                                                                                                                                                                                                                             有关详细信息，请参阅 MBIM_CONTEXT_IP_TYPE 表。                                                                                                                                                                                                                                                                              |
|   8    |  4   | AccessStringOffset |          OFFSET          | 数据缓冲区中的偏移量到字符串 AccessString （用于访问网络）。 对于基于 GSM 的网络，此名称应为接入点名称 (APN) string，如 "data.thephone-company.com"。 对于基于 CDMA 的网络，这可能是一种特殊的拨号代码，如 "#777" 或 (NAI) 的网络访问标识符，如 " foo@thephone-company.com "。 此成员可为空，请求网络分配默认 APN。 注意：并非所有网络都支持此 NULL APN 约定。 因此，无效的 APN 导致的连接失败是可能的结果。 字符串的大小不应超过100个字符。 |
|   12   |  4   |  AccessStringSize  |       大小 (0.. 200)        |                                                                                                                                                                                                                                                                                        用于 AccessString 的大小（字节）。                                                                                                                                                                                                                                                                                        |
|   16   |  4   |   UserNameOffset   |          OFFSET          |                                                                                                                                                                                                                          从该结构的开头算起的偏移量（以字节为单位），表示要进行身份验证的用户名。 此成员可以为 NULL。                                                                                                                                                                                                                           |
|   20   |  4   |    UserNameSize    |       大小 (0.. 510)        |                                                                                                                                                                                                                                                                                          用于用户名的大小（字节）。                                                                                                                                                                                                                                                                                          |
|   24   |  4   |   PasswordOffset   |          OFFSET          |                                                                                                                                                                                                                             从该结构的开头算起的偏移量（以字节为单位），表示该用户名的密码。 此成员可以为 NULL。                                                                                                                                                                                                                             |
|   28   |  4   |    PasswordSize    |       大小 (0.. 510)        |                                                                                                                                                                                                                                                                                          用于密码的大小（字节）。                                                                                                                                                                                                                                                                                          |
|   32   |  4   |    压缩     |     MBIM_COMPRESSION     |                                                                                                                                                                           指定要用于标头和数据的数据连接的压缩。 此成员仅适用于基于 GSM 的设备。 主机将此成员设置为基于 CDMA 的设备的 MBIMCompressionNone。 有关详细信息，请参阅 MBIM_COMPRESSION 表。                                                                                                                                                                           |
|   36   |  4   |    AuthProtocol    |    MBIM_AUTH_PROTOCOL    |                                                                                                                                                                                                                                                     用于 PDP 激活的身份验证类型。 有关详细信息，请参阅 MBIM_AUTH_PROTOCOL 表。                                                                                                                                                                                                                                                     |
|   40   |  4   |                    |        DataBuffer        |                                                                                                                                                                                                                                                                                                     DATABUFFER                                                                                                                                                                                                                                                                                                     |

前面的表中使用了以下数据结构。

MBIM_MS_LTE_ATTACH_STATE 指示设备当前是否已连接到 LTE 网络。

| 类型 | 值 | 描述 |
| --- | --- | --- |
| MbimMsLteAttachStateDetached | 0 | 指示设备未连接到 LTE 网络。 |
| MbimMsLteAttachStateAttached | 1 | 指示设备已连接到 LTE 网络。 |

#### <a name="notification"></a>通知

有关详细信息，请参阅 MBIM_MS_LTE_ATTACH_STATUS 表。

### <a name="status-codes"></a>状态代码

对于查询和设置操作：

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_READ_FAILURE | 操作失败，因为设备无法检索预配的上下文。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持此操作。 |

## <a name="hardware-lab-kit-hlk-tests"></a>硬件实验室工具包 (HLK) 测试

请参阅 [安装 HLK 的步骤](https://microsoft.sharepoint.com/teams/HWKits/SitePages/HWLabKit/Manual%20Controller%20Installation.aspx)。
 
在 HLK Studio 中，连接到设备蜂窝电话调制解调器驱动程序并运行测试： [Win6_4. MB。GSM.TestLteAttach](https://docs.microsoft.com/windows-hardware/test/hlk/testref/aaa1f042-8535-4d09-b19e-082bef24f518)。

或者，运行 **TestLteAttach** HLK testlist by [**netsh-mbn**](/windows-server/networking/technologies/netsh/netsh-mbn) 和 [**netsh-mbn**](mb-netsh-mbn-test.md)--安装。

```
netsh mbn test feature=lte testpath="C:\\data\\test\\bin" taefpath="C:\\data\\test\\bin"
```

显示 HLK 测试结果的此文件应已在运行 "netsh mbn test" 命令的目录中生成： `TestLteAttach.htm` 。

## <a name="manual-tests"></a>手动测试
- 要求：一个带有正确接入点设置的 sim，另一个是手动使用的接入点信息。

1. 打开设置->网络 & Internet-> 手机网络
1. 单击 "***高级选项***"

使用手机网络设置：

3. 至少应有一个接入点，它是来自 sim 信息的设置。 可以通过单击 APN 并单击 "查看" 按钮来获取 APN 的详细信息。

使用手动设置：

3. 按照 [手机网络设置](https://support.microsoft.com/windows/cellular-settings-in-windows-10-905568ff-7f31-3013-efc7-3f396ac92cd7) 中的 "添加 apn" 部分手动设置 APN。
4. 附加 APN 并检查附加状态。

## <a name="mb-lte-attach-troubleshooting-guide"></a>MB LTE 附加故障排除指南
1. 获取%ProgramData%\Microsoft\WwanSvc\DMProfiles 下的所有附加接入点配置文件
1. 了解将基于创建类型优先级应用哪个特定的配置文件
1. 调查日志以检查为什么错误地配置了 LTE 附加 APN
1. 使用[收集日志](mb-collecting-logs.md)中的说明收集和解码日志
1. 打开在[TextAnalysisTool](mb-analyzing-logs.md)中生成的 .txt 文件。
1. 加载 [LTE 附加筛选器](mb-lte-attach-tat.md)
## <a name="sample-log-of-lte-attach"></a>LTE 附加的示例日志
```
10409 [0]0370.0434::2020-03-06 01:16:13.118424000 [WwanDimCommon] ReadyState  : WwanReadyStateInitialized (0x1)
14137 [0]0370.0684::2020-03-06 01:16:13.146883200 [WwanProfileManager]INFO: SaveModemConfiguredLteAttachConfig: added modem configured LTE attach profile
14362 [0]0370.0684::2020-03-06 01:16:13.149255900 [WwanProfileManager]INFO: SaveModemConfiguredLteAttachConfig: added modem configured LTE attach profile
14476 [1]0370.0434::2020-03-06 01:16:13.149677900 [WwanDimCommon] ReadyState  : WwanReadyStateInitialized (0x1)
14503 [0]0370.0684::2020-03-06 01:16:13.151412000 [WwanProfileManager]INFO: SaveModemConfiguredLteAttachConfig: added modem configured LTE attach profile
14962 [0]0370.0684::2020-03-06 01:16:13.156860700 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanDataExecutor::OnLteAttachProfileUpdate: WwanPmGetLteAttachProfileInEffect() didn't find anything, using Network Assigned. 
14963 [0]0370.0684::2020-03-06 01:16:13.156862600 [Microsoft-Windows-WWAN-SVC-EVENTS]WWAN Service event: [Info] CWwanDataExecutor::OnLteAttachProfileUpdate: LTEAttachConfig has same config as modem has, skip 
```