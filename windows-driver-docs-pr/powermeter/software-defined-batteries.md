---
title: 软件定义的电池
description: 软件定义的电池
keywords:
- 软件定义的电池
- SDB
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cc44dfff5e2fe72b95010538488ee3f0472d156
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829038"
---
# <a name="software-defined-battery"></a>软件定义的电池

>[!NOTE]
> 在商业发行之前会发生实质性修改的、与预发布产品相关的一些信息。 Microsoft 对于此处提供的信息不作任何明示或默示的担保。

## <a name="introduction"></a>简介

本主题的目的是介绍软件定义电池（SDB），介绍 Windows SDB 体系结构，并详细介绍 Windows API 和此功能的 DDI 协定。 

本主题首先介绍了一个虚构的2个电池系统的简单生存期平衡 SDB 算法。 这后跟实现 SDB 算法所需的体系结构布局和 API 约定。

## <a name="nomenclature"></a>命名法

- BattC-电量类驱动程序

- CAD-充电仲裁驱动程序（CAD）是一个 Microsoft 驱动程序，可仲裁 USB 旧、USB 类型 C 和无线计费源之间的电力

- 冷插拔电池-无法从系统中删除的电池，但不会出现限电或总断电的风险

- 周期计数-电池完成的完整充电周期数，如 ACPI 规范中所述

- 热插拔电池-在系统运行时可以安全删除的电池，无限电的风险

- HPMI-硬件电源管理器界面

- 非热插拔电池-安装在系统中的一个或多个冷插拔和不可交换电池

- 不可交换电池-未设计并且打算由最终用户删除的电池

## <a name="sdb-overview"></a>SDB 概述
可在以下位置找到有关软件定义电池的 MSR 研究文档： [https://www.microsoft.com/research/wp-content/uploads/2016/02/multibattery_sosp2015.pdf](https://www.microsoft.com/research/wp-content/uploads/2016/02/multibattery_sosp2015.pdf)。 

本主题 reprises 介绍了本文中所述的观点，并向他们介绍了便携式计算机和其他移动设备中基于 productizing software 的电池寿命平衡功能。 

假设有两个电池系统。 其中一个电池是不可移动电池，位于 SOC 旁边–我们来调用此*内部电池*。 另一电池是可热插拔的电池，位于可移动键盘旁边–我们来称这*外部电池*。 

*多电池系统*

![显示内部和外部电池的多电池系统](images/powermeter-multi-battery.png)

当键盘连接在一段时间内断开连接时，它会强制两个电池的使用时间不同。 这会通过使用 SDB simple age 平衡算法，创建用于平衡电池和延长系统可用性周期的时间范围。

## <a name="simple-age-balancing-sdb-algorithm"></a>简单的 Age 平衡 SDB 算法

此算法称为 "*简单年龄平衡*"，因为它会尝试平衡电池寿命。 简单的 age 平衡算法会使系统更倾向于放电电量最少的电池。 如果电池的累计量较小，则不只会有更高的容量来保持电源，但在交付能力时通常更有效。 因此延长系统可以承受电池的时间。

*简单的 Age 平衡 SDB 算法*

![简单的 Age 平衡 SDB 算法](images/powermeter-simple-age-balancing-algorithm.png)

简单的 age 平衡算法背后的核心理念是，只需使用最小的电池周期计数，如以上流程图中的决策框（2）所示。 在此示例中，假设系统允许使用内部或外部电池。 但对于所有系统来说，这种情况并不适用。 其他系统可能不是很灵活，或者可能对电池的使用有电气限制。 在这种情况下，该算法需要最佳的老化平衡尝试。 例如，请考虑以下事项。  

1. 不能以独占方式使用外部电池的系统（可能是因为外部电池只是一种补充的电源）。 此系统可通过同时在上述流程图中同时放电进程块（A）中的内部和外部电池来实现简单的 age 平衡算法。

2. 每次出现时都需要使用外部电池的系统（可能是由于与使可移动键盘保持开机而增加的额外功率绘图）：此系统可以同时实现简单的 age 平衡算法正在在上述流程图中同时处理进程块（B）中的内部和外部电池。

仅当内部和外部电池中有足够的费用运行系统时，才可以使用简单的 age 平衡算法，但决定框（1）描述了上述流程图中的此条件检查。 例如（再次回到假设的系统）如果外部电池不收取任何费用，则不存在电池电量平衡的作用域，并且决策框（1）将导致 "NO" 分支。

当简单的年龄平衡算法未生效时，OEM 可以自由选择约束和条件，这种情况除外。 例如，OEM 可能会选择不在以下情况进行任何时期平衡：

1.  SOC/处理器在高性能模式下运行
2.  系统不稳定

当未使用简单的生存期平衡算法时（由于上述一个或多个条件），逻辑将还原为 OEM 的专有电池使用策略，如以上流程图中的进程框（3）所示。 处理框（3）是指如果不支持 SDB，则 OEM 将会生效。


## <a name="span-idadapting-sdbspanspan-idadapting-sdbspanadapting-sdb-algorithm-for-use-with-hot-swappable-batteries"></a><span id="adapting-sdb"></span><span id="ADAPTING-SDB"></span>调整用于热插拔电池的 SDB 算法

简单的 age 平衡 SDB 算法会尝试使用 healthiest 的电池，尽管此策略非常适合用于缩短长期的电池寿命，但可能会严重影响系统的短期可用性，如以下方案中所述。

在上面所述的两个电池系统中，考虑以下情况：

1.  用户的使用时间应足够长，直到内部和外部电池的电量耗尽。

2.  与内部电池相比，外部电池已过时。

在此系统上执行简单的 age 平衡算法时，它将尝试先消耗内部电池中存储的电量（基于条件 #1 和上面列出的 #2）。 当用户决定在一段时间后拔出外部电池时，这会导致用户体验不佳，因为当外部电池被分离时，一旦外部电池被占用就会大幅降低。

在非 SDB 系统上，通常不会出现此问题，因为在大多数情况下，在将内部电池投入使用之前，外部电池将耗尽。

因此，在可能发生上述情况时，需要有选择地禁用简单的 age 平衡算法。 

概括而言，每当用户预计使用系统长时间才能删除外部电池时，最好禁用 SDB 算法，并使用 OEM 电池使用策略（通常优先使用外部电池）恢复到。

Windows 计算电池可用性，并生成 "保留非热插拔电池" 提示。 当 SDB 算法使用此提示时，如以下流关系图中的决策框（X）所示。

*适用于热插拔电池的简单时期平衡 SDB 算法*

![适用于热插拔电池的简单时期平衡 SDB 算法](images/powermeter-simple-age-balancing-algorithm-hot-swap.png)


## <a name="span-idimplementing-sdbspanspan-idimplementing-sdbspanimplementing-sdb-algorithm-in-firmware"></a><span id="implementing-sdb"></span><span id="IMPLEMENTING-SDB"></span>在固件中实现 SDB 算法

本部分描述系统固件中实现的完全电池放电控制逻辑。 这会在上述电池使用情况平衡逻辑上构建，以演示现有的多电池放电逻辑（标记在（Y）块中）如何与它合并在一起。

请注意，这并不是 Oem 如何实现 SDB 算法的处方，而是本部分中介绍的用于阐释 SDB 行为的简单、假设多电池设备的综合示例。


*简单的生存期平衡 SDB 算法的完整固件实现*

![简单的生存期平衡 SDB 算法的完整固件实现](images/powermeter-firmware-age-balancing-algorithm-hot-swap.png)


## <a name="power-stack-architecture"></a>电源堆栈体系结构

本部分介绍每个参与电源堆栈的组件的组件布局及其相对关系。

![显示 HPMI 的电源堆栈体系结构](images/powermeter-hpmi-stack-architecture.png)


### <a name="battery-miniport"></a>电池微型端口

电池微型端口接口保持不变。

SDB 接口不会影响或影响 OEM 想要依赖 ACPI/CmBatt 机制或开发其专用微型端口。

注意： Windows 会将所有[IOCTL_BATTERY_SET_INFORMATION](https://docs.microsoft.com/windows/desktop/Power/ioctl-battery-set-information)命令转发到系统上枚举的所有电池设备。

### <a name="hpmi"></a>HPMI

硬件电源管理器接口（HPMI）是在电源堆栈中引入的新组件。

HPMI 是 OEM/设备制造商开发和拥有的驱动程序。

HPMI 对基础硬件配置和状态进行了深入了解，并可以访问系统固件。 

若要实现 SDB 功能，HPMI 驱动程序将：

1.  向 Windows 注册自身。
2.  公布 SDB 支持。
3.  使用 Windows 提供的 SDB 控制参数。

支持 SDB 的多电池系统需要实现 HPMI 接口。 HPMI API 协议是实现多个电池系统的新标准。

目前有一些计划，HPMI 会进行更新，以支持其他收费、放电和收费管理功能。

### <a name="driver-characteristics"></a>驱动程序特征

系统上不应存在 HPMI 驱动程序的多个实例。
HPMI 可以作为用户模式或内核模式驱动程序实现。

### <a name="installation"></a>安装

HPMI 可以表现为 ACPI 设备，也可以是由 OEM 的其他 OEM 服务/驱动程序所枚举的根。

### <a name="implementation-of-sdb-algorithm"></a>SDB 算法的实现

下图说明了在固件组件已承载大容量控制逻辑的情况下，如何实现 SDB 算法的两个示例。

![HPMI 和固件示例 SDB 算法堆栈示例](images/powermeter-firmware-and-hpmi-implementation.png)


### <a name="hpmi-implements-sdb-algorithm"></a>HPMI 实现 SDB 算法

HPMI 可以选择实现 SDB 算法，这将要求 HPMI 将收费/放电提示转发到固件。 

### <a name="firmware-implements-sdb-algorithm"></a>固件实现 SDB 算法

或者，HPMI 可以充当转发器，只需将 Windows 电池使用提示转发到用于实现 SDB 算法的固件，如上图所示。 建议使用此模型，原因如下：

1. 实现 SDB 算法所需的信息随时可用–无需将此信息传递到 HPMI

2. SDB 算法是一种用于释放多个电池系统中已经实现的逻辑的扩展

描述如何实现 SDB 算法的完整流程图模型，如在[固件中实现 Sdb 算法](#IMPLEMENTING-SDB)中所示。



## <a name="interface-definitions"></a>接口定义

引入了新的 HPMI 设备的设备接口类 GUID。 HPMI 设备必须将自身标识为实现[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。 有关详细信息，请参阅在 WDK 中[使用设备接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)。

Windows 使用设备到达通知来查询和配置 HPMI 设备。

```cpp
//
// HPMI Device Interface Class.
//

// {DEDAE202-1D20-4C40-A6F3-1897E319D54F}
DEFINE_GUID(GUID_DEVINTERFACE_HPMI, 
            0xdedae202, 0x1d20, 0x4c40, 0xa6, 0xf3, 0x18, 0x97, 0xe3, 0x19, 0xd5, 0x4f);
```

HPMI 应能够为多个同时执行的 IOCTL 调用服务。

请注意，设备索引应设置为零。

### <a name="feature-discovery"></a>功能发现

[IOCTL_HPMI_QUERY_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ni-hpmi-ioctl_hpmi_query_capabilities)用于发现 HPMI 支持的功能。 IOCTL_HPMI_QUERY_CAPABILITIES 是必需的 IOCTL。

发现新的 HPMI 驱动程序实例之后，Windows 将发出此 IOCL 一次 HPMI。 


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

Windows 通过[HPMI_QUERY_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ns-hpmi-_hpmi_query_capabilities)发出此 IOCTL。

版本设置为 HPMI_QUERY_CAPABILITIES_VERSION_1。


### <a name="response-format"></a>响应格式 

HPMI 必须返回 STATUS_SUCCESS 代码。

HPMI 通过设置[HPMI_QUERY_CAPABILITIES_RESPONSE](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ns-hpmi-_hpmi_query_capabilities_response)结构中的以下值来做出响应：

- 版本设置为 HPMI_QUERY_CAPABILITIES_RESPONSE_VERSION_1
- RequestService 设置为 HPMI_REQUEST_SERVICE_BATTERY_UTILIZATION_HINTS，以确保 HPMI 驱动程序接收[IOCTL_HPMI_BATTERY_UTILIZATION_HINT](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ni-hpmi-ioctl_hpmi_battery_utilization_hint)。
- SdbCapabilities 设置为 HPMI_CAPABILITY_SDB_OEM_SIMPLE_AGE_BALANCING，指示电池电量平衡支持。


#### <a name="battery-utilization"></a>电池利用率

Windows [IOCTL_HPMI_BATTERY_UTILIZATION_HINT](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ni-hpmi-ioctl_hpmi_battery_utilization_hint) HPMI 提供最新的电池使用提示。 IOCTL_HPMI_BATTERY_UTILIZATION_HINT 是必需的 IOCTL。

HPMI 可以利用 PreserveNonHotSwappableBatteries 提示，如[使用热插拔电池调整 SDB 算法](#ADAPTING-SDB)以节省内部电池。

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

Windows 通过 HPMI_BATTERY_UTILIZATION_HINT 发出此 IOCTL。 版本设置为*HPMI_BATTERY_UTILIZATION_HINT_VERSION_1*。

[HPMI_BATTERY_UTILIZATION_HINT](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/ns-hpmi-_hpmi_battery_utilization_hint)

PreserveNonHotSwappableBatteries 设置为以下值之一：

- HpmiBoolUnavailable：在未提供电池使用率提示时设置。 作为响应，HPMI/Fimware 通常应参与到事实的放电策略。
- HpmiBoolFalse：在 Windows 确定要进行电池电量平衡的时机时间时设置。
- HpmiBoolTrue：在 Windows 确定需要保留内部电池中存储的能量时设置。

### <a name="response-format"></a>响应格式

HPMI 必须返回 STATUS_SUCCESS 代码。

响应中未返回任何数据。


## <a name="sample-interface-contract"></a>示例接口协定

请参阅[HMPI](https://docs.microsoft.com/windows-hardware/drivers/ddi/hpmi/index) ，了解此处所述的接口定义的完整（示例） API 约定。



>[!NOTE]
> 此文档的内容如有更改，恕不另行通知。



