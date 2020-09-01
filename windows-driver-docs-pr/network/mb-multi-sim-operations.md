---
title: MB 多 SIM 操作
description: MB 多 SIM 操作
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 200bcd941b851dfcfbd580ccd6d5fda85c44db42
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213957"
---
# <a name="mb-multi-sim-operations"></a>MB 多 SIM 操作

## <a name="desktop-multi-modem-multi-executor-support"></a>桌面多调制解调器多执行程序支持

传统上，尚未为多 SIM 调制解调器配置非电话 Windows 设备，因为它们的物理空间限制少于手机。 这样，他们就可以同时真正地利用多个活动的无线电设备，而不是使用一台具有多个 SIM 卡（如电话）的调制解调器;然而，由于在企业中的 eSIM 和方案增加，对非电话设备上的多 SIM 每个调制解调器支持的需求已增加。

大多数典型的多 SIM 电话设备具有双 SIM 插槽，但被限制为一个支持数据的主要 SIM 卡，而另一个则仅支持语音功能。 由于所有 SIM 卡都用于数据连接，因此不存在此类限制。

虽然在理论上定义的框架可以支持不限定数量的调制解调器和 SIM 卡，但 Windows 10 版本1703和更高版本仅支持双 SIM/单一活动方案端到端。 

## <a name="ndis-modem-interface-specification"></a>NDIS 调制解调器接口规范

### <a name="existing-interface-and-feature-gaps"></a>现有接口和功能间隙

可以通过多个独立的调制解调器支持双重 SIM/双重活动功能，其中每个调制解调器都是单独的设备，并完全独立运行。 但是，这不在此文档的范围内，而是侧重于一个可向主机提供多个和同时连接堆栈的 WWAN 微型端口调制解调器。 本节定义各种对象，并建立与多 SIM 功能相关的所有 MB 文档中使用的术语。

硬件上的改进导致设备能够同时维护多个手机网络的注册。 在此类设备中，假设是并行运行的 "多个移动电话堆栈实例"，每个实例都可以维护注册、监视信号强度、执行 handovers 和侦听传入页面。 此 "蜂窝堆栈" 的每个实例将被称为本文档其余部分的 *执行* 程序。 例如，在能够同时维护两个网络的注册的设备中，调制解调器硬件被视为具有两个执行器。

执行器是硬件的逻辑表示形式，实际上，它可能是一个多路复用的单个硬件收发器。 确切的硬件细节被视为供应商实现细节，并超出了本规范的范围。 对于 NDIS 微型端口驱动程序，执行器作为 WWAN 微型端口适配器的多个实例公开。 对于 MBIM 调制解调器，执行器由枚举复合设备上的多个 MBIM 函数表示。

以下两个图像说明了双 SIM 调制解调器的逻辑视图。 每个都显示了执行器和 UICC 的可能组合。

![双 SIM 调制解调器的逻辑视图](images/multi-SIM_1_dualSimModem.png "双 SIM 调制解调器的逻辑视图")

执行器中的移动电话堆栈主要被视为自包含，只不过在双重备用调制解调器实现的情况下，执行器会将流量 (语音和/或数据) 阻止其他方维护注册。

下图说明了双重备用调制解调器的逻辑视图。 执行器0上的流量（电话呼叫）将导致执行程序1失去注册。

![双备用调制解调器的逻辑视图](images/multi-SIM_2_dualExecutors.png "双备用调制解调器的逻辑视图")

NDIS 6.7 中的 Windows 桌面调制解调器接口模型不能容纳此类体系结构，因为它基于若干隐式假设：

* 该模型假定调制解调器内有一个执行器。
* 该模型假定只有一个 UICC 卡与调制解调器硬件直接关联。
* UICC 被视为单个应用程序 SIM 卡。

与此相反，Windows Mobile 上 (RIL) 接口的 Microsoft 无线接口层显式公开了这些假设的重数。 Windows Mobile 中的移动宽带接口公开通过单独的微型端口进行注册的功能，并假定已通过 RIL 接口完成了设备的某些基本配置。 若要提供等效的功能，Windows Desktop 必须提供机制来发现执行器和槽的数量，单独访问执行器，定义执行器与槽之间的映射，并定义每个执行器将使用的映射 UICC 卡中的应用程序。

有关手机结构的详细信息以及 Windows 10 移动版和桌面版之间的差异，请参阅 [移动设备体系结构和实施](cellular-architecture-and-driver-model.md)。

### <a name="major-objects-and-operations"></a>主要对象和操作

下图显示了调制解调器的抽象模型。

![调制解调器、执行器和槽之间的关系](images/multi-SIM_3_majorObjectsAndOperations.png "调制解调器、执行器和槽之间的关系")

每个调制解调器都由全局唯一标识符 (GUID) 标识，其中包含一个或多个执行器的集，其中每个执行程序都可以独立注册到蜂窝网络。 每个执行器都有一个关联的执行器索引，一个整数，从0开始，为第一个执行器。 此外，该调制解调器还公开了一个或多个可能包含 UICC 卡的插槽。 假定槽的数目大于或等于执行器的数目。 每个槽都具有关联的索引（从0开始）以及与槽中的卡的电源状态相关的当前状态， (如果有任何) ，则为槽的可用性状态。

为了保持与现有调制解调器的兼容性，每个执行程序都使用 UICC 卡在单个插槽中提供的信息来运行。 执行器和槽之间的关联由槽映射定义，后者将每个执行器映射到恰好一个槽。

槽可能包含 UICC 卡;每个卡都包含一个或多个 UICC 应用程序（例如 USIM、CSIM、ISIM），或可能是其他电话和非电话应用程序，如 PKCS # 15 或适用于 NFC 安全元素的全局平台应用程序。 这些单独的 UICC 应用程序的寻址和使用是一种用于未来规范的主题，并超出了本文档的范围。

到调制解调器的 Windows 桌面 NDIS 接口的特征在于 Oid 和 NDIS 通知的交换。 在大多数情况下，这些 Oid 定向到各个执行器;但是，有几个命令和通知的作用域限定为调制解调器。

对于非 Windows Mobile 操作系统，多执行程序的调制解调器显示为一个具有多个物理 WWAN 小型端口实例的设备。 每个物理微型端口实例都表示一个执行程序，该执行器可将注册作为 NDIS 实例进行维护。 可以在运行时创建其他虚拟实例来管理特定于上下文的数据包数据和设备服务会话。 执行器特定的命令和通知通过表示该执行器的 WWAN 微型端口 NDIS 物理实例进行交换。 换句话说，特定于调制解调器的命令 (，而不是特定于执行程序的) 及其相应的通知可以发送到或来自任何物理微型端口实例。

以下两个关系图显示了第一个关系图)  (第一个关系图中的执行器特定命令和通知的不同之处，其中的命令和通知将在第二个关系图)  (，其中，命令可通过任何执行器并来自任何执行器。

![执行器特定的命令和通知](images/multi-SIM_4_executorSpecificCommands.png "执行器特定的命令和通知")

![调制解调器特定的命令和通知](images/multi-SIM_4_modemSpecificCommands.png "调制解调器特定的命令和通知")

将对与微型端口实例关联的调制解调器和执行程序执行发出到微型端口实例的所有 OID 集或查询请求。 同样，从微型端口实例发送的所有未经请求的通知和未请求的设备服务事件都适用于与该小型应用程序实例关联的调制解调器和执行程序。 例如，来自微型端口的未经请求的 NDIS_STATUS_WWAN_REGISTER_STATE 或 NDIS_STATUS_WWAN_PACKET_SERVICE 通知指示关联的调制解调器和执行器的注册 (或数据包服务状态) ，并且与其他调制解调器 () 或其他执行器 (的状态无关。 

如果设备中有多个调制解调器和/或多个执行程序，则与该调制解调器和执行器组合关联的物理微型端口适配器将发出与特定调制解调器和执行器组合相关的非特定于上下文的未经请求的通知。 

同样，如果设备有多个调制解调器和/或多个执行程序，则与特定调制解调器和执行器组合关联的物理微型端口适配器实例可以接收与该调制解调器和执行器相关的非特定于上下文的 OID 查询请求。 接收此类查询请求的适配器根据 OID 定义处理该请求。 如果使用微型端口驱动程序选择此项，则此查询请求可以与该调制解调器和执行器关联的任何适配器实例中的任何其他进程内 OID 集或查询请求同时进行处理。 与同一调制解调器和执行器关联的微型端口适配器的所有实例都会报告该移动电话调制解调器和执行器的相同状态信息 (如无线电电源状态、注册状态、数据包服务状态等 ) 。  

对于具有多个调制解调器和/或多个执行器的设备，与调制解调器和执行器组合关联的物理微型端口适配器实例可以接收非特定于上下文的 OID 集请求。 微型端口驱动程序应跟踪此类请求的进度。 如果在任何适配器中有一个此类设置请求正在进行，并且尚未完成，则第二个此类设置请求尝试 (到与同一调制解调器关联的任何适配器实例，) 并在上一个请求完成后处理。 

Windows 10 desktop WMBCLASS 驱动程序遵循上一段中所述的规范来处理此设置请求争用条件，但是，如果在调制解调器层发生争用条件，则调制解调器应遵循相同的指南来对 MBIM 函数上的冲突设备范围内的命令进行排队（如果它仍在处理链接到同一基础设备的另一个函数）。

## <a name="oids-for-set-and-query-requests"></a>Set 和 Query 请求的 Oid

若要查询调制解调器中 (执行器) 和槽的设备数，以及可以同时处于活动状态的执行器的数目，主机使用 [OID_WWAN_SYS_CAPS](https://go.microsoft.com/fwlink/p/?linkid=841265)。

为了查询执行器的功能，主机使用 [OID_WWAN_DEVICE_CAPS_EX](https://go.microsoft.com/fwlink/p/?linkid=841266)。

若要定义绑定到每个执行器或查询当前映射的槽，主机使用 [OID_WWAN_DEVICE_SLOT_MAPPINGS](https://go.microsoft.com/fwlink/p/?linkid=841267)。

若要在调制解调器上查询特定插槽的状态，主机使用 [OID_WWAN_SLOT_INFO_STATUS](https://go.microsoft.com/fwlink/p/?linkid=841268)。

## <a name="per-device-and-per-executor-commands"></a>每个设备和每个执行器命令

在 Windows 10 版本1703及更高版本中，将执行器概念添加到非 Windows 移动设备后，Oid 现在分为两类：按设备 Oid 和按执行器 Oid。 下表说明哪些 Oid 属于哪个类别。

| 每设备或按执行器| OID 名称 |
| --- | --- |
| 每设备| OID_WWAN_DRIVER_CAPS |
|  | OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS |
|  | OID_WWAN_ENUMERATE_DEVICE_SERVICES |
|  | OID_WWAN_PRESHUTDOWN |
|  | OID_WWAN_VENDOR_SPECIFIC |
|  | OID_WWAN_SYS_CAPS |
|  | OID_WWAN_DEVICE_SLOT_MAPPINGS |
| 按执行程序 | OID_WWAN_AUTH_CHALLENGE |
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
> Windows 10 版本1703也已更新[OID_WWAN_RADIO_STATE](./oid-wwan-radio-state.md) 。 有关详细信息，请参阅 OID_WWAN_RADIO_STATE。

## <a name="mbim-interface-update-for-multi-sim-operations"></a>多 SIM 操作的 MBIM 接口更新

对于非 Windows Mobile 操作系统，多执行程序的调制解调器显示为具有多个 MBIM 函数的一个 USB 复合设备。 每个 MBIM 函数都表示一个可以维护注册的执行器。 执行特定于执行程序的命令和通知通过表示该执行器的 MBIM 函数进行交换，而特定于调制解调器的命令 (换言之，那些不是特定于执行程序的) 及其相应的通知可以发送到或来自属于同一基础 USB 复合设备的任何 MBIM 函数。 

向 MBIM 函数发出的所有 CID 集或查询请求均针对与该微型端口实例关联的调制解调器和执行器执行;同样，通过 MBIM 函数发送的所有未经请求的通知都适用于与 MBIM 函数关联的调制解调器和执行程序。 同样，从微型端口实例发送的所有未请求的设备服务事件都适用于与 MBIM 函数关联的调制解调器和执行程序。 例如，未经请求的 MBIM_CID_REGISTER_STATE 或来自 MBIM 函数的 MBIM_CID_PACKET_SERVICE 通知仅指示关联的调制解调器/执行器的注册或数据包服务状态，并且与其他调制解调器 () 或其他执行器 () 的状态无关。 

如果设备中有多个调制解调器和/或多个执行程序，则应从与上述调制解调器和执行器关联的 MBIM 函数发出与特定调制解调器和执行器组合相关的非特定于上下文的未经请求的通知。 

在具有多个调制解调器和/或多个执行器的设备中，与特定调制解调器相关的非特定于上下文的 CID 查询请求和执行器可能会颁发给与该调制解调器和执行器组合关联的 MBIM 函数。 接收此类查询请求的函数应根据 CID 定义进行处理。 如果调制解调器固件选择了此类连接，则可能会与任何其他 CID 集或与该调制解调器和执行器关联的任何 MBIM 函数正在处理的查询请求同时处理此类查询请求。 除了所表示的执行器外，与同一调制解调器关联的所有 MBIM 函数应报告该移动电话调制解调器的相同状态信息。  

如果设备中有多个调制解调器和/或多个执行程序，则可能会向与该调制解调器和执行器关联的 MBIM 函数发出非执行程序特定的 CID 集请求。 调制解调器应始终跟踪此类请求的进度。 如果在任何适配器中有一个此类设置请求正在进行，并且尚未完成，则第二个这样的 set 请求尝试 (到与同一调制解调器关联的任何适配器实例，并且执行器) 应在之前的请求完成后进行排队和处理。

下图说明了两个不同的调制解调器中的 WWANSVC 和 MBIM 函数之间的信息流。

![包含 MBIM 函数的调制解调器结构](images/multi-SIM_10_MBIMspecification.png "包含 MBIM 函数的调制解调器结构")

本部分包含定义的设备服务的详细的调制解调器范围和每个执行器 CID CID 说明。 定义引用现有公有 MBIM 1.0 规范。 与 MBIM 兼容的设备在 CID_MBIM_DEVICE_SERVICES 进行查询时实现并报告以下设备服务。 在 USB NCM MBIM 1.0 规范的第10.1 节中定义了现有的已知服务。 Microsoft 对此进行了扩展，定义了以下服务。

服务名称 = **基本连接扩展**

UUID = **UUID_BASIC_CONNECT_EXTENSIONS**

UUID 值 = **3d01dcc5-fef5-4d05-0d3abef7058e9aaf**

以下 Cid 是为 **UUID_MS_BasicConnect**定义的：

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_MS_SYS_CAPS | 5 | Windows 10 版本 1703 |
| MBIM_CID_MS_DEVICE_CAPS_V2 | 6 | Windows 10 版本 1703 |
| MBIM_CID_MS_DEVICE_SLOT_MAPPINGS | 7 | Windows 10 版本 1703 |
| MBIM_CID_MS_SLOT_INFO_STATUS | 8 | Windows 10 版本 1703 |

以下 CID 部分中的所有偏移均从 InformationBuffer MBIM_COMMAND_MSG 的开头进行计算。

### <a name="mbim_cid_ms_sys_caps"></a>MBIM_CID_MS_SYS_CAPS

#### <a name="description"></a>说明

此 CID 检索有关调制解调器的信息。 这可以在作为 USB 函数公开的任何 MB 实例上发送。

##### <a name="query"></a>查询

MBIM_COMMAND_MSG 上的 InformationBuffer 包含 MBIM_MS_SYS_CAPS_INFO 的响应数据。

##### <a name="set"></a>设置

不适用。

##### <a name="unsolicited-event"></a>主动事件

不适用。

#### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | 不适用 | 不适用 |
| 响应 | 不适用 | MBIM_MS_SYS_CAPS_INFO | 不适用 |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

InformationBuffer 应为 null，而 InformationBufferLength 应为零。

##### <a name="set"></a>设置

不适用。

##### <a name="response"></a>响应

以下 MBIM_SYS_CAPS_INFO 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | NumberOfExecutors | UINT32 | 此调制解调器报告的 MBB 实例数 |
| 4 | 4 | NumberOfSlots | UINT32 | 此调制解调器上可用的物理 UICC 槽数 |
| 8 | 4 | 并发 | UINT32 | 可以同时处于活动状态的 MBB 实例的数目 |
| 12 | 8 | ModemId | UINT64 | 每个调制解调器唯一的64位标识符 |

*NumberOfExecutors*字段表示调制解调器在其当前配置中*支持的执行*器的数目。 这会直接映射到调制解调器支持的 "子电话" 堆栈数。 

*NumberofSlots*字段表示在调制解调器上物理存在的槽数。 报告的每个插槽都必须能够接收 UICC 卡 (插槽本身可以是一种异类混合，如需要，还可以使用 ETSI) 定义的小型 SIM、微 SIM、nano SIM 或任何标准。 槽数必须等于或大于支持的执行器数量。 "大于" 预配允许使用非电话 UICC，例如用于安全性、NFC 等。

*并发*字段表示可以同时处于活动状态的执行器 (MBB 实例数) 。 它必须为 *1 ≤ Concurrency ≤ NumberOfExecutors*。 例如，双备用调制解调器的并发性为1，而双主动调制解调器的并发性为2

*ModemId*字段表示给定调制解调器硬件的唯一64位标识符。 IHV 可以实现自己的逻辑，为每个调制解调器生成唯一的64位值;例如，对其中一个 IMEI 号码进行哈希处理，随机生成64位数字等。生成64位 ID 后，它应在重新启动和 SIM 卡删除/插入之间保持不变。

#### <a name="status-codes"></a>状态代码

此 CID 使用一般状态代码 (参阅 [公共 USB MBIM standard](https://go.microsoft.com/fwlink/p/?linkid=842064)) 的9.4.5 节中的状态代码的使用。

### <a name="mbim_cid_ms_device_caps_v2"></a>MBIM_CID_MS_DEVICE_CAPS_V2

#### <a name="description"></a>说明

此 CID 检索与执行器相关的功能信息。 由于此 CID 是 MBIM_CID_DEVICE_CAPS 的扩展，因此此处仅介绍 MBIM_CID_DEVICE_CAPS 公用 USB MBIM 标准的10.5.1 部分中所述的更改。

此 CID 继续作为查询，并将返回 MBIM_MS_DEVICE_CAPS_INFO_V2 结构，以响应与 MBIM 服务 MSUUID_BASIC_CONNECT 和 CID MBIM_CID_MS_DEVICE_CAPS_V2 MBIM_COMMAND_MSG。

#### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | 不适用 | 不适用 |
| 响应 | 不适用 | MBIM_MS_DEVICE_CAPS_INFO_V2 | 不适用 |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

与公共 USB MBIM 标准的10.5.1.4 节相同。

##### <a name="set"></a>设置

不适用。

##### <a name="response"></a>响应

以下 MBIM_DEVICE_CAPS_INFO_V2 结构应在 InformationBuffer 中使用。 与公共 USB MBIM standard 的10.5.1 部分中定义的 MBIM_CID_DEVICE_CAPS 结构相比，以下结构包含名为 *DeviceIndex*的新字段。 除非在此处说明，否则此处将应用公共 USB MBIM standard 的表10-14 中的字段说明。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | DeviceType | MBIM_DEVICE_TYPE |  |
| 4 | 4 | CellularClass | MBIM_CELLULAR_CLASS |  |
| 8 | 4 | VoiceClass | MBIM_VOICE_CLASS |  |
| 12 | 4 | SimClass | MBIM_SIM_CLASS | 对于支持此 CID 的 MBIM 调制解调器，SimClass 将始终报告为 MBIMSimClassSimRemovable。 |
| 16 | 4 | Microsoft.visualstudio.ordesigner.dataclass. | MBIM_DATA_CLASS |  |
| 20 | 4 | SmsCaps | MBIM_SMS_CAPS |  |
| 24 | 4 | ControlCaps | MBIM_CTRL_CAPS |  |
| 28 | 4 | MaxSessions | UINT32 |  |
| 32 | 4 | CustomDataClassOffset | OFFSET |  |
| 36 | 4 | CustomDataClassSize | 大小 (0 ... 22)  |  |
| 40 | 4 | DeviceIdOffset | OFFSET |  |
| 44 | 4 | DeviceIdSize | 大小 (0. 26)  |  |
| 48 | 4 | FirmwareInfoOffset | OFFSET |  |
| 52 | 4 | FirmwareInfoSize | 大小 (0)  |  |
| 56 | 4 | HardwareInfoOffset | OFFSET |  |
| 60 | 4 | HardwareInfoSize | 大小 (0)  |  |
| 64| 4 | ExecutorIndex | UINT32 | 执行器索引。 它的范围为 *0* 到 *n-1* ，其中 *n* 是 MBIM 调制解调器中包含的 MBB 实例的数目。 它的值始终保持不变，并且与枚举顺序无关。 |
| 68 |  | DataBuffer | DATABUFFER | 包含 *CustomDataClass*、 *DeviceId*、 *FirmwareInfo*和 *HardwareInfo* 成员的数据缓冲区。 |

#### <a name="status-codes"></a>状态代码

此 CID 使用一般状态代码 (参阅公共 USB MBIM standard) 的9.4.5 节中的状态代码的使用。

### <a name="mbim_cid_ms_device_slot_mappings"></a>MBIM_CID_MS_DEVICE_SLOT_MAPPINGS

#### <a name="description"></a>说明

此 CID 设置或返回设备槽映射 (换言之，即执行器槽映射) 。

##### <a name="query"></a>查询

不使用 MBIM_COMMAND_MSG 上的 InformationBuffer。 MBIM_MS_DEVICE_SLOT_MAPPING_INFO 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

##### <a name="set"></a>设置

MBIM_COMMAND_MSG 的 InformationBuffer 包含 MBIM_MS_DEVICE_SLOT_MAPPING_INFO。 MBIM_MS_DEVICE_SLOT_MAPPING_INFO 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。 不管集 CID 是成功还是失败，响应中包含的 MBIM_MS_DEVICE_SLOT_MAPPING_INFO 都表示当前的设备槽映射。

##### <a name="unsolicited-events"></a>未经请求的事件

不适用。

#### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | 不适用 | 不适用 |
| 响应 | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | MBIM_MS_DEVICE_SLOT_MAPPING_INFO | 不适用 |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

InformationBuffer 应为 null，而 InformationBufferLength 应为零。

##### <a name="set"></a>设置

以下 MBIM_MS_DEVICE_SLOT_MAPPING_INFO 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MapCount (MC)  | UINT32 | 映射的数量，始终等于设备/执行器的数目。 |
| 4 | 8 * MC | SlotMapList | OL_PAIR_LIST | 此列表的 *第 i* 对，其中 (0 <= i <= (MC-1) # A5 记录当前映射到 *i 个* 设备/执行器的槽的索引。 该对中的第一个元素是一个4字节字段，其偏移量为 DataBuffer 的偏移量，计算方式为从此 MBIM_MS_DEVICE_SLOT_MAPPINGS_INFO 结构的开始 (偏移量 0) 到 UINT32。 对的第二个元素是 record 元素的4字节大小。 由于槽索引的类型为 UINT32，因此对中的第二个元素始终为4。 |
| 4 + (8 * MC)  | 4 * MC | DataBuffer | DATABUFFER | 包含 *SlotMapList*的数据缓冲区。 由于槽的大小为4个字节，并且 MC 等于槽索引的数目，因此 DataBuffer 的总大小为 4 * MC。 |

##### <a name="response"></a>响应

InformationBuffer 中使用的 MBIM_MS_DEVICE_SLOT_MAPPING_INFO 也用于响应。

#### <a name="status-codes"></a>状态代码

| 状态代码 | 说明 |
| --- | --- |
| MBIM_STATUS_BUSY | 操作失败，因为设备正忙。 如果没有来自函数的任何显式信息来清除此条件，则宿主可以通过函数使用后续操作 (例如，通知或命令完成) 作为重试失败的操作的提示。 |
| MBIM_STATUS_FAILURE |  (一般故障) ，操作失败。 |
| MBIM_STATUS_VOICE_CALL_IN_PROGRESS | 操作失败，因为正在进行语音呼叫。 |
| MBIM_STATUS_INVALID_PARAMETERS | 由于参数无效 (例如槽号超出范围或映射) 中的重复值，因此操作失败。 |

### <a name="mbim_cid_ms_slot_info_status"></a>MBIM_CID_MS_SLOT_INFO_STATUS

#### <a name="description"></a>说明

此 CID 检索指定 UICC 槽的高级聚合状态，并 (如果任何) ，则它。 当某个槽的状态发生更改时，也可以使用它来传递未经请求的通知。

##### <a name="query"></a>查询

MBIM_COMMAND_MSG 的 InformationBuffer 包含 MBIM_MS_SLOT_INFO_REQ 的结构。 MBIM_COMMAND_DONE 消息的 InformationBuffer 包含 MBIM_MS_SLOT_INFO 的结构。

##### <a name="set"></a>设置

不适用。

##### <a name="unsolicited-events"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_MS_SLOT_INFO 结构。 如果复合槽/卡片状态发生变化，则函数将发送此事件。

#### <a name="parameters"></a>参数

| 操作 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | MBIM_MS_SLOT_INFO_REQ | 不适用 |
| 响应 | 不适用 | MBIM_MS_SLOT_INFO | MBIM_MS_SLOT_INFO |

#### <a name="data-structures"></a>数据结构

##### <a name="query"></a>查询

以下 MBIM_MS_SLOT_INFO_REQ 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SlotIndex | UINT32 | 要查询的槽的索引。 |

##### <a name="set"></a>设置

不适用。

##### <a name="response"></a>响应

以下 MBIM_MS_SLOT_INFO 结构应在 InformationBuffer 中使用。

| Offset | 大小 | 字段 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SlotIndex | UINT32 | 槽的索引。 |
| 4 | 4 | 状态 | MBIM_MS_UICC_SLOT_STATE | 槽和卡的状态 (（如果适用）) 。 |

以下 MBIM_MS_UICCSLOT_STATE 结构描述了槽的可能状态。

| 状态 | 值 | 说明 |
| --- | --- | --- |
| UICCSlotStateUnknown | 0 | 调制解调器仍处于初始化过程中，因此 SIM 插槽状态不是确定性的。 |
| UICCSlotStateOffEmpty | 1 | UICC 槽已关闭并且无卡。 无法确定已关闭的插槽中是否存在卡的实现将其状态报告为 UICCSlotStateOff。 |
| UICCSlotStateOff | 2 | UICC 槽已关机。 |
| UICCSlotStateEmpty | 3 | UICC 槽为空 (没有卡) 中。 |
| UICCSlotStateNotReady | 4 | UICC 槽已占用并已打开，但其中的卡尚未就绪。 |
| UICCSlotStateActive | 5 | UICC 槽已被占用，其中卡已准备就绪。 |
| UICCSlotStateError | 6 | UICC 槽已占用并已打开，但该卡处于错误状态，因此在下一次重置之前无法使用。 |
| UICCSlotStateActiveEsim | 7 | 槽中的卡是一个具有活动配置文件的 eSIM 卡，并已准备好接受命令。 |
| UICCSlotStateActiveEsimNoProfiles | 8 | 槽中的卡是不含任何配置文件的 eSIM 卡 (或没有活动的配置文件) 并且已准备好接受命令。 |

##### <a name="mbim_ms_uiccslot_state-transition-guidance-for-multi-sim-devices"></a>多 sim 设备的 MBIM_MS_UICCSLOT_STATE 转换指南

符合正确的 UICC 槽状态转换可确保 OS 正确处理所有更改并向用户显示正确的 toast 通知。

对于 *插入* 的 toast 通知，操作系统需要选择嵌入的槽 (SIM2/插槽 1) ，并在物理槽 (SIM1/插槽 0) 中将 SIM 插入时出现以下状态转换。

| SIM 插入前插槽0的可能值 | SIM 插入后插槽0的可能值 |
| --- | --- |
| UICCSlotStateEmpty | UICCSlotStateActive |
| UICCSlotStateOffEmpty | <ul><li>UICCSlotStateActiveEsim</li><li>UICCSlotStateActiveEsimNoProfile</li></ul> |

对于删除了 toast 通知的 *sim* ，操作系统需要在插入 SIM (SIM1/插槽 0) 的物理槽，并在从物理槽 (SIM1/插槽 0) 删除 sim 后发生以下状态转换。

| 删除 SIM 之前插槽0的可能值 | 删除 SIM 后插槽0的可能值 |
| --- | --- |
| UICCSlotStateActive | UICCSlotStateEmpty |
| <ul><li>UICCSlotStateActiveEsim</li><li>UICCSlotStateActiveEsimNoProfile</li></ul> | UICCSlotStateOffEmpty |

#### <a name="status-codes"></a>状态代码

此 CID 使用一般状态代码 (参阅公共 USB MBIM standard) 的9.4.5 节中的状态代码的使用。

### <a name="non-ndis-mapping-of-per-executor-and-per-modem-mbim-cids"></a>每个执行器和每个调制解调器 MBIM Cid 的非 NDIS 映射

大多数 MBIM Cid 映射或与 NDIS Oid 相关，但 Windows WMB 类驱动程序使用的一些命令没有 NDIS 对应项。  本部分清楚地说明这些命令是每个调制解调器还是按执行器。  

| 每设备或按执行器 | CID 名称 |
| --- | --- |
| 每设备 | CID_MBIM_MSEMERGENCYMODE |
|  | CID_MBIM_MSHOSTSHUTDOWN |
| 按执行程序 | CID_MBIM_MSIPADDRESSINFO |
|  | CID_MBIM_MSNETWORKIDLEHINT |
|  | CID_MBIM_MULTICARRIER_CURRENT_CID_LIST |