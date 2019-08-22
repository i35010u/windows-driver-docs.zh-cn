---
title: MB 5G 数据类支持
description: MB 5G 数据类支持
ms.assetid: 16531A63-76EC-4722-8817-FA8DB3B2B82F
keywords:
- MB 5G 数据类支持, Mobile 宽带5G 数据类支持
ms.date: 04/17/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b22b2b62bb837e690ddd8105dd4fe1a3dfb3e80f
ms.sourcegitcommit: 340fffb04a0a36fe951e78cbfdfb814cf58383aa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "67866145"
---
# <a name="mb-5g-data-class-support"></a>MB 5G 数据类支持

## <a name="terminology"></a>术语

本主题使用以下术语:

| 术语 | 定义 |
| --- | --- |
| NR | 新增收音机。 NR 是引用5G 时在3GPP 中使用的术语。 |
| MBB | 移动宽带。 |
| EPC | 增强的数据包核心。 引用 LTE core 网络时在3GPP 中使用的术语。 |
| NGC | 下一代核心。 引用5G 核心网络时在3GPP 中使用的术语。 NR 等效于 EPC。 |
| DC | 双重连接。 网络可以支持 LTE 和 5G NR, 包括与设备同时连接到 LTE 和 NR 的双重连接。 |
| SA | 独立5G。 引用任何基于 NGC 的 NR 网络。 |
| NSA | 非独立5G。 引用任何基于 EPC 的 NR 网络。 |
| gNB | 支持 NR 无线接口以及与 NGC 的连接的 NR 收音机基站。 |
| RAT | 无线电访问技术。 |

## <a name="overview"></a>概述

Windows 10 1903 版是 Windows 的第一个版本, 它支持由 IHV 合作伙伴开发的 5G mobile 宽带驱动程序开发的预览版本。 Name *5G*是[3GPP 版本15规范](https://www.3gpp.org/release-15)中引入的新收音机 (NR) 的友好名称。 NR 是一套全面的标准, 旨在提供到现有的第四代 LTE 技术的真正长期发展, 可能涵盖从窄带到超高宽带的所有手机通信需求, 以及标称到关键任务延迟要求。 作为一项技术, 5G 预计会在十年时间内发展。 

本主题介绍 Windows 10 版本1903中首次发布的 MBIM 扩展, 这使硬件合作伙伴能够开发 MBB 驱动程序, 该驱动程序具有针对 5G "非独立" 基于 EPC 的 NR 网络的数据类支持。 5G 吞吐量和产品/服务的数据平面支持和支持不属于此 Windows 版本, 本主题未对此进行介绍。 

## <a name="windows-5g-mbim-interface-extension"></a>Windows 5G MBIM interface extension

### <a name="mbim-interface"></a>MBIM 接口

从 Windows 10 版本 1903, 整个中的5G 仍在开发中。 从网络部署的角度来看, 5G 应分两个阶段进行部署: 

* 在阶段1中, 大多数移动网络操作员都应该部署 5G, 并将5G 广播添加到现有的 LTE 广播和 EPC 核心部署 (通常称为 "nonstandalone 5G" 网络)。  

* 在阶段2中, 移动网络操作员应并行替换 Epc 和 NGCs, 并 densify 5G 无线电部署, 以启用真正的 "独立" 或基于 NR 的5G 网络。 阶段2接口扩展不在本主题或 Windows 版本的范围内。 

Windows 10 版本1903中引入了支持基本阶段1网络要求或 "nonstandalone" EPC based5G 网络的接口扩展。 为了能够实现与旧的调制解调器的可扩展且完全向后兼容, 引入了新的 Microsoft MBIM 扩展版本 (2.0)。 

新的 Microsoft MBIM extesnion 版本是必需的, 因为[MBIM 1.0 勘误表规范](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)包含用于添加和播发可选 cid 的机制, 但它缺少用于更改现有 cid (新负载或已修改有效负载) 或引入可选 Cid 无法容纳的任何方面的更改。 每个有效负载可能由固定大小的成员或动态大小 (偏移/大小对) 成员组成。 如果存在一个或多个动态大小的成员, 则最后一个成员的大小为 variable。  

此规范还为主机添加了一个额外的 CID, 以将其 MBIM 发行版和扩展发行版播发到 MBIM 设备。 对于字段中已存在的旧驱动程序, 此 CID 是可选的, 因此完全维护向后兼容性。  有关更多详细信息, 请参阅[MBIM Extension Release 2.0](#mbim-extensions-release-20---5g-nonstandalone-epc-based-option-3-network-support)网络支持。 

### <a name="ndis-interface"></a>NDIS 接口

NDIS 支持 NDIS_HEADER 中的修订号。 这允许向 OID 消息添加新成员, NDIS 在[OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)中使用可选的服务 cap 表。

以下 NDIS Oid 及其数据结构已针对5G 数据类支持进行了更新。

- [OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)
- [OID_WWAN_REGISTER_STATE](oid-wwan-register-state.md)
- [OID_WWAN_PACKET_SERVICE](oid-wwan-packet-service.md)
- [OID_WWAN_SIGNAL_STATE](oid-wwan-signal-state.md)

本主题的以下部分介绍了这些 Oid 的等效 MBIM CID 消息。

## <a name="mbim-extensions-release-20---5g-nonstandalone-epc-based-option-3-network-support"></a>MBIM 扩展版本 2.0-5G nonstandalone (基于 EPC 的选项 3) 网络支持

由于[MBIM 1.0 勘误表规范](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)缺少使用新的或已修改的有效负载更改现有 cid 的机制, 因此, Windows 10 版本1903引入了 MBIM 1.0 扩展2.0 来扩展接口以支持5G。

### <a name="versioning-scheme"></a>版本控制方案

> [!NOTE]
> 在本部分中, 术语 " *MBIMEx 版本*" 是指 MBIM 扩展发布号。

该主机通过两种方式学习设备的 MBIMEx 版本:

1. MBIM 扩展功能说明符。
2. 可选的 MBM_CID_VERSION 消息 (如果设备支持) 并声明对它的支持。

如果这两个版本不同, 则更高版本会在设备保持为主机的持续时间内提供 MBIMEx 版本。 较高的 MBIMEx 版本称为设备的已*发布 MBIMEx 版本*。 设备的已发布 MBIMEx 版本可以低于其本机 MBIMEx 版本, 该版本是设备支持的最高 MBIMEx 版本。 设备只能通过 MBIM_CID_VERSION 消息显式了解主机的 MBIMEx 版本。

在任何版本中, 主机总是在设备初始化序列的开头使用 MBIM_CID_DEVICE_SERVICES 在设备上查询支持的服务和 Cid。 如果设备支持 MBIM_CID_VERSION 并在 MBIM_CID_DEVICE_SERVICE 查询响应中公布其支持, 则不了解 MBIM_CID_VERSION 或 MBIMEx 版本低于2.0 的主机将忽略它。 同时, 主机会了解 MBIM_CID_VERSION, 并具有2.0 或更高版本的本机 MBIMEx 版本, 使用主机的本机 MBIMEx 版本将 MBIM_CID_VERSION 消息发送到设备, 并且 CID 是接收到设备后发送到设备的第一个 CID_CID_DEVICE_SERVICES 响应。

如果设备在响应 MBIM_CID_DEVICE_SERVICES 查询后接收到来自主机的 MBIM_CID_VERSION 作为首次接收的 CID, 则设备将知道主机的 MBIMEx 版本。 如果设备在响应 MBIM_CID_DEVICE_SERVICES 查询后收到主机中的任何其他 CID 作为首次接收的 CID, 则设备假定主机的本机 MBIMEx 版本为1.0。

功能更高的 MBIMEx 版本是所有较低 MBIMEx 版本的超集。 主机支持在主机的本机 MBIMEx 版本下或之下已公告 MBIMEx 版本的所有设备。 如果设备的已发布 MBIMEx 版本高于主机的本机 MBIMEx 版本, 则该主机不需要支持该设备, 并且在此情况下, 主机的确切行为是未定义的。

打算使用较旧主机的设备最初应播发 MBIMEx 版本 1.0, 或在 MBIM 扩展功能描述符中使用设备的最低主机 MBIMEx 版本。 如果主机发送 MBIM_CID_VERSION, 而主机的 MBIMEx 版本高于设备最初公布的版本, 则设备应在 MBIM_CID_VERSION 响应中指出较高的 MBIMEx 版本, 最高可达主机的本机 MBIMEx 版本和设备的本机 MBIMEx 版本。

> [!NOTE]
> 例如, 设备支持 MBIMEx 版本 2.0, 但适用于不支持 MBIMEx 2.0 的较早版本的操作系统。 设备最初会公布 MBIMEx 版本 1.0, 并公布对可选 MBIM_CID_VERSION 的支持。 当插入运行 Windows 10 版本1803的主机时, 主机不会理解 MBIM_CID_VERSION 并且不会将 MBIM_CID_VERSION 发送到设备。 对于主机, 设备的 MBIMEx 版本为1.0。 主机继续以初始化序列发送其他 Cid。 收到除 MBIM_CID_VERSION 以外的 Cid 时, 设备知道主机支持 MBIMEx 版本1.0。 双方继续符合 MBIMEx 版本1.0。 稍后, 在将同一设备插入运行 Windows 10 版本 1903 (版本, 版本, 版本为 2.0) 的主机时, 主机会将 MBIM_CID_VERSION 发送到设备, 通知其主机的本机 MBIMEx 版本为2.0。 设备会发回 MBIM_CID_VERSION, 以响应设备的已公布 MBIMEx 版本2.0。 从这里开始, 这两个端都继续符合 MBIMEx 版本2.0。

下表显示了一个兼容性矩阵, 其中包含三个假设主机和三个假设的设备, 每个都具有所述的本机 MBIMEx 版本。 设备在最初在 USB 描述符中公布 MBIMEx 版本1.0。 该矩阵显示每个设备在每个主机上的行为方式。

| 设备 (见下)/主机 (正确) | Windows 10 版本1809或更低版本 (native MBIMEx 版本 1.0) | Windows 10 版本1903及更高版本 (MBIMEx 版本 2.0) |
| --- | --- | --- |
| 4G 设备 <p>Native MBIMEx 版本1。0</p> | 设备最初公布 MBIMEx 1.0。 无 MBIM_CID_VERSION 交换。 兼容的设备和主机。 默认情况下, MBIMEx 版本1.0 运行。 | 设备最初公布 MBIMEx 1.0。 无 MBIM_CID_VERSION 交换。 主机使用 MBIMEx 1.0 与设备一起工作。 |
| 5G NSA 设备 <p>Native MBIMEx 版本2。0</p> | 设备最初公布 MBIMEx 1.0。 无 MBIM_CID_VERSION 交换。 设备知道主机已 MBIMEx 1.0, 并继续 MBIMEx 1.0。 | 设备最初公布 MBIMEx 1.0。 主机发送 MBIM_CID_VERSION 以通知设备主机支持 MBIMEx 2.0。 设备响应 MBIMEx 2.0。 两端均继续 MBIMEx 2.0。 |

下表列出了在 MBIMEx 版本2.0 中修改的所有现有 Cid 及其修改后的负载。 这些 Cid 中的所有 unmentioned 有效负载和表中未提及的所有其他 Cid 将从 MBIMEx 版本1.0 中继续运行, 并且保持不变。 

| CID | 有效负载 |
| --- | --- |
| MBIM_CID_REGISTER_STATE | MBIM_REGISTRATION_STATE_INFO_V2 |
| MBIM_CID_PACKET_SERVICE | MBIM_PACKET_SERVICE_INFO_V2 |
| MBIM_CID_SIGNAL_STATE | MBIM_SIGNAL_STATE_INFO_V2 |

## <a name="mbim-service"></a>MBIM 服务

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft 基本 IP 连接扩展插件 | UUID_BASIC_CONNECT_EXTENSIONS | 3D01DCC5-FEF5-4D05-9D3A-BEF7058E9AAF |

## <a name="mbim_cid_version"></a>MBIM_CID_VERSION

对于支持 MBIM Microsoft extension 2.0 或更高版本的 MBB 驱动程序, MBIM_CID_VERSION 是在主机和设备之间交换 MBIM 版本信息的强制性命令。 对于包含不能识别此 CID 的驱动程序的市场内设备, 主机将假定并提供向后兼容性。

主机以查询形式发送此命令 (如果设备支持)。 查询包含主机当前支持的 MBIM 发布号和 MBIM 扩展发布号。

在设备端, 设备根据[版本控制方案](#versioning-scheme)中定义的规则调整其公布的 MBIM 版本号和 MBIM 扩展发行版号, 然后在对主机的响应中发送它们。

此命令在 "**基本连接扩展**" 服务下定义。

| CID | 命令代码 | UUID |
| --- | --- | --- |
| MBIM_CID_VERSION | 15 | 3d01dcc5-fef5-4d05-0d3abef7058e9aaf |

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | MBIM_VERSION_INFO | 不适用 |
| 响应 | 不适用 | MBIM_VERSION_INFO | 不适用 |

### <a name="query"></a>查询

通知设备主机的本机 MBIM 发行版号和 MBIM 扩展发布号。 InformationBuffer 包含以下 MBIM_VERSION_INFO 结构。

| 偏移量 | Size | 字段 | type | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 2 | bcdMBIMVersion | UINT16 | BCD 中发送方的 MBIM 发布号, 在位7和8之间具有隐含的小数点。 例如， `0x0100 == 1.00 == 1.0` 。 这是一个小 endian 常量, 因此字节数为 0x00, then 为0x01。 |
| 2 | 2 | bcdMBIMExtendedVersion | UINT16 | BCD 中发送方的 MBIM 扩展发布号, 在位7和8之间具有隐含的小数点。 例如， `0x0100 == 1.00 == 1.0` 。 这是一个小 endian 常量, 因此字节数为 0x00, then 为0x01。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 中的 InformationBuffer 包含 MBIM_VERSION_INFO 结构。

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

此 CID 仅使用[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的9.4.5 部分中定义的通用状态代码。

## <a name="mbim_cid_ms_device_caps_v2"></a>MBIM_CID_MS_DEVICE_CAPS_V2

此 CID 与在[MB 多 SIM 操作](mb-multi-sim-operations.md#mbim-interface-update-for-multi-sim-operations)上定义的相同, 后者本身就是 MBIM_CID_MS_DEVICE_CAPS 的扩展, 如[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)部分10.5.1 中所定义。 对于 MBIM 扩展版本 2.0, 在 MBIM_DATA_CLASS 表中定义了新的数据类, 使设备能够报告其5G 功能。 MBIMDataClass5G_NSA 表示设备支持[3GPP TS 37.340](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3198)中定义的5G 非独立 (NSA), MBIMDataClass5G_SA 表示设备支持5G 独立 (SA), 也在 3GPP TS 37.340 中定义。

如果设备同时支持两个新数据类, 则应设置这两个位。

## <a name="mbim_data_class"></a>MBIM_DATA_CLASS

| 类型 | 掩码 |
| --- | --- |
| MBIMDataClassNone | 0h |
| MBIMDataClassGPRS | 1小时 |
| MBIMDataClassEDGE | 下半年 |
| MBIMDataClassUMTS | 4h |
| MBIMDataClassHSDPA | 8h |
| MBIMDataClassHSUPA | 10h |
| MBIMDataClassLTE | 20h |
| **MBIMDataClass5G_NSA** | **40h** |
| **MBIMDataClass5G_SA** | **80h** |
| 保留 | 100h-8000h |
| MBIMDataClass1XRTT | 10000h |
| MBIMDataClass1XEVDO | 20000h |
| MBIMDataClass1XEVDORevA | 40000h |
| MBIMDataClass1XEVDV | 80000h |
| MBIMDataClass3XRTT | 100000h |
| MBIMDataClass1XEVDORevB | 200000h |
| MBIMDataClassUMB | 400000h |
| 保留 | 800000-40000000h |
| MBIMDataClassCustom | 80000000h |

## <a name="mbim_cid_register_state"></a>MBIM_CID_REGISTER_STATE

此命令是已在[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中定义的 MBIM_CID_REGISTER_STATE CID 的扩展。 此扩展插件为响应结构添加一个名为**PreferredDataClasses**的新成员。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_REGISTRATION_STATE | 空 | 不适用 |
| 响应 | MBIM_REGISTRATION_STATE_INFO_V2 | MBIM_REGISTRATION_STATE_INFO_V2 | MBIM_REGISTRATION_STATE_INFO_V2 |

### <a name="query"></a>查询

InformationBuffer 为 null, 而 InformationBufferLength 为零。

### <a name="set"></a>设置

设置注册状态。 该信息与[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中所述的信息相同。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 中的 InformationBuffer 包含以下 MBIM_REGISTRATION_STATE_INFO_V2 结构。 与[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的节10.5.10.6 中定义的 MBIM_REGISTRATION_STATE_INFO 结构相比, 以下结构包含新的**PreferredDataClasses**字段。 除非在此注明, 否则[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的表10-55 中的字段说明适用于此结构。

#### <a name="mbim_registration_state_info_v2"></a>MBIM_REGISTRATION_STATE_INFO_V2

| 偏移量 | Size | 字段 | type | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NwError | UINT32 | 网络特定的错误。 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中的表10-44 记录了 NwError 的原因代码。 |
| 4 | 4 | RegisterState | MBIM_REGISTER_STATE | 请参阅[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中的表10-46。 |
| 8 | 4 | RegisterMode | MBIM_REGISTER_MODE | 请参阅[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中的表10-47。 |
| 12 | 4 | AvailableDataClass | UINT32 | [MBIM_DATA_CLASS](#mbim_data_class)中的值的位图, 表示注册的网络上受支持的数据类, 这些类用于注册设备的单元。 <p>如果**RegisterState**不是**MBIMRegisterStateHome**、 **MBIMRegisterStateRoaming**或**MBIMRegisterStatePartner**, 则此值设置为 MBIMDataClassNone。 </p> |
| 16 | 4 | CurrentCellularClass | MBIM_CELLULAR_CLASS | 指示当前用于多模式功能的手机网络类。 有关详细信息, 请参阅[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中的表10-8。 <p>对于单模式功能, 这与 MBIM_CID_DEVICE_CAPS 中报告的手机网络类相同。 对于多模式函数, 使用更新的**CurrentCellularClass**来指示从 CDMA 到 GSM 的转换, 反之亦然。 </p> |
| 20 | 4 | ProviderIdOffset | 抵销 | 从该结构的开头算起的偏移量 (以字节为单位), 它是一个名为**ProviderId**的数值 (0-9) 字符串, 表示网络提供程序标识。 <p>对于基于 GSM 的网络, 此字符串是三位数 Mobile 国家/地区代码 (MCC) 和两位数或三位数移动网络代码 (MNC) 的串联。 基于 GSM 的运营商可能有多个 MNC, 因此有多个**ProviderId**。</p><p>对于基于 CDMA 的网络, 此字符串是一个五位数的系统 ID (SID)。 通常, 基于 CDMA 的运营商有多个 SID。 通常, 一个运营商对于每个市场都有一个 SID, 通常按国家/地区 (如美国中的大都市统计区域 (MSA)) 划分。 如果此信息不可用, 则基于 CDMA 的设备必须指定 MBIM_CDMA_DEFAULT_PROVIDER_ID。</p><p>当处理查询请求并且注册状态处于自动注册模式时, 此成员包含设备当前关联的提供程序 ID (如果适用)。 当注册状态处于手动注册模式时, 此成员包含向其请求注册设备的提供程序 ID (即使提供程序不可用)。</p><p>当处理集请求并且注册状态处于手动模式时, 这将包含用于注册设备的主机所选的提供程序 ID。 如果注册状态为自动注册模式, 则忽略此参数。</p><p>如果提供程序 ID 不可用, 则必须将 CDMA 1xRTT 提供程序设置为 MBIM_CDMA_DEFAULT_PROVIDER_ID。</p> |
| 24 | 4 | ProviderIdSize | 大小 (0 到 12) | **ProviderId**的大小 (以字节为单位)。 |
| 28 | 4 | ProviderNameOffset | 抵销 | 从该结构的开头算起的偏移量 (以字节为单位), 该偏移量是一个名为**ProviderName**的字符串, 用于表示网络提供程序的名称。 此成员最多只能有 MBIM_PROVIDERNAME_LEN 个字符。 <p>对于基于 GSM 的网络, 如果首选的国家/地区缩写和移动网络名称 (PCCI & N) 的表示形式超过20个字符, 则设备应缩写网络名称。</p><p>当主机设置首选提供程序列表时, 将忽略此成员。 设备应为不具有此信息的设备指定一个空字符串。</p> |
| 32 | 4 | ProviderNameSize | 大小 (0-40) | **ProviderName**的大小 (以字节为单位)。 |
| 36 | 4 | RoamingTextOffset | 抵销 | 从该结构的开头算起的偏移量 (以字节为单位), 该偏移量是一个名为**RoamingText**的字符串, 用于通知用户设备正在漫游。 此成员最多只能为63个字符。 当注册状态为 "MBIMRegisterStatePartner" 或 "MBIMRegisterStateRoaming" 时, 此文本应为用户提供附加信息。 此成员是可选的。 |
| 40 | 4 | RoamingTextSize | 大小 (0 ... 126) | **RoamingText**的大小 (以字节为单位)。 |
| 44 | 4 | RegistrationFlag | MBIM_REGISTRATION_FLAGS | [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中每个表10-48 的标志集。 |
| 48 | 4 | PreferredDataClass | UINT32 | [MBIM_DATA_CLASS](#mbim_data_class)中表示设备上已启用数据类的值的位图。 设备只能使用已启用的数据类进行操作。 |
| 动态 | 4 | DataBuffer | DATABUFFER | 包含**ProviderId**、 **ProviderName**和**RoamingText**的数据缓冲区。 |

### <a name="unsolicited-events"></a>未经请求的事件

通知包含 MBIM_REGISTRATION_STATE_INFO_V2 结构。

### <a name="status-codes"></a>状态代码

此 CID 仅使用[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的9.4.5 部分中定义的通用状态代码。

## <a name="mbim_cid_packet_service"></a>MBIM_CID_PACKET_SERVICE

此命令是[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中定义的现有 MBIM_CID_PACKET_SERVICE 的扩展。

此扩展为响应结构添加了名为**FrequencyRange**的新成员, 并将**HighestAvailableDataClass**成员重命名为**CurrentDataClass** , 以明确其目的。

**CurrentDataClass**指示设备当前注册到的无线电访问技术 (RAT)。 它包含来自[MBIM_DATA_CLASS](#mbim_data_class)的单个值。

**FrequencyRange**指示设备当前正在使用的频率范围。 仅当**CurrentDataClass**字段指示设置了 MBIMDataClass5G_NSA 或 MBIMDataClass5G_SA 位时, 此设置才有效。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_PACKET_SERVICE | 空 | 不适用 |
| 响应 | MBIM_PACKET_SERVICE_INFO_V2 | MBIM_PACKET_SERVICE_INFO_V2 | MBIM_PACKET_SERVICE_INFO_V2 |

### <a name="query"></a>查询

InformationBuffer 为 null, 而 InformationBufferLength 为零。

### <a name="set"></a>设置

[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中介绍了 set 命令的信息。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 中的 InformationBuffer 包含 MBIM_PACKET_SERVICE_INFO_V2 结构。 与[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的节10.5.10.6 中定义的 MBIM_PACKET_SERVICE_INFO 结构相比, 此新结构包含**CurrentDataClass**和**FrequencyRange**字段。 除非在此处说明, 否则在[MBIM 规范修订版 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的表10-55 中的字段说明适用于此处。

#### <a name="mbim_packet_service_info_v2"></a>MBIM_PACKET_SERVICE_INFO_V2

| 偏移量 | Size | 字段 | type | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NwError | UINT32 | 网络特定的错误。 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中的表10-44 记录了 NwError 的原因代码。 |
| 4 | 4 | PacketServiceState | MBIM_PACKET_SERVICE_STATE | 请参阅[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中的表10-53。 | 
| 8 | 4 | CurrentDataClass | MBIM_DATA_CLASS | 当前单元中的当前数据类, 根据[MBIM_DATA_CLASS](#mbim_data_class)指定。 如果函数未处于附加的数据包服务状态, 则函数必须将此成员设置为 MBIMDataClassNone。 除了 HSPA (即 HSUPA 和 HSDPA) 和 5G DC 外, 函数会将此成员设置为单个 MBIM_DATA_CLASS 值。 对于 HSPA 数据服务, 函数指定 MBIMDataClass HSDPA 和 MBIMDataClassHSUPA 的按位 "或"。 对于支持 HSDPA 而不是 HSUPA 的单元格, 只指示 HSDPA (表示上行数据的 UMTS 数据类)。 每当当前数据类发生更改时, 函数都将发送通知, 指示**CurrentDataClass**的新值。 |
| 12 | 8 | UplinkSpeed | UINT64 | 包含上行比特率 (以每秒位数为单位)。 |
| 20 | 8 | DownlinkSpeed | UINT64 | 包含下行比特率 (以每秒位数为单位)。 |
| 38 | 4 | FrequencyRange | MBIM_FREQUENCY_RANGE | [MBIM_FREQUENCY_RANGE](#mbim_frequency_range)中的值的位掩码, 表示设备当前正在使用的频率范围。 仅当**CurrentDataClass**为 MBIMDataClass5G_NSA 或 MBIMDataClass5G_SA 时, 此方法才有效。 |

#### <a name="mbim_frequency_range"></a>MBIM_FREQUENCY_RANGE

下面的枚举用作前面 MBIM_PACKET_SERVICE_INFO_V2 结构中的值。

| type | ReplTest1 | 描述|
| --- | --- | --- |
| MBIMFrequencyRangeUnknown | 0 | 如果系统类型不是5G。 |
| MBIMFrequencyRange1 | 1 | [3GPP TS 38.101](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3283)中的 Frequency 范围 1 (FR1)-1 (6G)。 |
| MBIMFrequencyRange2 | 2 | [3GPP TS 38.101-2](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3284) (mmWave) 中的 FR2。 |
| MBIMFrequencyRange1AndRange2 | 3 | 如果 "FR1" 和 "FR2" 载波都已连接。 |

### <a name="unsolicited-events"></a>未经请求的事件

通知包含 MBIM_PACKET_SERVICE_INFO_V2 结构。

### <a name="status-codes"></a>状态代码

此 CID 仅使用[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的9.4.5 部分中定义的通用状态代码。

## <a name="mbim_cid_signal_state"></a>MBIM_CID_SIGNAL_STATE

此 CID 是 MBIM_CID_SIGNAL_STATE 的扩展, 为信号状态标准引入 RSRP 和 SNR。 仅当设备指示支持 MBIM 扩展版本2.0 时, 此新扩展插件才有效。 如果调制解调器支持 MBIMDataClass5G_ (N) SA 数据类, 则此扩展是必需的。

仅当相应的 SystemType 是 MGBIMDataClassLTE 或 MBIMDataClass5G_ (N) SA 时, RSRP 和 SNR 字段才有效。 如果调制解调器报告 RSRP 和/或 SNR, 则 RSSI 字段应设置为**99**的值。

如果相应的 SystemType 为 MBIMDataClass5G_ (N) SA, 则 RSRP 字段是必需的, 并且 SNR 字段是可选的。 如果相应的 SystemType 为 MBIMDataClassLTE, 则 RSRP 和 SNR 字段是可选的, 可以改为使用 RSSI 字段。 在这种情况下, 可以通过为**RsrpSnrOffset**和**RsrpSnrSize**成员设置零 (**0**) 值来省略 RSRP 和 SNR 字段。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_SIGNAL_STATE | 空 | 不适用 |
| 响应 | MBIM_SIGNAL_STATE_INFO_V2 | MBIM_SIGNAL_STATE_INFO_V2 | MBIM_SIGNAL_STATE_INFO_V2 |

### <a name="query"></a>查询

InformationBuffer 为 null, 而 InformationBufferLength 为零。

### <a name="set"></a>设置

[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中介绍了 set 命令的信息。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 中的 InformationBuffer 包含以下 MBIM_SIGNAL_STATE_INFO_V2 结构。

#### <a name="mbim_signal_state_info_v2"></a>MBIM_SIGNAL_STATE_INFO_V2

| 偏移量 | Size | 字段 | type | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Rssi | UINT32 | 请参阅[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中的表10.58。 |
| 4 | 4 | ErrorRate | UINT32 | 请参阅[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)中的表10.58。 |
| 8 | 4 | SignalStrengthInterval | UINT32 | 报告间隔 (秒)。 |
| 12 | 4 | RssiThreshold | UINT32 | 触发报表的 RSSI 编码值的不同之处。 如果这并不重要, 则使用0xFFFFFFFF。 |
| 16 | 4 | ErrorRateThreshold | UINT32 | 触发报表的 ErrorRate 编码值的不同之处。 如果这并不重要, 则使用0xFFFFFFFF。 |
| 20 | 4 | RsrpSnrOffset | 抵销 | 从该结构的开头计算的偏移量 (以字节为单位), 该偏移量为包含 RSRP 和 SNR 信号信息的缓冲区。 当没有可用的 RSRP 和 SNR 信号信息时, 此成员可为**NULL** 。 |
| 24 | 4 | RsrpSnrSize | 规格 | 缓冲区的大小 (以字节为单位), 包含 RSRP 和 SNR 信号信息, 格式为 MBIM_RSRP_SNR_INFO 结构。 |
|   | 4 | DataBuffer | DATABUFFER | MBIM_RSRP_SNR 结构。 |

#### <a name="mbim_rsrp_snr"></a>MBIM_RSRP_SNR

以下 MBIM_RSRP_SNR 结构用于 MBIM_SIGNAL_STATE_INFO_V2 结构的**DataBuffer**中。

| 偏移量 | Size | 字段 | type | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 | UINT32 | 跟随此元素的 RSRP_SNR 项的计数。 |
| 4 | 4 | DataBuffer | DATABUFFER | RSRP_SNR 记录的数组, 每个记录都指定为 MBIM_RSRP_SNR_INFO 结构。 |

#### <a name="mbim_rsrp_snr_info"></a>MBIM_RSRP_SNR_INFO

在 MBIM_RSRP_SNR 结构的**DataBuffer**中使用以下 MBIM_RSRP_SNR_INFO 结构的数组。

<table>
    <tr>
        <th>偏移量</th>
        <th>大小 ></th>
        <th>字段</th>
        <th>type</th>
        <th>描述</th>
    </tr>
    <tr>
        <td>0</td>
        <td>4</td>
        <td>RSRP</td>
        <td>UINT32</td>
        <td>
            <table>
                <tr>
                    <th>RSRP 值 (dBm)</th>
                    <th>编码值 (最小 = 0, 最大 = 126)</th>
                </tr>
                <tr>
                    <td>小于-156</td>
                    <td>0</td>
                </tr>
                <tr>
                    <td>小于-155</td>
                    <td>1</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>小于-138</td>
                    <td>18</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>小于-45</td>
                    <td>111</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>小于-31</td>
                    <td>125</td>
                </tr>
                <tr>
                    <td>-31 或更大</td>
                    <td>126</td>
                </tr>
                <tr>
                    <td>未知或无法检测</td>
                    <td>127</td>
                </tr>
            </table>
        </td>
    </tr>
    <tr>
        <td>4</td>
        <td>4</td>
        <td>SNR</td>
        <td>UINT32</td>
        <td>
            <table>
                <tr>
                    <th>数据库中的 SNR 值</th>
                    <th>编码值 (最小 = 0, 最大 = 127)</th>
                </tr>
                <tr>
                    <td>小于-23</td>
                    <td>0</td>
                </tr>
                <tr>
                    <td>小于-22。5</td>
                    <td>1</td>
                </tr>
                <tr>
                    <td>小于-22</td>
                    <td>2</td>
                </tr>
                <tr>
                    <td>小于-21。5</td>
                    <td>3</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>小于39。5</td>
                    <td>125</td>
                </tr>
                <tr>
                    <td>小于40</td>
                    <td>126</td>
                </tr>
                <tr>
                    <td>40或更高版本</td>
                    <td>127</td>
                </tr>
                <tr>
                    <td>未知或无法检测</td>
                    <td>128</td>
                </tr>
            </table>
        </td>
    </tr>
    <tr>
        <td>8</td>
        <td>4</td>
        <td>RSRPThreshold</td>
        <td>UINT32</td>
        <td>定义旧 (已缓存) RSRP 值与新计算的 RSRP 值之间的阈值。 如果绝对差异大于阈值, 则设备会触发一个未经请求的事件。 单位为 1 dBm。 如果设置为零, 则使用设备函数中的默认行为。 如果设置为 0xFFFFFFFF, 请不要使用它来触发事件。 如果设备不支持给定的阈值, 则它将返回它所支持的最大阈值。</td>
    </tr>
    <tr>
        <td>12</td>
        <td>4</td>
        <td>SNRThreshold</td>
        <td>UINT32</td>
        <td>定义旧 (已缓存) SNR 值与新计算的 SNR 值之间的阈值。 如果绝对差异大于阈值, 则设备会触发一个未经请求的事件。 单位为 1 dB。 如果设置为零, 则使用设备函数中的默认行为。 如果设置为 0xFFFFFFFF, 请不要使用它来触发事件。 如果设备不支持给定的阈值, 则它将返回它所支持的最大阈值。</td>
    </tr>
    <tr>
        <td>16</td>
        <td>4</td>
        <td>SystemType</td>
        <td>MBIM_DATA_CLASS</td>
        <td>指示信号状态信息有效的系统类型。 此成员是<a href="#mbim_data_class">MBIM_DATA_CLASS</a>中定义的一种类型的位掩码。</td>
    </tr>
</table>

### <a name="unsolicited-events"></a>未经请求的事件

通知包含 MBIM_SIGNAL_STATE_INFO_V2 结构。

### <a name="status-codes"></a>状态代码

此 CID 仅使用[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)的9.4.5 部分中定义的通用状态代码。
