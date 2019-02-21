---
title: MB 多 SIM 操作
description: MB 多 SIM 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ed574ad545900fa22d779253824d49c32d4205c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534571"
---
# <a name="mb-multi-sim-operations"></a>MB 多 SIM 操作

## <a name="desktop-multi-modem-multi-executor-support"></a>桌面多调制解调器多执行器支持

传统上，非 phone Windows 设备尚未配置的多 SIM 调制解调器因为它们具有比手机的较少的物理空间约束。 这使他们能够真正而不是让一个调制解调器具有多个 SIM 卡像手机一样; 同时利用多个活动的无线电收发器但是，由于在企业中的 esim 卡和方案的兴起，增加非 phone 设备上的每个调制多 SIM 支持的需求。

最典型的多 SIM phone 设备有双 SIM 插槽，但仅限于一个主 SIM 卡支持数据时其他仅支持语音功能。 因为所有 SIM 卡都用于数据连接非电话 PC 模型中不存在此类限制。

尽管本规范中定义的框架从理论上来说可以支持不限的数量的调制解调器和 SIM 卡，Windows 10 版本 1703年及更高版本支持仅限双 SIM 单一活动方案端到端。 

## <a name="ndis-modem-interface-specification"></a>NDIS 调制解调器接口规范

### <a name="existing-interface-and-feature-gaps"></a>现有的接口和功能差距

它是可以支持多个独立调制解调器，其中每个调制解调器是一个单独的设备，都完全独立运行的双 SIM 双活动功能。 但是，这是本文档的作用域，而是关注，并且能够提供多个同时进行的 WWAN 微型端口调制解调器外到主机的移动电话网络堆栈。 本部分中定义的各种对象，并建立与多 SIM 功能相关的所有 MB 文档中使用的术语。

在硬件中的改进会导致可以维护具有多个移动电话网络的同时进行注册的设备。 在此类设备，存在被假定为"移动电话网络堆栈的多个实例"中无法保持注册每个并行运行，监视信号强度、 执行切换和侦听传入的页面。 此"移动电话网络堆栈"的每个实例将称为*执行器*本文档的其余部分。 例如，在支持的同时维护两个网络具有注册的设备的调制解调器硬件被视为具有两个执行器。

执行器是一个单个硬件收发器正在多路复用实际上是硬件和可能的逻辑表示形式。 确切的硬件具体情况视为供应商实现详细信息和超出此规范的讨论范围。 NDIS 微型端口驱动程序，执行器被称为 WWAN 微型端口适配器的多个实例。 对于 MBIM 调制解调器，由枚举复合设备上的多个 MBIM 函数表示执行器。

以下两个映像演示了双 SIM 调制解调器的逻辑视图。 每个显示了可能的执行器和 UICC 组合。

![双 SIM 调制解调器的逻辑视图](images/multi-SIM_1_dualSimModem.png "双 SIM 调制解调器的逻辑视图")

执行器内的移动电话网络堆栈被视为主要除自包含在其中执行流量 （语音和/或数据） 的执行程序可能会阻止其他维护注册的双待机调制解调器实现的情况下。

下图说明了双备用调制解调器的逻辑视图。 执行器 0，电话呼叫上的流量会导致执行器 1 无法继续注册。

![逻辑视图双待机调制解调器](images/multi-SIM_2_dualExecutors.png "双待机调制解调器的逻辑视图")

NDIS 6.7 中的 Windows 桌面的调制解调器接口模型不会提供这样的体系结构，因为它基于多个隐式假设：

* 模型假定调制解调器在单个执行器。
* 模型假定存在单个 UICC 卡直接与调制解调器硬件相关联。
* UICC 被视为如同它是单个应用程序 SIM 卡。

与此相反，Windows 移动设备上的 Microsoft 单选接口层 (RIL) 接口显式公开这些假设的重数。 在 Windows Mobile 中的移动宽带接口公开的功能通过单独的微型端口单独注册，并假定通过 RIL 界面已完成设备的某些基本配置。 若要提供等效的功能，Windows 桌面必须提供机制以发现执行器数目和槽，独立访问执行器、 定义执行器和槽之间的映射和定义内映射的应用程序每个执行器将使用的 UICC 卡。

有关移动电话网络体系结构和 Windows 10 移动版和桌面之间的差异的详细信息，请参阅[移动电话网络体系结构和实现](cellular-architecture-and-driver-model.md)。

### <a name="major-objects-and-operations"></a>主要对象和操作

下图显示了一个调制解调器的抽象模型。

![调制解调器、 执行器和槽之间的关系](images/multi-SIM_3_majorObjectsAndOperations.png "调制解调器、 执行器和槽之间的关系")

每个调制解调器由全局唯一标识符 (GUID) 标识，并包含一组的一个或多个执行器，其中每个是能够在移动电话网络上的独立注册。 每个执行器具有关联的执行器索引，一个整数，从 0 开始为第一个执行器。 此外，调制解调器公开可能包含 UICC 卡的一个或多个槽。 假定为的槽数是否大于或等于执行器数。 每个插槽有关联的索引，还开头使用 0，并与槽的电源状态和卡 （如果有） 的槽中的可用性状态相关的当前状态。

为了保持与现有的调制解调器的兼容性，每个执行器操作通过在单个槽中的 UICC 卡提供信息。 通过将每个执行器映射到一个槽的槽映射定义执行器和槽之间的关联。

在槽可能包含 UICC 卡;每个卡包含一个或多个 UICC 应用程序如 USIM、 CSIM、 ISIM，或可能是其他电话服务和非电话服务应用程序，例如 NFC 安全元素的 PKCS #15 或全球平台应用程序。 寻址和这些单个 UICC 应用程序的使用是未来的规范和带本文档讨论范围的主题。

调制解调器的 Windows 桌面 NDIS 接口表征的 Oid 和 NDIS 通知的 exchange。 在大多数情况下这些 Oid 定向到单独的执行器;但是，一些命令和通知的作用域到调制解调器。

对于非 Windows Mobile 操作系统，多执行器调制解调器将显示为一台设备具有多个物理 WWAN 微型端口实例。 每个物理微型端口实例表示执行器可保持与 NDIS 实例注册的。 可能会在运行时管理特定于上下文的数据包数据和设备服务会话创建其他虚拟实例。 特定于执行器的命令和通知通过 WWAN 微型端口 NDIS 物理实例，表示该执行器进行交换。 特定于调制解调器的命令 （即，那些并不特定于执行器的） 和其相应的通知可能会发送到或来自任何物理微型端口实例。

以下两个关系图显示在特定于执行器的命令和通知 （第一个关系图中），其中命令和通知经历和来自同一个执行器和特定于调制解调器的命令和通知 （第二个图） 中的差异其中命令可能会经过任何执行器和来自任何执行器。

![特定于执行器的命令和通知](images/multi-SIM_4_executorSpecificCommands.png "特定于执行器的命令和通知")

![特定于调制解调器的命令和通知](images/multi-SIM_4_modemSpecificCommands.png "特定于调制解调器的命令和通知")

所有 OID 集或查询对调制解调器和微型端口实例与之关联的执行器执行的请求颁发给微型端口实例。 同样，所有未经请求的通知和从微型端口实例发送未经请求的设备服务事件是适用于调制解调器和执行器的微型端口实例与之关联。 例如，从微型端口的未经请求的 NDIS_STATUS_WWAN_REGISTER_STATE 或 NDIS_STATUS_WWAN_PACKET_SERVICE 通知指示关联的调制解调器和执行器仅注册 （或数据包服务状态） 和不相关的状态其他调制解调器或其他 executor(s)。 

如果有多个调制解调器和/或设备中的多个执行器，物理微型端口关联的适配器与调制解调器和执行器的组合问题与特定调制解调器和执行程序相关的非特定于上下文的未经请求的通知组合。 

在相同的方式，如果设备具有多个调制解调器和/或多个执行程序，与特定调制解调器和执行器组合关联的物理微型端口适配器实例可以收到与该调制解调器和执行器相关的非特定于上下文的 OID 查询请求。 适配器接收此类查询请求根据 OID 定义对其进行处理。 如果因此选择的微型端口驱动程序，可以与任何其他进程中 OID 集或与该调制解调器和执行器关联的适配器的任何实例中请求查询并发处理此查询请求。 具有相同的调制解调器和执行器关联的微型端口适配器的所有实例都报告该蜂窝调制解调器和执行程序 （如单选电源状态、 注册状态、 数据包服务状态等） 的相同状态信息。  

对于具有多个调制解调器和/或多个执行器的设备，与调制解调器和执行器组合关联的物理微型端口适配器实例可以收到非上下文特定 OID 集请求。 微型端口驱动程序应跟踪的此类请求的进度。 如果一个此类集请求正在进行中的任何适配器，且尚未完成，第二个集 （对任何具有相同的调制解调器和执行器关联的适配器实例） 的请求尝试应进行排队和处理的上一个请求完成后。 

Windows 10 桌面 WMBCLASS 驱动程序中处理此集请求的争用条件，使上一个段落所述的规范; 但如果争用条件发生在调制解调器层调制解调器应遵循相同的指南进行排队冲突MBIM 函数，如果它仍在处理链接到同一基础设备的另一个函数上的设备级命令。

## <a name="oids-for-set-and-query-requests"></a>设置和查询请求的 Oid

若要查询的设备 （执行器） 和调制解调器中的槽数，以及可能会同时处于活动状态的执行器数，则主机将使用[OID_WWAN_SYS_CAPS](https://go.microsoft.com/fwlink/p/?linkid=841265)。

若要查询的执行器的功能，则主机将使用[OID_WWAN_DEVICE_CAPS_EX](https://go.microsoft.com/fwlink/p/?linkid=841266)。

若要定义绑定到每个执行器或查询当前映射的槽，则主机将使用[OID_WWAN_DEVICE_SLOT_MAPPINGS](https://go.microsoft.com/fwlink/p/?linkid=841267)。

若要查询的调制解调器上的特定位置的状态，则主机将使用[OID_WWAN_SLOT_INFO_STATUS](https://go.microsoft.com/fwlink/p/?linkid=841268)。

## <a name="per-device-and-per-executor-commands"></a>每个设备和每个执行器命令

通过添加到 Windows 10，版本 1703年及更高版本中的非 Windows 移动设备的执行器概念 Oid 现在拆分为两个类别： 每个设备 Oid 和每个执行器 Oid。 下表介绍了其 Oid 属于哪个类别。

| 每个设备或每个执行器| OID 名称 |
| --- | --- |
| 每个设备| OID_WWAN_DRIVER_CAPS |
|  | OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS |
|  | OID_WWAN_ENUMERATE_DEVICE_SERVICES |
|  | OID_WWAN_PRESHUTDOWN |
|  | OID_WWAN_VENDOR_SPECIFIC |
|  | OID_WWAN_SYS_CAPS |
|  | OID_WWAN_DEVICE_SLOT_MAPPINGS |
| 每个执行器 | OID_WWAN_AUTH_CHALLENGE |
|  | OID_WWAN_CONNECT |
|  | OID_WWAN_DEVICE_CAPS |
|  | OID_WWAN_DEVICE_CAPS_EX |
|  | OID_WWAN_DEVICE_SERVICE_COMMAND |
|  | OID_WWAN_DEVICE_SERVICE_SESSION |
|  | OID_WWAN_DEVICE_SERVICE_SESSION_WRITE |
|  | OID_WWAN_DEVICE_SERVICES |
|  | OID_WWAN_HOME_PROVIDER |
|  | OID_WWAN_NETWORK_IDLE_HINT |
|  | OID_WWAN_PACKET_SERVICE |
|  | OID_WWAN_PIN |
|  | OID_WWAN_PIN_EX |
|  | OID_WWAN_PIN_LIST |
|  | OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS |
|  | OID_WWAN_PREFERRED_PROVIDERS |
|  | OID_WWAN_PROVISIONED_CONTEXTS |
|  | OID_WWAN_RADIO_STATE |
|  | OID_WWAN_READY_INFO |
|  | OID_WWAN_REGISTER_STATE |
|  | OID_WWAN_SERVICE_ACTIVATION |
|  | OID_WWAN_SIGNAL_STATE |
|  | OID_WWAN_SMS_CONFIGURATION |
|  | OID_WWAN_SMS_DELETE |
|  | OID_WWAN_SMS_READ |
|  | OID_WWAN_SMS_SEND |
|  | OID_WWAN_SMS_STATUS |
|  | OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS |
|  | OID_WWAN_USSD |
|  | OID_WWAN_VISIBLE_PROVIDERS |
|  | OID_WWAN_SLOT_INFO_STATUS |

> [!NOTE]
> [OID_WWAN_RADIO_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569832)适用于 Windows 10，版本 1703年也已更新。 有关详细信息，请参阅 OID_WWAN_RADIO_STATE。

## <a name="mbim-interface-update-for-multi-sim-operations"></a>对于多 SIM 操作 MBIM 界面更新

对于非 Windows Mobile 操作系统，多执行器调制解调器将显示为一个 USB 复合设备，多个 MBIM 函数。 每个 MBIM 函数表示可保持注册的执行器。 特定于执行器的命令和通知交换通过 MBIM 函数表示该执行器、 特定于调制解调器的命令 （即，那些并不特定于执行器的） 时和可能会发送到或来自及其相应的通知从属于相同的基础 USB 复合设备任何 MBIM 函数。 

所有 CID 集或查询的调制解调器和执行器的微型端口实例与之关联的; 对执行的请求颁发给 MBIM 函数同样，所有未经请求的通知发送从 MBIM 函数都适用于调制解调器和 MBIM 函数与之关联的执行程序。 同样，从微型端口实例发送的所有未经请求的设备服务事件都适用于调制解调器和 MBIM 函数与之关联的执行程序。 例如，从 MBIM 函数的未经请求的 MBIM_CID_REGISTER_STATE 或 MBIM_CID_PACKET_SERVICE 通知表示的关联调制解调器/执行程序的仅注册或数据包服务状态，它是无关的其他调制解调器状态或其他executor(s)。 

当有多个调制解调器和/或设备中的多个执行器与特定调制解调器相关的非特定于上下文的未经请求的通知和执行器组合应发出从 MBIM 函数与前面提到的调制解调器和执行器。 

在具有多个调制解调器和/或多个执行器的设备，与特定调制解调器和执行程序相关的非特定于上下文的 CID 查询请求可能会颁发给该调制解调器和执行器组合与关联的 MBIM 函数。 接收此类查询请求的函数应处理它根据 CID 定义。 如果因此可能会与任何其他并发处理的调制解调器的固件，此类查询请求的 CID 设置或与该调制解调器和执行器关联的任何 MBIM 函数正在处理查询请求。 与相同的调制解调器相关联的所有 MBIM 函数应都报告它们所表示的执行器除了该蜂窝调制解调器相同的状态信息。  

如果有多个调制解调器和/或设备中的多个执行器，非特定于执行器的 CID 集请求可能发出到与该调制解调器和执行器关联的 MBIM 函数。 调制解调器应跟踪的此类请求作为一个整体的进度。 如果一个此类集请求正在进行中的任何适配器，且尚未完成，第二个集 （对任何具有相同的调制解调器和执行器关联的适配器实例） 的请求尝试应进行排队和处理后已完成上一请求。

下图说明了在两个不同的调制解调器 WWANSVC 和 MBIM 函数之间的信息流。

![调制解调器具有 MBIM 功能结构](images/multi-SIM_10_MBIMspecification.png "调制解调器具有 MBIM 功能结构")

本部分包含定义的设备服务的详细的调制解调器范围和每个执行器 CID 说明。 返回到现有公共 MBIM1.0 规范定义引用。 MBIM 合规的设备实现，并报告以下设备服务 CID_MBIM_DEVICE_SERVICES 进行查询时。 10.1 一部分 USB NCM MBIM 1.0 规范中定义现有的已知服务。 Microsoft 扩展，以便定义以下服务。

服务名称 = **Basic 连接扩展**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID Value = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

为定义以下 Cid **UUID_MS_BasicConnect**:

| CID | 命令代码 | 最低 OS 版本 |
| --- | --- | --- |
| MBIM_CID_MS_SYS_CAPS | 5 | Windows 10 版本 1703 |
| MBIM_CID_MS_DEVICE_CAPS_V2 | 6 | Windows 10 版本 1703 |
| MBIM_CID_MS_DEVICE_SLOT_MAPPINGS | 7 | Windows 10 版本 1703 |
| MBIM_CID_MS_SLOT_INFO_STATUS | 8 | Windows 10 版本 1703 |

InformationBuffer MBIM_COMMAND_MSG 从头计算以下 CID 部分中的所有偏移量。

### <a name="mbimcidmssyscaps"></a>MBIM_CID_MS_SYS_CAPS

#### <a name="description"></a>描述

此 CID 检索有关调制解调器的信息。 这可以在任何 MB 实例公开为 USB 函数发送。

##### <a name="query"></a>查询

在 MBIM_COMMAND_MSG InformationBuffer MBIM_MS_SYS_CAPS_INFO 作为包含的响应数据。

##### <a name="set"></a>设置

不适用。

##### <a name="unsolicited-event"></a>未经请求的事件

不适用。

#### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | 不适用 | 不适用 |
| 响应 | 不适用 | MBIM_MS_SYS_CAPS_INFO | 不适用 |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

InformationBuffer 应为 null，并且 InformationBufferLength 应该为零。

##### <a name="set"></a>设置

不适用。

##### <a name="response"></a>响应

应在 InformationBuffer 中使用以下 MBIM_SYS_CAPS_INFO 结构。

| 偏移量 | 尺寸 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NumberOfExecutors | UINT32 | 报告该调制解调器的 MBB 实例数 |
| 4 | 4 | NumberOfSlots | UINT32 | 可在该调制解调器上的物理 UICC 槽数 |
| 8 | 4 | 并发 | UINT32 | MBB 可以同时处于活动状态的实例数 |
| 12 | 8 | ModemId | UINT64 | 每个调制解调器的唯一 64 位标识符 |

*NumberOfExecutors*字段表示数*执行器*受其当前配置中的调制解调器。 这直接映射到子电话堆栈调制解调器支持数。 

*NumberofSlots*字段表示的是实实在在存在调制解调器上的槽数。 报告每个插槽必须能够接收 UICC 卡 （槽本身可以是异类混合必要 – 微型 SIM，micro SIM 中，nano SIM 或 ETSI 由定义的任何标准）。 槽数量必须等于或大于支持的执行器数。 大于预配允许使用的非电话 UICC 这样的安全，NFC，等等。

*并发*字段表示同一时间可能会处于活动状态的执行器 （MBB 实例） 数。 其范围必须是*1 ≤ 并发 ≤ NumberOfExecutors*。 例如，双待机调制解调器将具有并发度为 1，而双活动调制解调器将具有 2 的并发

*ModemId*字段表示给定的调制解调器硬件的唯一 64 位标识符。 IHV 可以实现其自己的逻辑来生成每个调制解调器; 的唯一 64 位值例如，哈希的一个 IMEI 号码，随机生成 64 位数字，等等。后生成的 64 位 ID，它应在重新启动和 SIM 卡删除/插入操作中保持原样。

#### <a name="status-codes"></a>状态代码

此 CID 使用泛型状态代码 (请参阅使用的状态代码中的部分 9.4.5[公共标准，USB MBIM](https://go.microsoft.com/fwlink/p/?linkid=842064))。

### <a name="mbimcidmsdevicecapsv2"></a>MBIM_CID_MS_DEVICE_CAPS_V2

#### <a name="description"></a>描述

此 CID 检索与执行器相关的功能信息。 由于此 CID 是 MBIM_CID_DEVICE_CAPS 的扩展，此处介绍 MBIM_CID_DEVICE_CAPS 中的公共标准 USB MBIM 10.5.1 部分所述的更改。

此 CID 仍是仅限查询的将返回 MBIM_MS_DEVICE_CAPS_INFO_V2 MSUUID_BASIC_CONNECT 和 CID MBIM_CID_MS_DEVICE_CAPS_V2 响应与 MBIM MBIM_COMMAND_MSG 结构提供服务。

#### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | 不适用 | 不适用 |
| 响应 | 不适用 | MBIM_MS_DEVICE_CAPS_INFO_V2 | 不适用 |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

与公共 USB MBIM 标准 10.5.1.4 部分相同。

##### <a name="set"></a>设置

不适用。

##### <a name="response"></a>响应

应在 InformationBuffer 中使用以下 MBIM_DEVICE_CAPS_INFO_V2 结构。 与公共 USB MBIM 标准 10.5.1 节中定义的 MBIM_CID_DEVICE_CAPS 结构相比，以下结构有一个名为的新字段*DeviceIndex*。 除非另有说明，字段说明表 10-14 中的公共标准 USB MBIM 在此处适用。

| 偏移量 | 尺寸 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | DeviceType | MBIM_DEVICE_TYPE |  |
| 4 | 4 | CellularClass | MBIM_CELLULAR_CLASS |  |
| 8 | 4 | VoiceClass | MBIM_VOICE_CLASS |  |
| 12 | 4 | SimClass | MBIM_SIM_CLASS | MBIM 调制解调器支持此 CID，SimClass 将始终报告为 MBIMSimClassSimRemovable。 |
| 16 | 4 | DataClass | MBIM_DATA_CLASS |  |
| 20 | 4 | SmsCaps | MBIM_SMS_CAPS |  |
| 24 | 4 | ControlCaps | MBIM_CTRL_CAPS |  |
| 28 | 4 | MaxSessions | UINT32 |  |
| 32 | 4 | CustomDataClassOffset | 偏移量 |  |
| 36 | 4 | CustomDataClassSize | SIZE(0..22) |  |
| 40 | 4 | DeviceIdOffset | 偏移量 |  |
| 44 | 4 | DeviceIdSize | SIZE(0..26) |  |
| 48 | 4 | FirmwareInfoOffset | 偏移量 |  |
| 52 | 4 | FirmwareInfoSize | SIZE(0..60) |  |
| 56 | 4 | HardwareInfoOffset | 偏移量 |  |
| 60 | 4 | HardwareInfoSize | SIZE(0..60) |  |
| 64| 4 | ExecutorIndex | UINT32 | 执行器的索引。 它的范围介于*0*到*n-1*其中*n*是包含在 MBIM 调制解调器 MBB 实例数。 其值始终为常量，并独立于枚举顺序。 |
| 68 |  | DataBuffer | DATABUFFER | 包含的数据缓冲区*CustomDataClass*， *DeviceId*， *FirmwareInfo*，以及*HardwareInfo*成员。 |

#### <a name="status-codes"></a>状态代码

此 CID 使用泛型 （请参阅使用的状态代码的公共标准的 USB MBIM 9.4.5 部分中） 的状态代码。

### <a name="mbimcidmsdeviceslotmappings"></a>MBIM_CID_MS_DEVICE_SLOT_MAPPINGS

#### <a name="description"></a>描述

此 CID 设置或返回设备槽映射 （即执行器-slot 映射）。

##### <a name="query"></a>查询

不使用上 MBIM_COMMAND_MSG InformationBuffer。 MBIM_MS_DEVICE_SLOT_MAPPING_INFO MBIM_COMMAND_DONE InformationBuffer 中返回。

##### <a name="set"></a>设置

MBIM_COMMAND_MSG InformationBuffer 包含 MBIM_MS_DEVICE_SLOT_MAPPING_INFO。 MBIM_MS_DEVICE_SLOT_MAPPING_INFO MBIM_COMMAND_DONE InformationBuffer 中返回。 无论设置 CID 成功或失败，响应中包含 MBIM_MS_DEVICE_SLOT_MAPPING_INFO 表示当前的设备-slot 映射。

##### <a name="unsolicited-events"></a>未经请求的事件

不适用。

#### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | 不适用 | 不适用 |
| 响应 | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | 不适用 |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

InformationBuffer 应为 null，并且 InformationBufferLength 应该为零。

##### <a name="set"></a>设置

应在 InformationBuffer 中使用以下 MBIM_MS_DEVICE_SLOT_MAPPING_INFO 结构。

| 偏移量 | 尺寸 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MapCount (MC) | UINT32 | 数映射，也始终等于的设备/执行程序数量。 |
| 4 | 8 * MC | SlotMapList | OL_PAIR_LIST | *第 i 个*对此列表中，其中 (0 < = i < = (MC-1)) 记录的当前映射到的槽索引*第 i 个*设备/执行程序。 对中的第一个元素是与 DataBuffer，计算从 MBIM_MS_DEVICE_SLOT_MAPPINGS_INFO 此结构的开头 （偏移量为 0） 到 UINT32 中的偏移量的 4 字节字段。 该对的第二个元素是记录元素的一个 4 字节大小。 因为槽索引的类型为 UINT32，对中的第二个元素始终为 4。 |
| 4 + (8 * MC) | 4 * MC | DataBuffer | DATABUFFER | 包含的数据缓冲区*SlotMapList*。 由于槽的大小为 4 个字节，MC 相当于槽索引的数目，DataBuffer 的总大小为 4 * MC。 |

##### <a name="response"></a>响应

在组中使用 MBIM_MS_DEVICE_SLOT_MAPPING_INFO 还用于在 InformationBuffer 响应。

#### <a name="status-codes"></a>状态代码

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 操作失败，因为设备正忙。 在没有要清除这种情况的函数的任何显式信息的情况下，主机可用于后续操作由函数 （例如，通知或命令完成） 作为提示重试失败的操作。 |
| MBIM_STATUS_FAILURE | 操作失败 （一般性失败）。 |
| MBIM_STATUS_VOICE_CALL_IN_PROGRESS | 操作失败，因为正在进行语音呼叫。 |
| MBIM_STATUS_INVALID_PARAMETERS | 由于无效的参数 （例如槽号超出范围或映射中的重复的值） 操作失败。 |

### <a name="mbimcidmsslotinfostatus"></a>MBIM_CID_MS_SLOT_INFO_STATUS

#### <a name="description"></a>描述

此 CID 检索指定的 UICC 槽中，在其中 （如果有） 卡的高级聚合的状态。 它还可能用于一个槽的状态发生更改时提供的未经请求的通知。

##### <a name="query"></a>查询

MBIM_COMMAND_MSG InformationBuffer 包含 MBIM_MS_SLOT_INFO_REQ 结构。 MBIM_COMMAND_DONE 消息的 InformationBuffer 包含 MBIM_MS_SLOT_INFO 结构。

##### <a name="set"></a>设置

不适用。

##### <a name="unsolicited-events"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_MS_SLOT_INFO 结构。 该函数发送该事件的事件中复合槽/卡状态更改。

#### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | MBIM_MS_SLOT_INFO_REQ | 不适用 |
| 响应 | 不适用 | MBIM_MS_SLOT_INFO | MBIM_MS_SLOT_INFO |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

应在 InformationBuffer 中使用以下 MBIM_MS_SLOT_INFO_REQ 结构。

| 偏移量 | 尺寸 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SlotIndex | UINT32 | 要查询的槽的索引。 |

##### <a name="set"></a>设置

不适用。

##### <a name="response"></a>响应

应在 InformationBuffer 中使用以下 MBIM_MS_SLOT_INFO 结构。

| 偏移量 | 尺寸 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SlotIndex | UINT32 | 槽的索引。 |
| 4 | 4 | 状态 | MBIM_MS_UICC_SLOT_STATE | 此槽和数据卡 （如果适用） 的状态。 |

以下 MBIM_MS_UICCSLOT_STATE 结构描述槽的可能的状态。

| 状态 | 值 | 描述 |
| --- | --- | --- |
| UICCSlotStateUnknown | 0 | 调制解调器仍正在进行初始化以便 SIM 槽状态具有不确定性。 |
| UICCSlotStateOffEmpty | 1 | UICC 槽已关机，不则存在任何卡。 无法确定存在已关机的槽中的卡的实现作为 UICCSlotStateOff 报告其状态。 |
| UICCSlotStateOff | 2 | UICC 槽处于关闭状态。 |
| UICCSlotStateEmpty | 3 | UICC 槽为空 （在其中没有任何卡）。 |
| UICCSlotStateNotReady | 4 | 占用且已打开电源 UICC 槽，但尚未准备好在其中的卡。 |
| UICCSlotStateActive | 5 | UICC 槽已被占用，可以在其中的卡。 |
| UICCSlotStateError | 6 | 占用且已打开电源 UICC 槽但卡处于错误状态，直到下一步重置不能使用。 |
| UICCSlotStateActiveEsim | 7 | 在槽中的卡是活动配置文件与 esim 卡，并已准备好接受命令。 |
| UICCSlotStateActiveEsimNoProfiles | 8 | 在槽中的卡是 esim 卡与任何配置文件 （或没有活动的配置文件），并已准备好接受命令。 |

#### <a name="status-codes"></a>状态代码

此 CID 使用泛型 （请参阅使用的状态代码的公共标准的 USB MBIM 9.4.5 部分中） 的状态代码。

### <a name="non-ndis-mapping-of-per-executor-and-per-modem-mbim-cids"></a>每个执行器和每个调制解调器 MBIM Cid 非 NDIS 映射

大部分 MBIM Cid 映射或与 NDIS Oid，但有几个 Windows WMB 类驱动程序使用而没有 NDIS 对应的命令。  本部分提供有关这些命令的每个调制解调器或每个执行器的清晰度。  

| 每个设备或每个执行器 | CID 名称 |
| --- | --- |
| 每个设备 | CID_MBIM_MSEMERGENCYMODE |
|  | CID_MBIM_MSHOSTSHUTDOWN |
| 每个执行器 | CID_MBIM_MSIPADDRESSINFO |
|  | CID_MBIM_MSNETWORKIDLEHINT |
|  | CID_MBIM_MULTICARRIER_CURRENT_CID_LIST |

