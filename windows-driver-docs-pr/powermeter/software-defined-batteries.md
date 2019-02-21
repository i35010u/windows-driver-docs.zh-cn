---
title: 软件定义的电池
description: 软件定义的电池
keywords:
- 软件定义的电池
- SDB
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 527c7f1488a855300c65a14951b9a120a27a760a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523755"
---
# <a name="software-defined-battery"></a>软件定义的电池

>[!NOTE]
> 在商业发行之前会发生实质性修改的、与预发布产品相关的一些信息。 Microsoft 不对此处提供的信息作任何明示或默示的担保。

## <a name="introduction"></a>简介

本主题旨在介绍软件定义电池 (SDB)、 描述 Windows SDB 体系结构和详细信息的 Windows API 和 DDI 约定对于此功能。 

本主题首先会引入假设两个电池系统的简单年龄平衡 SDB 算法。 这一切后跟体系结构实现的 SDB 算法时所需的布局和 API 协定。

## <a name="nomenclature"></a>命名法

- BattC-电池类驱动程序

- CAD-费用仲裁驱动程序 (CAD) 是调整 power USB 旧版、 USB 类型 C 和无线充电源之间的 Microsoft 驱动程序

- 冷可交换的电池不能从会限电或总电源故障导致系统中删除的电池

- 周期计数-ACPI 规范中所述的电池，进行了完整的费用放电周期数

- 热更换电池的系统在操作中，而不用担心限电时可以安全删除的电池

- HPMI-硬件电源管理器接口

- 非热插拔电池的一个或多个冷可交换，在系统中安装的非 Swappable 电池

- 非可更换电池的电池不设计的、 用于删除由最终用户

## <a name="sdb-overview"></a>SDB 概述
在软件定义电池 MSR 研究论文可在此处找到： [ https://www.microsoft.com/research/wp-content/uploads/2016/02/multibattery_sosp2015.pdf ](https://www.microsoft.com/research/wp-content/uploads/2016/02/multibattery_sosp2015.pdf)。 

本主题技术性选择在本白皮书中所述的想法并提供继续基于软件电池年龄平衡便携式计算机中的新功能和其他移动设备的视图。 

设想有两个电池系统。 其中一个电池是非可移动电池，恰好位于旁边 SOC – 我们称之为*内部电池*。 其他电池是热插拔电池，恰好位于旁边可移动键盘 – 我们称之为*外部电池*。 

*多电池系统*

![显示内部和外部电池多电池系统](images/powermeter-multi-battery.png)

由于键盘一段时间内是附加分离，它会以不同的方式强制到年龄两个电池。 这将创建对应： 年龄平衡电池和采用平衡算法的 SDB 简单期限延长系统可用性时间范围。

## <a name="simple-age-balancing-sdb-algorithm"></a>简单年龄平衡 SDB 算法

该算法称为*简单年龄平衡*因为它会尝试均衡电池年龄。 简单的年龄平衡算法会导致系统更喜欢具有过期的最小电池放电。 电池已产生较小的周期计数不仅具有更高的容量来保存电源，但通常更高效中提供。 从而因而增加了系统可以承受电池的时间。

*简单年龄平衡 SDB 算法*

![简单年龄平衡 SDB 算法](images/powermeter-simple-age-balancing-algorithm.png)

简单的年龄平衡算法的核心理念是只需使用电池已产生最小电池周期计数，如下图所示的决策框 （2） 在上述流程图中。 在此示例中，假设系统允许独占使用的内部或外部的电池。 但是，这可能不是所有的系统，则返回 true。 其他系统可能不灵活，或者可能已在使用电池电源约束。 在这种情况下该算法需要年龄平衡的最佳尝试。 例如，考虑以下。  

1. 系统无法承受以独占方式打开外部 （可能是因为外部电池旨在作为只补充电源） 的电池电源。 此系统可能会实现简单的保留时间的同时放电同时上述流程图中的 process 块 (A) 中的内部和外部电池平衡算法。

2. 只要存在使用要求外部电池的系统 （可能是由于与保持通电可移动键盘关联的其他电源抽签排位）：此系统可能会实现简单的保留时间的同时放电同时上述流程图中的 process 块 (B) 中的内部和外部电池平衡算法。

可能会使简单年龄平衡算法仅在内部和外部电池来运行系统，决策框 （1） 描述了上述流程图中的此条件检查中存在足够收费时要使用。 例如 （再次转到假设的系统） 外部电池中不包含不收取任何费用，如果没有平衡电池的期限无作用域和决策框 （1） 将产生"NO"分支中。

OEM 可以自由地平衡算法的简单期限不会放入的效果，除了时内部或外部的电池电量用尽时选择的约束和条件。 例如，OEM 可以选择不执行任何年龄段平衡时：

1.  在高性能模式下运行 SOC/处理器
2.  系统不稳定散热

当平衡算法的简单期限不 （由于前面所述的一个或多个条件） 放在使用中时，逻辑将恢复为 OEM 的专有的电池使用情况策略如下图所示的进程框 （3） 在上述流程图中。 进程框 （3） 是将具有 OEM 使生效，如果不支持 SDB 的逻辑。


## <a name="span-idadapting-sdbspanspan-idadapting-sdbspanadapting-sdb-algorithm-for-use-with-hot-swappable-batteries"></a><span id="adapting-sdb"></span><span id="ADAPTING-SDB"></span>热更换电池用于调整 SDB 算法

简单年龄平衡 SDB 算法将尝试使用电池，尽管此策略的工作原理是 healthiest，以提高长期电池寿命，它可能会严重影响系统的短时间内可用性在以下方案中所述。

在上述两个电池系统中，请考虑以下情况：

1.  用户应使用系统足够长的时间，直到在内部和外部的电池电量用尽。

2.  外部电池已过期多相比内部电池。

此系统上执行简单的年龄平衡算法时它将尝试以耗尽电量首先存储在内部电池 （根据条件 #1 和上面列出的 #2）。 当用户决定分离后一段时间，其可能会导致不良用户体验可供使用的电池容量将会大大降低一次外部电池因为外部电池被分离，因为内部电池会用完。

在非 SDB 系统中，此通常不会出现问题，因为内部电池将使用之前在大多数情况下耗尽外部电池。

因此想要有选择性地禁用上述方案时负载平衡算法很可能发生这种情况的简单期限。 

总而言之，每当用户预期需要与外部电池中删除了长时间使用系统时，它是将禁用 SDB 算法并恢复为使用 OEM 电池使用情况策略 （这通常倾向于先使用外部电池） 最佳选择。

Windows 计算电池可用性，并生成"保留非热的可交换电池"提示。 当此提示使用 SDB 算法，如下图所示以下数据流关系图中的决策框 (X)。

*平衡改写，以便进行热插拔电池的 SDB 算法的简单年龄*

![平衡改写，以便进行热插拔电池的 SDB 算法的简单年龄](images/powermeter-simple-age-balancing-algorithm-hot-swap.png)


## <a name="span-idimplementing-sdbspanspan-idimplementing-sdbspanimplementing-sdb-algorithm-in-firmware"></a><span id="implementing-sdb"></span><span id="IMPLEMENTING-SDB"></span>在固件中实现 SDB 算法

本部分描述了系统固件中实现的电池放电装置控制逻辑。 这会生成电池保留时间平衡来演示如何将与之合并 （标记 (Y) 块中） 的现有多电池放电装置逻辑上面所述的逻辑。

请注意，这不是处方的 SDB 算法应如何实现由 Oem、 但相当简单，假设，多电池设备用于说明 SDB 行为此部分中所述的综合示例。


*完整的固件 Implemenation 的平衡 SDB 算法的简单年龄*

![完整的固件 Implemenation 的平衡 SDB 算法的简单年龄](images/powermeter-firmware-age-balancing-algorithm-hot-swap.png)


## <a name="power-stack-architecture"></a>Power 堆栈体系结构

本部分介绍 power 堆栈及它们与每个其他的相对关系中包含的所有组件的组件布局。

![显示 HPMI power 堆栈体系结构](images/powermeter-hpmi-stack-architecture.png)


### <a name="battery-miniport"></a>电池微型端口

电池微型端口接口保持不变。

SDB 接口执行操作会影响或影响依赖于 ACPI/CmBatt 机制或开发其专有的微型端口 OEM 的愿望。

注意：Windows 将转发所有[IOCTL_BATTERY_SET_INFORMATION](https://msdn.microsoft.com/library/windows/desktop/aa372701.aspx)枚举在系统上的所有电池设备的命令。

### <a name="hpmi"></a>HPMI

硬件电源管理器接口 (HPMI)，是在 power 堆栈中引入的新组件。

HPMI 是开发和拥有的 OEM/设备制造商的驱动程序。

HPMI 详尽了解的基础硬件配置和状态，并且有权访问系统固件。 

若要实现的 SDB 功能，则 HPMI 驱动程序将：

1.  向 Windows 注册自身。
2.  公布 SDB 支持。
3.  使用提供的 Windows 的 SDB 控制参数。

支持 SDB 多电池系统所需实现今后 HPMI 接口。 HPMI API 协议是用于实现多个电池系统的新标准。

没有计划，以便在将来，HPMI 将更新以支持其他充电，放电和管理功能进行收费。

### <a name="driver-characteristics"></a>驱动程序特征

HPMI 驱动程序的多个实例都不存在的系统上。
HPMI 可能作为用户模式或内核模式驱动程序实现。

### <a name="installation"></a>安装

HPMI 可能表现为 ACPI 设备也是由一个其他 OEM 服务/驱动程序的 OEM 自行枚举的根。

### <a name="implementation-of-sdb-algorithm"></a>SDB 算法的实现

下图说明了如果固件组件已承载的电池控制逻辑的大容量方式可能实现的 SDB 算法的两个示例。

![HPMI 和固件示例 SDB 算法堆栈示例](images/powermeter-firmware-and-hpmi-implementation.png)


### <a name="hpmi-implements-sdb-algorithm"></a>HPMI 实现 SDB 算法

HPMI 可能会选择实现 SDB 算法，这需要 HPMI 到对固件的正向的费用放电提示。 

### <a name="firmware-implements-sdb-algorithm"></a>固件实现 SDB 算法

或者，HPMI 可能充当转发器，只需对固件 SDB 算法实现的位置，利用率提示转发 Windows 电池上, 图中所示。 出于以下原因，建议使用此模型：

1. 实现 SDB 算法所需的信息是随时可用 – 无需将最高为 HPMI 此信息

2. SDB 算法是以释放逻辑已在多电池系统中实现的扩展

完整流程图模型描述了如何实现 SDB 算法所示[固件中实现 SDB 算法](#IMPLEMENTING-SDB)。



## <a name="interface-definitions"></a>接口定义

引入 HPMI 设备新的设备接口类 GUID。 HPMI 设备必须将自身标识为实现[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。 有关详细信息，请参阅[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)WDK 中。

Windows 用于查询和配置 HPMI 设备使用设备到达通知。

```cpp
//
// HPMI Device Interface Class.
//

// {DEDAE202-1D20-4C40-A6F3-1897E319D54F}
DEFINE_GUID(GUID_DEVINTERFACE_HPMI, 
            0xdedae202, 0x1d20, 0x4c40, 0xa6, 0xf3, 0x18, 0x97, 0xe3, 0x19, 0xd5, 0x4f);
```

HPMI 应该可以向服务多个同时 IOCTL 调用。

请注意，设备索引应设置为零。

### <a name="feature-discovery"></a>功能发现

[IOCTL_HPMI_QUERY_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/mt828475.aspx)用于发现支持 HPMI 的功能。 IOCTL_HPMI_QUERY_CAPABILITIES 是所需的 IOCTL。

Windows 将发出此 IOCL HPMI 到一次后发现新 HPMI 驱动程序实例。 


```cpp
//
// Query command sent to HPMI to query features supported by HPMI and Windows
// services requested by HPMI.
//
// This IOCTL may be issued multiple times, HPMI must respond with same 
// information in HPMI_QUERY_CAPABILITIES_RESPONSE, as a response to all
// subsequent IOCTL calls.
//

#define IOCTL_HPMI_QUERY_CAPABILITIES                     
    CTL_CODE(FILE_DEVICE_BATTERY, 0x200, 
             METHOD_BUFFERED, FILE_READ_ACCESS | FILE_WRITE_ACCESS)
```

```cpp
//
// IOCTL_HPMI_QUERY_CAPABILITIES - Command.
//

typedef struct _HPMI_QUERY_CAPABILITIES {

    //
    // Set to HPMI_QUERY_CAPABILITIES_VERSION_1.
    //

    ULONG Version;

} HPMI_QUERY_CAPABILITIES, *PHPMI_QUERY_CAPABILITIES;
```

```cpp
#define HPMI_QUERY_CAPABILITIES_VERSION_1                   
    (1)
#define HPMI_QUERY_CAPABILITIES_SIZEOF_VERSION_1         
    sizeof(HPMI_QUERY_CAPABILITIES)
```

```cpp
//
// IOCTL_HPMI_QUERY_CAPABILITIES - Response.
//

#define HPMI_REQUEST_SERVICE_NONE                           
    (0x00000000)    // No Windows services is requested.
#define HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS      
    (0x00000001)    // Battery utilization hints requested from Windows.

#define HPMI_CAPABILITY_NOT_SUPPORTED                       
    (0x00000000)    // HPMI supports no capabilities.
#define HPMI_CAPABILITY_SDB_OEM_SIMPLE_AGE_BALANCING        
    (0x00000001)    // OEM device specific age balancing SDB support
```

```cpp
typedef struct _HPMI_QUERY_CAPABILITIES_RESPONSE {

    //
    // Set to HPMI_QUERY_CAPABILITIES_RESPONSE_VERSION_1.
    //

    ULONG Version;

    //
```


### <a name="command-format"></a>命令格式

Windows 会发出具有此 IOCTL [HPMI_QUERY_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/mt828472.aspx)。

版本设置为 HPMI_QUERY_CAPABILITIES_VERSION_1。


### <a name="response-format"></a>响应格式 

HPMI 必须返回 STATUS_SUCCESS 代码。

HPMI 响应中设置以下值[HPMI_QUERY_CAPABILITIES_RESPONSE](https://msdn.microsoft.com/library/windows/hardware/mt828473.aspx)结构：

- 版本设置为 HPMI_QUERY_CAPABILITIES_RESPONSE_VERSION_1
- RequestService 设置为 HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS 确保 HPMI 驱动程序收到[IOCTL_HPMI_BATTERY_UTILIZATION_HINT](https://msdn.microsoft.com/library/windows/hardware/mt828474.aspx)。
- SdbCapabilities 设置为 HPMI_CAPABILITY_SDB_OEM_SIMPLE_AGE_BALANCING 以指示电池年龄均衡支持。


#### <a name="battery-utilization"></a>电池利用率

Windows 问题[IOCTL_HPMI_BATTERY_UTILIZATION_HINT](https://msdn.microsoft.com/library/windows/hardware/mt828474.aspx)到 HPMI 以提供最更新的电池利用率的提示。 IOCTL_HPMI_BATTERY_UTILIZATION_HINT 是所需的 IOCTL。

HPMI 可能利用 PreserveNonHotSwappableBatteries 提示中所述[调整 SDB 算法，用于具有热插拔电池](#ADAPTING-SDB)以节省内部电池。

```cpp
//
// Set command sent to HPMI to provide battery utilization hints.
//
// This IOCTL may be issued multiple times if HPMI requests
// HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS service.
//

#define IOCTL_HPMI_BATTERY_UTILIZATION_HINT                 
    CTL_CODE(FILE_DEVICE_BATTERY, 0x201, 
             METHOD_BUFFERED, FILE_READ_ACCESS | FILE_WRITE_ACCESS)

//
// Boolean type value.
//

typedef enum _HPMI_HINT_BOOL {
    // No data is available.
    HpmiBoolUnavailable = 0,

    // Condition is asserted to be false.
    HpmiBoolFalse,

    // Condition is asserted to be true.
    HpmiBoolTrue,

    // Value not used.
    HpmiBoolMax

} HPMI_HINT_BOOL, *PHPMI_HINT_BOOL;
```

```cpp
//
// IOCTL_HPMI_BATTERY_UTILIZATION_HINT - Command.
//

typedef struct _HPMI_BATTERY_UTILIZATION_HINT {

    //
    // Set to HPMI_BATTERY_UTILIZATION_HINT_VERSION_1.
    //

    ULONG Version;

    //
    // This hint indicates if the OEM Battery Manager should attempt to save as
    // much charge as possible in the non-hot swappable batteries (i.e. the
    // batteries are generally referred to as "internal batteries", these
    // batteries cannot be removed while system is operational).
    //
    // Interpretation of values:
    //  - HpmiBoolUnavailable:
    //      Battery utilization hint is unavailable at the moment.
    //  - HpmiBoolFalse:
    //      It is not necessary to preserve charge in the internal batteries
    //      at the moment.
    //  - HpmiBoolTrue:
    //      Every attempt should be made to save as much charge as possible in
    //      the internal batteries.
    //

    HPMI_HINT_BOOL PreserveNonHotSwappableBatteries;

} HPMI_BATTERY_UTILIZATION_HINT, *PHPMI_BATTERY_UTILIZATION_HINT;
```

```cpp
#define HPMI_BATTERY_UTILIZATION_HINT_VERSION_1              
    (1)
#define HPMI_BATTERY_UTILIZATION_HINT_SIZEOF_VERSION_1       
    sizeof(HPMI_BATTERY_UTILIZATION_HINT)
```


### <a name="command-format"></a>命令格式 

Windows 会发出与 HPMI_BATTERY_UTILIZATION_HINT 此 IOCTL。 版本设置为*HPMI_BATTERY_UTILIZATION_HINT_VERSION_1*。

[HPMI_BATTERY_UTILIZATION_HINT](https://msdn.microsoft.com/library/windows/hardware/mt828469.aspx)

PreserveNonHotSwappableBatteries 设置为以下值之一：

- HpmiBoolUnavailable:可以提供没有电池利用率提示时设置。 作为响应，HPMI/固件通常应该咨询成为放电装置策略。
- HpmiBoolFalse:Windows 确定电池年龄平衡发生扩大时设置。
- HpmiBoolTrue:当 Windows 确定需要节省存储在内部电池的能源的组。

### <a name="response-format"></a>响应格式

HPMI 必须返回 STATUS_SUCCESS 代码。

在响应中不返回任何数据。


## <a name="sample-interface-contract"></a>示例接口协定

请参阅[HMPI.h](https://msdn.microsoft.com/library/windows/hardware/mt828470.aspx)完整 （示例） API 协定的接口定义，此处所述。



>[!NOTE]
> 本文档的内容可能会发生更改，恕不另行通知。



