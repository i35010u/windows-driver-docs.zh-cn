---
title: MB 5g 数据类支持
description: MB 5g 数据类支持
ms.assetid: 16531A63-76EC-4722-8817-FA8DB3B2B82F
keywords:
- MB 5g 数据类支持，移动宽带的 5 个 G 数据类的支持
ms.date: 04/17/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c895a81e549bcd856ff796c1cdddd85bbbcf82d9
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905253"
---
# <a name="mb-5g-data-class-support"></a>MB 5g 数据类支持

## <a name="terminology"></a>术语

本主题使用以下术语：

| 术语 | 定义 |
| --- | --- |
| NR | 新单选。 NR 是指 5g 时在 3GPP 中使用的术语。 |
| MBB | 移动宽带。 |
| EPC | 增强的数据包核心。 引用 LTE 核心网络时在 3GPP 中使用的术语。 |
| NGC | 下一代核心。 引用 5g 核心网络时在 3GPP 中使用的术语。 EPC NR 等效。 |
| DC | 双建立连接。 网络可以支持 LTE 和 5g NR，包括双与其设备具有 LTE 和 NR 同时连接的连接。 |
| SA | 独立 5g。 是指任何基于 NGC NR 网络，其中最常见的是选项 2，独立 NR。 |
| NSA | 非独立 5g。 是指任何基于 EPC 的 NR 网络，其中最常见的是选项 3，非独立 NR。 |
| gNB | 支持 NR 无线接口以及连接到 NGC NR 单选基站。 |
| RAT | 单选访问技术。 |

## <a name="overview"></a>概述

Windows 10，版本 1903年是为 IHV 合作伙伴支持 5g 移动宽带驱动程序的第一个 Windows 版本。 名称*5g*是友好名称，为新单选 (NR)，在引入[3GPP 版本 15 规范](http://www.3gpp.org/release-15)。 NR 是提供一组全面的标准，设想提供 true 长期发展到现有的第四代 LTE 介绍的技术，可能会从窄带到超宽带和到名义上的所有移动电话通信需求关键的延迟要求。 作为一种技术，5g 应开发一段长达十年时间。 

本主题介绍 Windows 支持的 Windows 10，版本 1903，开头 5g 增强移动宽带 (eMBB) 超过 5g nonstandalone 基于 EPC 的网络中的 5 个 G 的第一个步骤。

## <a name="windows-5g-mbim-interface-extension"></a>Windows 5g MBIM 接口扩展

### <a name="mbim-interface"></a>MBIM 接口

Windows 10，版本 1903，截至 5g 总的来说仍在开发。 下表总结了从该处 5g 网络将部署，以不同的网络体系结构选项 (1-7) 的特征的不同阶段。 选项 1 表示现有 LTE 移动宽带，这很好地支持 Windows 平台上。

![移动宽带 5g 部署选项](images/mb-5g-deployment-options.png "移动宽带 5g 部署选项")

选项 3 或"nonstandalone"(NSA) 5g 网络应部署的主要的移动运营商 (MOs) 从 2019 年开始在世界各地。 基于 NGC，或"独立"(SA) 选项 2/4/5/7 网络应部署更广泛地开始在 2020年，最早。

支持的选项 3 (NSA) 在 Windows 10，版本 1903年中引入了基于 EPC 的 5g 网络。 但是，基于 NGC (SA) 网络是仍处于开发阶段。 因此，在 Windows 中的 5 个 G 支持是易于扩展和并行情况下，完全向后兼容旧调制解调器。 

[MBIM 1.0 勘误表规范](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)有一种机制来添加并公布可选 Cid，但它缺少一种机制来更改现有 Cid 与新的负载或修改后的负载，或在引入无法满足的任何更改可选的 Cid。 MBIM 1.0 勘误表规范中的每个有效负载可能包含固定的大小成员或动态大小偏移量/大小对成员。 如果存在动态大小调整的成员，最后一个成员是大小可变的缓冲区。 尽管最大程度地避免重大更改了，但它们都不可避免要支持所有 5g 网络要求。

Windows 10，版本 1903年已通过添加支持的选项 3 (NSA) 5g 更新 MBIM 1.0 规范的网络，包括对现有 Cid 的重大更改。 此外在 Windows 10，版本 1903，以及新的 CID 以使宿主能够播发其 MBIM 发行版号和 MBIM 扩展版本号 MBIM 设备添加了新的 MBIM 扩展版本 2.0。

### <a name="ndis-interface"></a>NDIS 接口

NDIS 支持 NDIS_HEADER 中的修订号。 这允许将新成员添加到一个 OID 消息后，尽管并非所有微型端口驱动程序遵循版本编号，并且不能容忍新修订版本。 在这种情况下，微型端口驱动程序版本可以用于确定是否是否驱动程序支持 OID 的较新版本。 但是，因为这会向 IHV 驱动程序添加一个依赖项，而是 NDIS 使用中的可选服务 caps 表[OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)。

已为 5g 数据类支持更新以下 NDIS Oid 和他们的数据结构。

- [OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)
- [OID_WWAN_REGISTER_STATE](oid-wwan-register-state.md)
- [OID_WWAN_PACKET_SERVICE](oid-wwan-packet-service.md)
- [OID_WWAN_SIGNAL_STATE](oid-wwan-signal-state.md)

这些 Oid 的等效 MBIM CID 消息本主题的以下各节所述。

## <a name="mbim-extensions-release-20---5g-nonstandalone-epc-based-option-3-network-support"></a>MBIM 扩展版本 2.0-5 G nonstandalone (基于 EPC 的选项 3) 网络支持

因为[MBIM 1.0 勘误表规范](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)缺少一种机制来更改现有的新的或修改有效负载，Windows 10 中，Cid 1903 引入了 MBIM 1.0 Extension 2.0 扩展接口以支持 5 个 G 的版本。

### <a name="versioning-scheme"></a>版本控制方案

> [!NOTE]
> 在本部分中，术语*MBIMEx 版本*指 MBIM 扩展发行版号。

主机得知通过两种方法的设备的 MBIMEx 版本：

1. MBIM 扩展功能描述符。
2. 可选 MBM_CID_VERSION 的消息，如果设备支持它并且声明对它的支持。

如果这两个不同，更高版本的设备仍保持枚举到主机的持续时间指示 MBIMEx 版本。 更高版本的 MBIMEx 版本设备的方式被称为*宣布 MBIMEx 版本*。 设备的宣布 MBIMEx 版本可以是低于其本机 MBIMEx 版本，它是设备支持的最高 MBIMEx 版本。 设备可以显式了解主机的 MBIMEx 版本，只能通过 MBIM_CID_VERSION 消息。

在任何版本中，主机始终查询设备中受支持的服务和设备初始化序列开头位置使用 MBIM_CID_DEVICE_SERVICES 的 Cid。 如果设备支持 MBIM_CID_VERSION，并且将公布其支持 MBIM_CID_DEVICE_SERVICE 查询响应中的，然后不理解 MBIM_CID_VERSION 或具有 MBIMEx 版本低于 2.0 的主机将其忽略。 同时，能理解 MBIM_CID_VERSION 并具有本机 MBIMEx 版本 2.0 或更高版本的主机将 MBIM_CID_VERSION 消息发送到主机的本机 MBIMEx 版本中，设备和 CID 是第一个收到 MBIM 后发送到设备的 CID_CID_DEVICE_SERVICES 响应。

如果第一个收到 CID MBIM_CID_DEVICE_SERVICES 查询响应后，设备从主机接收 MBIM_CID_VERSION，设备就会知道主机的 MBIMEx 版本。 如果第一个收到 CID MBIM_CID_DEVICE_SERVICES 查询响应后，设备从主机接收任何其他 CID，则设备会假定主机的本机 MBIMEx 版本为 1.0。

，更高版本的 MBIMEx 版本是所有较低的 MBIMEx 版本的超集。 主机支持我们已经发出通告的 MBIMEx 版或以下主机的本机 MBIMEx 版本的所有设备。 如果设备的宣布 MBIMEx 版本高于主机的本机 MBIMEx 版本，主机不应支持的设备，并在此情况下主机的具体行为是不确定。

想要使用较旧主机的设备最初应播发 MBIMEx 版本 1.0 或与设备用于工作的在扩展功能描述符 MBIM 的最低主机 MBIMEx 版本。 如果主机发送 MBIM_CID_VERSION，并且主机具有更高版本的 MBIMEx 版本不是设备最初播发，则在 MBIM_CID_VERSION 响应中，设备应指示最多的主机的本机 MBIMEx 版本较小者的更高版本 MBIMEx 版本和设备的本机 MBIMEx 版本。

> [!NOTE]
> 例如，设备支持 MBIMEx 版本 2.0 中，只用于使用较旧版本的操作系统不支持 MBIMEx 2.0。 设备最初播发 MBIMEx 1.0 版中的 USB 描述符并播发对可选 MBIM_CID_VERSION 的支持。 插入到运行 Windows 10，版本 1803 的主机时主机并不了解 MBIM_CID_VERSION 并不向设备发送 MBIM_CID_VERSION。 到主机，设备的 MBIMEx 版本为 1.0。 主机仍会继续发送初始化序列中的其他 Cid。 收到非 MBIM_CID_VERSION Cid 时，设备识别主机支持 MBIMEx 1.0 版。 双方继续符合 MBIMEx 1.0 版。 更高版本，在同一设备插入到运行 Windows 10，版本 1903年 2.0 中，本机 MBIMEx 版本的主机时主机将 MBIM_CID_VERSION 发送到设备，以通知其主机的本机 MBIMEx 版本是 2.0。 设备发送与设备的响应中 MBIM_CID_VERSION 宣布 MBIMEx 2.0 版。 在这里，双方继续符合 MBIMEx 2.0 版。

下表显示了具有三个假设主机和三个假设设备，每个都具有声明其本机 MBIMEx 版本的兼容性矩阵。 设备播发 MBIMEx 版本 1.0 最初在 USB 描述符。 该矩阵显示每个设备使用每个主机的行为方式。

| （下面） 调制解调器 / OS （右） | Windows 10，版本 1809年或更早 (本机 MBIMEx 1.0 版) | Windows 10，版本 1903年和更高版本 (MBIMEx 版本 2.0) |
| --- | --- | --- |
| 4g 设备 <p>本机 MBIMEx 版本 1.0</p> | 设备最初会通告 MBIMEx 1.0。 没有 MBIM_CID_VERSION exchange。 兼容的设备和主机。 默认情况下使用 MBIMEx 1.0 版。 | 设备最初会通告 MBIMEx 1.0。 没有 MBIM_CID_VERSION exchange。 主机可用于使用 MBIMEx 1.0 的设备。 |
| 5g NSA 设备 <p>本机 MBIMEx 2.0 版</p> | 设备最初会通告 MBIMEx 1.0。 没有 MBIM_CID_VERSION exchange。 设备识别主机具有 MBIMEx 1.0，并继续使用 MBIMEx 1.0。 | 设备最初会通告 MBIMEx 1.0。 主机发送 MBIM_CID_VERSION 以通知设备主机支持 MBIMEx 2.0。 设备使用 MBIMEx 2.0 进行响应。 双方继续 MBIMEx 2.0。 |

下表列出了在 MBIMEx 版本 2.0 中，并且其已修改的有效负载中修改的所有现有 Cid。 在这些 Cid 所有 unmentioned 的负载和所有其他 Cid 不表执行进位通过从 MBIMEx 版本 1.0 中所述，保持不变。 

| CID | 有效负载 |
| --- | --- |
| MBIM_CID_REGISTER_STATE | MBIM_REGISTRATION_STATE_INFO_V2 |
| MBIM_CID_PACKET_SERVICE | MBIM_PACKET_SERVICE_INFO_V2 |
| MBIM_CID_SIGNAL_STATE | MBIM_SIGNAL_STATE_INFO_V2 |

## <a name="mbim-service"></a>MBIM 服务

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft Basic IP 连接扩展 | UUID_BASIC_CONNECT_EXTENSIONS | 3D01DCC5-FEF5-4D05-9D3A-BEF7058E9AAF |

## <a name="mbimcidversion"></a>MBIM_CID_VERSION

MBIM_CID_VERSION 是用于交换 MBIM 主机和设备之间的版本信息的可选命令。 如果设备需要与旧版 MBIM 向后的兼容性，它必须支持此命令。

如果设备支持，该主机以查询形式发送此命令。 查询包含 MBIM 发行版号和 MBIM 扩展发行版号的主机目前支持。

设备在设备端，调整其公布的 MBIM 发行版号和基于中定义的规则 MBIM 扩展版本号[版本控制方案](#versioning-scheme)，然后将其发送到主机在响应中。

此命令定义下**基本连接扩展**服务。

| CID | 命令代码 | UUID |
| --- | --- | --- |
| MBIM_CID_VERSION | 15 | 3d01dcc5-fef5-4d05-0d3abef7058e9aaf |

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | MBIM_VERSION_INFO | 不适用 |
| 响应 | 不适用 | MBIM_VERSION_INFO | 不适用 |

### <a name="query"></a>查询

通知主机的本机 MBIM 发行版号以及 MBIM 扩展发行版号的设备。 InformationBuffer 包含以下 MBIM_VERSION_INFO 结构。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 2 | bcdMBIMVersion | UINT16 | 带有隐含小数点位 7 和 8 之间 BCD 时，在发送方 MBIM 发行版号。 例如，`0x0100 == 1.00 == 1.0`。 这是一个小字节序常量，因此字节是 0x00，然后 0x01。 |
| 2 | 2 | bcdMBIMExtendedVersion | UINT16 | MBIM 扩展发布带有隐含小数点位 7 和 8 之间 BCD 时，在发送方的数目。 例如，`0x0100 == 1.00 == 1.0`。 这是一个小字节序常量，因此字节是 0x00，然后 0x01。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

在 MBIM_COMMAND_DONE InformationBuffer 包含 MBIM_VERSION_INFO 结构。

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

此 CID 仅使用 9.4.5 节中定义的泛型状态代码[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。

## <a name="mbimcidmsdevicecapsv2"></a>MBIM_CID_MS_DEVICE_CAPS_V2

此 CID 是上定义的相同[MB 多 SIM operations](mb-multi-sim-operations.md#mbim-interface-update-for-multi-sim-operations)，其本身是 MBIM_CID_MS_DEVICE_CAPS 的扩展，如 10.5.1 节中定义[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 MBIM 扩展的 2.0 版，有新数据类 MBIM_DATA_CLASS 表中定义，使设备能够报告其 5g 功能。 MBIMDataClass5G_NSA 表示设备是否支持 5 个 G 非-独立 (NSA) 中定义[3GPP TS 37.340](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3198)，MBIMDataClass5G_SA 表示设备是否支持 5 个 G 独立 (SA)，也在 3GPP TS 37.340 中定义。

如果设备支持这两个新的数据类，则应设置两个位。

### <a name="mbimdataclass"></a>MBIM_DATA_CLASS

| 类型 | 掩码 |
| --- | --- |
| MBIMDataClassNone | 0h |
| MBIMDataClassGPRS | 1h |
| MBIMDataClassEDGE | 2h |
| MBIMDataClassUMTS | 4h |
| MBIMDataClassHSDPA | 8h |
| MBIMDataClassHSUPA | 10h |
| MBIMDataClassLTE | 20h |
| **MBIMDataClass5G_NSA** | **40h** |
| **MBIMDataClass5G_SA** | **80 h** |
| 保留 | 100h-8000 h |
| MBIMDataClass1XRTT | 10000 h |
| MBIMDataClass1XEVDO | 20000 h |
| MBIMDataClass1XEVDORevA | 40000 h |
| MBIMDataClass1XEVDV | 支持 80000 h |
| MBIMDataClass3XRTT | 100000 h |
| MBIMDataClass1XEVDORevB | 200000 h |
| MBIMDataClassUMB | 400000 h |
| 保留 | 800000 40000000 h |
| MBIMDataClassCustom | 80000000 h |

## <a name="mbimcidregisterstate"></a>MBIM_CID_REGISTER_STATE

此命令是扩展中已定义 MBIM_CID_REGISTER_STATE CID [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 此扩展添加一个名为的新成员**PreferredDataClasses**响应结构。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_REGISTRATION_STATE | 空 | 不适用 |
| 响应 | MBIM_REGISTRATION_STATE_INFO_V2 | MBIM_REGISTRATION_STATE_INFO_V2 | MBIM_REGISTRATION_STATE_INFO_V2 |

### <a name="query"></a>查询

InformationBuffer 为 null，InformationBufferLength 为零。

### <a name="set"></a>设置

设置注册状态。 信息是相同的中所述[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。

### <a name="response"></a>响应

在 MBIM_COMMAND_DONE InformationBuffer 包含以下 MBIM_REGISTRATION_STATE_INFO_V2 结构。 与 10.5.10.6 节中定义的 MBIM_REGISTRATION_STATE_INFO 结构相比[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)，以下结构有一个新的**PreferredDataClasses**字段。 除非另有说明，字段说明中的表 10-55 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)应用于此结构。

#### <a name="mbimregistrationstateinfov2"></a>MBIM_REGISTRATION_STATE_INFO_V2

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NwError | UINT32 | 一个特定于网络错误。 表 10-44 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)介绍用于 NwError 的原因代码。 |
| 4 | 4 | RegisterState | MBIM_REGISTER_STATE | 请参阅表 10-46 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 |
| 8 | 4 | RegisterMode | MBIM_REGISTER_MODE | 请参阅表 10-47 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 |
| 12 | 4 | AvailableDataClass | UINT32 | 中的值的位图[MBIM_DATA_CLASS](#mbimdataclass) ，表示已注册的网络，单元格注册该设备上的受支持的数据类。 <p>如果此值设置为 MBIMDataClassNone **RegisterState**不是**MBIMRegisterStateHome**， **MBIMRegisterStateRoaming**，或**MBIMRegisterStatePartner**。 </p> |
| 16 | 4 | CurrentCellularClass | MBIM_CELLULAR_CLASS | 指示当前的移动电话类使用的多模式函数。 请参阅表 10-8 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)有关详细信息。 <p>对于单模式函数，这是与移动电话 MBIM_CID_DEVICE_CAPS 中报告的类相同。 对于多模式函数，指示从 CDMA 转换到 GSM 或从外部使用的已更新**CurrentCellularClass**。 </p> |
| 20 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串**ProviderId**表示网络提供程序标识。 <p>为基于 GSM 的网络，此字符串是三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc) 的串联。 基于 GSM 的运营商可能具有多个 mnc 是否，并因此多台**ProviderId**。</p><p>为基于 CDMA 的网络，此字符串是一个 5 位数字系统 ID (SID)。 通常情况下，基于 CDMA 的承运人具有多个 SID。 通常情况下，承运人具有通常除以地理位置内的国家/地区法规，如都市统计区域 (MSA) 在美国每个市场为一个 SID。 如果此信息不可用，则基于 CDMA 的设备必须指定 MBIM_CDMA_DEFAULT_PROVIDER_ID。</p><p>在自动注册模式下处理查询请求和注册状态时，此成员包含与该设备是当前关联 （如果适用） 的提供程序 ID。 在手动注册模式下的注册状态时，此成员包含向其请求设备注册 （即使该提供程序不可用） 的提供程序 ID。</p><p>在手动模式下处理 set 请求和注册状态时，这包含用来注册设备的主机选择的提供程序 ID。 自动注册模式下的注册状态时，将忽略此参数。</p><p>如果提供程序 ID 不可用，CDMA 1xRTT 提供程序必须设置为 MBIM_CDMA_DEFAULT_PROVIDER_ID。</p> |
| 24 | 4 | ProviderIdSize | SIZE(0..12) | 大小 （字节），对于**ProviderId**。 |
| 28 | 4 | ProviderNameOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到一个字符串称为**ProviderName**表示网络提供商的名称。 此成员仅限于最多 MBIM_PROVIDERNAME_LEN 字符。 <p>为基于 GSM 的网络，如果首选的演示文稿的国家/地区首字母缩写和移动网络名称 (PCCI & N) 的长度超过 20 个字符，设备应使用缩写的网络名称。</p><p>主机设置首选提供程序列表时，将忽略此成员。 设备应指定不具有此信息的设备的一个 NULL 字符串。</p> |
| 32 | 4 | ProviderNameSize | SIZE(0..40) | 大小 （字节），对于**ProviderName**。 |
| 36 | 4 | RoamingTextOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到一个字符串称为**RoamingText**以通知用户设备漫游。 此成员仅限于最多 63 个字符。 注册状态为 MBIMRegisterStatePartner 或 MBIMRegisterStateRoaming 时，此文本应该向用户提供的其他信息。 此成员是可选的。 |
| 40 | 4 | RoamingTextSize | SIZE(0..126) | 大小 （字节），对于**RoamingText**。 |
| 44 | 4 | RegistrationFlag | MBIM_REGISTRATION_FLAGS | 标志设置每个表 10-48 中[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 |
| 48 | 4 | PreferredDataClass | UINT32 | 中的值的位图[MBIM_DATA_CLASS](#mbimdataclass)在设备上的已启用的数据类。 设备只可使用已启用的数据类。 |
| 动态 | 4 | DataBuffer | DATABUFFER | 包含的数据缓冲区**ProviderId**， **ProviderName**，并**RoamingText**。 |

### <a name="unsolicited-events"></a>未经请求的事件

通知包含 MBIM_REGISTRATION_STATE_INFO_V2 结构。

### <a name="status-codes"></a>状态代码

此 CID 仅使用 9.4.5 节中定义的泛型状态代码[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。

## <a name="mbimcidpacketservice"></a>MBIM_CID_PACKET_SERVICE

此命令是扩展中定义的现有 MBIM_CID_PACKET_SERVICE [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。

此扩展添加一个名为的新成员**FrequencyRange**响应结构，重命名**HighestAvailableDataClass**成员添加到**CurrentDataClass**到说明其用途。

**CurrentDataClass**指示单选访问技术 (RAT) 与其当前注册该设备。 它包含的单个值[MBIM_DATA_CLASS](#mbimdataclass)。

**FrequencyRange**指示设备当前使用的频率范围。 这会有效。 仅当**CurrentDataClass**字段指示 MBIMDataClass5G_NSA 或 MBIMDataClass5G_SA 位是否设置。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_PACKET_SERVICE | 空 | 不适用 |
| 响应 | MBIM_PACKET_SERVICE_INFO_V2 | MBIM_PACKET_SERVICE_INFO_V2 | MBIM_PACKET_SERVICE_INFO_V2 |

### <a name="query"></a>查询

InformationBuffer 为 null，InformationBufferLength 为零。

### <a name="set"></a>设置

Set 命令的信息是中所述[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。

### <a name="response"></a>响应

在 MBIM_COMMAND_DONE InformationBuffer 包含 MBIM_PACKET_SERVICE_INFO_V2 结构。 与 10.5.10.6 节中定义的 MBIM_PACKET_SERVICE_INFO 结构相比[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)，但这个新结构具有**CurrentDataClass**和**FrequencyRange**字段。 除非另行说明，字段说明在表 10-55 的[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)在此处适用。

#### <a name="mbimpacketserviceinfov2"></a>MBIM_PACKET_SERVICE_INFO_V2

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NwError | UINT32 | 一个特定于网络错误。 表 10-44 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)介绍用于 NwError 的原因代码。 |
| 4 | 4 | PacketServiceState | MBIM_PACKET_SERVICE_STATE | 请参阅表 10-53 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 | 
| 8 | 4 | CurrentDataClass | MBIM_DATA_CLASS | 当前数据中的类的当前单元格，指定根据[MBIM_DATA_CLASS](#mbimdataclass)。 如果该函数不在附加的数据包服务状态，函数必须将此成员设置为 MBIMDataClassNone。 除了 HSPA （换而言之，HSUPA 和 HSDPA） 和 5 G DC，函数将此成员设置为单个 MBIM_DATA_CLASS 值。 对于 HSPA 数据服务，函数指定的按位或的 MBIMDataClass HSDPA 和 MBIMDataClassHSUPA。 对于支持 HSDPA 但不是 HSUPA 的单元格，仅 HSDPA 被指示 （这意味着 UMTS 上行数据的数据类）。 函数每当当前数据类的更改时发送通知的新值，该值指示**CurrentDataClass**。 |
| 12 | 8 | UplinkSpeed | UINT64 | 包含比特 / 秒上行比特率。 |
| 20 | 8 | DownlinkSpeed | UINT64 | 包含下行链路比特率，比特 / 秒。 |
| 38 | 4 | FrequencyRange | MBIM_FREQUENCY_RANGE | 中的值的位掩码[MBIM_FREQUENCY_RANGE](#mbimfrequencyrange) ，表示当前使用设备的频率范围。 此值仅有效如果**CurrentDataClass** MBIMDataClass5G_NSA 或 MBIMDataClass5G_SA。 |

#### <a name="mbimfrequencyrange"></a>MBIM_FREQUENCY_RANGE

以下枚举用作上述 MBIM_PACKET_SERVICE_INFO_V2 结构中的值。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述|
| --- | --- | --- |
| MBIMFrequencyRangeUnknown | 0 | 如果系统类型不 5g。 |
| MBIMFrequencyRange1 | 1 | 中的频率范围 1 (FR1) [3GPP TS 38.101 1](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3283) (Sub-6 G)。 |
| MBIMFrequencyRange2 | 2 | 在 FR2 [3GPP TS 38.101 2](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3284) (mmWave)。 |
| MBIMFrequencyRange1AndRange2 | 3 | 如果连接 FR1 和 FR2 运营商。 |

### <a name="unsolicited-events"></a>未经请求的事件

通知包含 MBIM_PACKET_SERVICE_INFO_V2 结构。

### <a name="status-codes"></a>状态代码

此 CID 仅使用 9.4.5 节中定义的泛型状态代码[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。

## <a name="mbimcidsignalstate"></a>MBIM_CID_SIGNAL_STATE

此 CID 是 MBIM_CID_SIGNAL_STATE，RSRP 和 SNR 简介信号状态条件的扩展。 此新扩展才有效设备将指示 MBIM 扩展版本 2.0 的支持。 此扩展是如果调制解调器支持 MBIMDataClass5G_ (N) SA 数据类必需的。

RSRP 和 SNR 字段的有效前提是相应 SystemType 是 MGBIMDataClassLTE 或 MBIMDataClass5G_ (N) SA。 如果调制解调器报告 RSRP 和/或 SNR，则 RSSI 字段应设置为值**99**。

如果相应 SystemType MBIMDataClass5G_ (N) SA，RSRP 字段是必需的 SNR 字段是可选的。 如果相应 SystemType，MBIMDataClassLTE RSRP 和 SNR 字段是可选的可以改为使用 RSSI 字段。 在这种情况下，可以通过设置零省略 RSRP 和 SNR 字段 (**0**) 值均**RsrpSnrOffset**并**RsrpSnrSize**成员。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_SIGNAL_STATE | 空 | 不适用 |
| 响应 | MBIM_SIGNAL_STATE_INFO_V2 | MBIM_SIGNAL_STATE_INFO_V2 | MBIM_SIGNAL_STATE_INFO_V2 |

### <a name="query"></a>查询

InformationBuffer 为 null，InformationBufferLength 为零。

### <a name="set"></a>设置

Set 命令的信息是中所述[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。

### <a name="response"></a>响应

在 MBIM_COMMAND_DONE InformationBuffer 包含以下 MBIM_SIGNAL_STATE_INFO_V2 结构。

#### <a name="mbimsignalstateinfov2"></a>MBIM_SIGNAL_STATE_INFO_V2

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Rssi | UINT32 | 请参阅中的表 10.58 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 |
| 4 | 4 | ErrorRate | UINT32 | 请参阅中的表 10.58 [MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。 |
| 8 | 4 | SignalStrengthInterval | UINT32 | 报告间隔，以秒为单位。 |
| 12 | 4 | RssiThreshold | UINT32 | RSSI 的区别编码触发报表的值。 如果这并不重要，请使用 0xFFFFFFFF。 |
| 16 | 4 | ErrorRateThreshold | UINT32 | 在 ErrorRate 区别编码触发报表的值。 如果这并不重要，请使用 0xFFFFFFFF。 |
| 20 | 4 | RsrpSnrOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到包含 RSRP 和 SNR 信号信息的缓冲区。 此成员可以是**NULL**时没有 RSRP 和 SNR 信号信息，请访问。 |
| 24 | 4 | RsrpSnrSize | 大小 | 以字节为单位，包含 RSRP 和 SNR 信号 MBIM_RSRP_SNR_INFO 结构的格式中的信息的缓冲区的大小。 |
|   | 4 | DataBuffer | DATABUFFER | 一种 MBIM_RSRP_SNR 结构。 |

#### <a name="mbimrsrpsnr"></a>MBIM_RSRP_SNR

中使用以下 MBIM_RSRP_SNR 结构**DataBuffer** MBIM_SIGNAL_STATE_INFO_V2 结构。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount | UINT32 | 请按照此元素的 RSRP_SNR 条目的计数。 |
| 4 | 4 | DataBuffer | DATABUFFER | 每个指定为 MBIM_RSRP_SNR_INFO 结构 RSRP_SNR 记录的数组。 |

#### <a name="mbimrsrpsnrinfo"></a>MBIM_RSRP_SNR_INFO

中使用以下 MBIM_RSRP_SNR_INFO 结构的数组**DataBuffer** MBIM_RSRP_SNR 结构。

<table>
    <tr>
        <th>偏移量</th>
        <th>大小 ></th>
        <th>字段</th>
        <th>在任务栏的搜索框中键入</th>
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
                    <th>在 dBm RSRP 值</th>
                    <th>编码的值 (最小值 = 0，最大 = 126)</th>
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
                    <td>-31 或更高版本</td>
                    <td>126</td>
                </tr>
                <tr>
                    <td>未知或未找到</td>
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
                    <th>在 dB 中的 SNR 值</th>
                    <th>编码的值 (最小值 = 0，最大 = 127)</th>
                </tr>
                <tr>
                    <td>小于-23</td>
                    <td>0</td>
                </tr>
                <tr>
                    <td>小于-22.5</td>
                    <td>1</td>
                </tr>
                <tr>
                    <td>小于-22</td>
                    <td>2</td>
                </tr>
                <tr>
                    <td>小于-21.5</td>
                    <td>3</td>
                </tr>
                <tr>
                    <td>...</td>
                    <td>...</td>
                </tr>
                <tr>
                    <td>小于 39.5</td>
                    <td>125</td>
                </tr>
                <tr>
                    <td>小于 40</td>
                    <td>126</td>
                </tr>
                <tr>
                    <td>40 或更高版本</td>
                    <td>127</td>
                </tr>
                <tr>
                    <td>未知或未找到</td>
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
        <td>定义在旧的 （缓存） RSRP 值和新计算的 RSRP 值之间的阈值。 如果绝对差异大于阈值的值，设备会触发一个未经请求的事件。 单位为 1 dBm。 如果设置为零，则在设备函数中使用的默认行为。 如果设置为 0xFFFFFFFF，不要使用此触发的事件。 如果设备不支持给定的阈值，则返回它所支持的最大阈值。</td>
    </tr>
    <tr>
        <td>12</td>
        <td>4</td>
        <td>SNRThreshold</td>
        <td>UINT32</td>
        <td>定义在旧的 （缓存） SNR 值和新计算的 SNR 值之间的阈值。 如果绝对差异大于阈值的值，设备会触发一个未经请求的事件。 单位为 1 个 dB。 如果设置为零，则在设备函数中使用的默认行为。 如果设置为 0xFFFFFFFF，不要使用此触发的事件。 如果设备不支持给定的阈值，则返回它所支持的最大阈值。</td>
    </tr>
    <tr>
        <td>16</td>
        <td>4</td>
        <td>SystemType</td>
        <td>MBIM_DATA_CLASS</td>
        <td>指示信号的状态信息的有效的系统类型。 此成员是一种类型的位掩码中定义<a href="#mbimdataclass">MBIM_DATA_CLASS</a>。</td>
    </tr>
</table>

### <a name="unsolicited-events"></a>未经请求的事件

通知包含 MBIM_SIGNAL_STATE_INFO_V2 结构。

### <a name="status-codes"></a>状态代码

此 CID 仅使用 9.4.5 节中定义的泛型状态代码[MBIM 规范修订版本 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)。
