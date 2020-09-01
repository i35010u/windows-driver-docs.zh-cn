---
title: 实现音频模块通信
description: 音频模块是一种执行相对原子功能的不同音频处理逻辑。
ms.date: 07/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 324b19b81ac6cd53e37eb89844a32d10ede81345
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209126"
---
<a name="implementing-audio-module-communication"></a>实现音频模块通信
========================================================================================

音频模块是一种执行相对原子功能的不同音频处理逻辑。 音频模块可能驻留在音频驱动程序或音频 DSP 中。 一个示例音频模块是基于 DSP 的音频处理。

从 Windows 10 版本1703开始，有 Api 和 DDIs 支持通用 Windows 平台 (UWP) 应用和内核模式设备驱动程序的通信。

本主题提供有关在内核设备驱动程序中实现音频模块通信的信息。 

有关如何使用 UWP 应用发送命令和接收来自音频设备模块的更改通知的信息，请参阅 [配置和查询音频设备模块](./configure-and-query-audiodevicemodules.md)。

## <a name="why-use-audio-modules"></a>为什么使用音频模块？

Oem 通常会在其系统上捆绑一个配置应用程序，使客户能够控制该音频系统的各个方面，并将其调整为首选项。 音频子系统可以包含各种组件，例如主机音频处理对象、硬件 DSP 处理以及专用硬件（如智能 amp (除了音频编解码器本身) 以外）。 在大多数情况下，这些组件由不同的供应商创建和销售。 从历史上看，Ihv 创建了自己的专用 Api 来彼此集成，并在各个组件之间发送信息。 然后，现有 WIN32 配置应用程序将利用这些私有 Api。

[通用 Windows 平台 (UWP) ](/windows/uwp/get-started/universal-application-platform-guide)提供了一组 api，使单个应用程序能够在各种设备上运行。 UWP 还引入了新的外观，使客户对在 Windows 10 上运行的应用程序感到满意。 许多 Oem 希望在 UWP 上生成其音频配置应用程序。 不过，UWP 沙箱 (的一种核心安全功能) 阻止将应用程序与音频子系统中的其他组件通信。 这会呈现在 UWP 中无法访问的配置应用以前使用的私有 Api。 

从 Windows 10 版本1703开始，音频模块 UWP API 允许配置应用程序和用户模式组件与通过新的 KS 属性集发现的内核和硬件层中的模块进行通信。
音频 IHV 和 Isv 可以编写应用程序和服务，使用 Windows 提供的定义完善的接口与硬件模块通信。 有关音频模块 API 的详细信息，请参阅 [Windows. Media 命名空间](/uwp/api/Windows.Media.Devices)


<a name="span-idaudio_module_definitionsspanaudio-module-definitions"></a><span id="Audio_Module_Definitions"></span>音频模块定义
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
这些定义特定于音频模块。

术语 | 定义
------------ | -------------
音频模块    | 执行相对原子功能的一种不同的音频处理逻辑。 可能驻留在音频驱动程序或音频 DSP 中。 例如音频处理对象是 (APO) 的音频处理对象。


<a name="span-idcommon_definitionsspancommon-audio-definitions"></a><span id="Common_Definitions"></span>常见音频定义
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
通常在使用音频驱动程序时使用这些定义。

术语 | 定义
------------ | -------------
OEM | 原始设备制造商
IHV | 独立硬件供应商
ISV | 独立软件供应商
 |
HSA | 硬件支持应用程序
UWP | 通用 Windows 平台
 | 
APO | 音频处理对象
DSP | 数字信号处理

<a name="span-idarchitecturespanarchitecture"></a><span id="Architecture"></span>体系结构 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
音频模块采用 Windows 支持的机制在用户模式和内核模式音频组件之间发送消息。 一个重要区别是音频模块将传输管道标准化。 它不会通过该传输建立通信协议，并依赖于 Isv 和 Ihv 来定义协议。 目的是允许现有的第三方设计轻松地迁移到音频模块，但变化非常少。

<Diagram Pending>

音频模块 API 通过两种不同的目标方法提供对模块的访问权限： KS 波筛选器和初始化的 KS pin (流) 。 定位和访问特定模块是特定于实现的。

HSAs 和其他应用程序将只能访问通过筛选器句柄提供的模块。 在流上加载的每个对象都是将有权访问目标为流的音频模块的对象。

有关的详细信息，请参阅 [Windows 音频处理对象](./windows-audio-processing-objects.md)。

### <a name="sending-commands"></a>发送命令

音频模块客户端用于查询和更改参数的途径是将命令发送到内核中的音频模块和音频子系统中的硬件组件。 音频模块 API 的命令结构是松散定义的，并以模型的发现方式和标识自身的方式来确定其结构。 但是，必须由所涉及的 ISV 和 IHV 设计和实现详细的命令结构，以便为可以发送哪些消息和预期响应建立协议。

### <a name="module-notifications-to-audio-module-clients"></a>向音频模块客户端发送模块通知

如果客户端已在特定模块上订阅了通知，则音频微型端口还可以通知并将信息传递给音频模块客户端。 传递到这些通知中的信息不由音频模块 API 定义，而是由 ISV 和/或 IHV 定义。

### <a name="enable-disable-and-general-topology-information"></a>启用、禁用和常规拓扑信息

音频模块 Api 定义如何枚举命令并将其发送到模块。 但是，Api 不会显式定义音频模块客户端如何启用或禁用特定模块。 此外，它不会为客户端提供一种方式来查找拓扑信息或模块相对于彼此的位置。 Ihv 和 Isv 可以确定是否需要此功能，决定如何实现此功能。

推荐的方法是公开全局驱动程序模块。 全局驱动程序模块将处理这些特定于拓扑的请求的自定义命令。

<a name="span-idaudio_module_ddisspanaudio-module-ddis"></a><span id="Audio_Module_DDIs"></span>音频模块 DDIs
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
**内核流音频模块属性** 

已为特定于音频模块的三个属性定义了新的 KS 属性集，由 [KSPROPSETID_AudioModule](./kspropsetid-audiomodule.md)标识。 

PortCls 微型端口驱动程序需要直接处理每个属性的响应，因为没有提供帮助程序接口。

#### <a name="ksmediah"></a>ksmedia：

``` C++
#define STATIC_KSPROPSETID_AudioModule \
    0xc034fdb0, 0xff75, 0x47c8, 0xaa, 0x3c, 0xee, 0x46, 0x71, 0x6b, 0x50, 0xc6
DEFINE_GUIDSTRUCT("C034FDB0-FF75-47C8-AA3C-EE46716B50C6", KSPROPSETID_AudioModule);
#define KSPROPSETID_AudioModule DEFINE_GUIDNAMED(KSPROPSETID_AudioModule)

typedef enum {
    KSPROPERTY_AUDIOMODULE_DESCRIPTORS            = 1,  
    KSPROPERTY_AUDIOMODULE_COMMAND                = 2,
    KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID = 3,
} KSPROPERTY_AUDIOMODULE;
```

### <a name="audio-module-descriptors"></a>音频模块描述符

对 [KSPROPERTY_AUDIOMODULE_DESCRIPTORS](./ksproperty-audiomodule-descriptors.md) 属性的支持将驱动程序标识为可识别音频模块。 将通过筛选器或 pin 句柄查询属性，并将 KSPROPERTY 作为 DeviceIoControl 调用的输入缓冲区进行传递。 定义了[KSAUDIOMODULE_DESCRIPTOR](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor) ，以描述音频硬件中的每个模块。 为了响应此请求，返回了这些说明符的数组

#### <a name="ksmediah"></a>ksmedia：

``` C++
#define AUDIOMODULE_MAX_NAME_SIZE 128

typedef struct _KSAUDIOMODULE_DESCRIPTOR
{
    GUID    ClassId; 
    ULONG   InstanceId;
    ULONG   VersionMajor;
    ULONG   VersionMinor;
    WCHAR   Name[AUDIOMODULE_MAX_NAME_SIZE];
} KSAUDIOMODULE_DESCRIPTOR, *PKSAUDIOMODULE_DESCRIPTOR;
```
有关详细信息，请参阅 [KSAUDIOMODULE_DESCRIPTOR](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)。

### <a name="audio-module-command"></a>音频模块命令

支持 [KSPROPERTY_AUDIOMODULE_COMMAND](./ksproperty-audiomodule-command.md) 属性允许音频模块客户端发送自定义命令以查询和设置音频模块上的参数。 可以通过筛选器或 pin 句柄发送属性，并将 [KSAUDIOMODULE_PROPERTY](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property) 作为 DeviceIoControl 调用的输入缓冲区进行传递。 客户端可以选择立即发送与输入缓冲区中的 [KSAUDIOMODULE_PROPERTY](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property) 相邻的附加信息，以便发送自定义命令。

#### <a name="ksmediah"></a>ksmedia：

``` C++
#define AUDIOMODULE_MAX_DATA_SIZE 64000

typedef struct _KSPAUDIOMODULE_PROPERTY
{
    KSPROPERTY Property;
    GUID       ClassId;
    ULONG      InstanceId;
} KSAUDIOMODULE_PROPERTY, *PKSPAUDIOMODULE_PROPERTY;

```
有关详细信息，请参阅 [KSAUDIOMODULE_PROPERTY](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)。


### <a name="audio-module-notification-device-id"></a>音频模块通知设备 ID

若要使微型端口发出通知并将信息传递给音频模块客户端，必须支持 [KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID](./ksproperty-audiomodule-notification-device-id.md) 。 此 ID 的生存期与正在公开并对 Windows 音频堆栈激活的音频设备的生存期相关联。 可以通过筛选器或 pin 句柄发送属性，并将 KSPROPERTY 作为 DeviceIoControl 调用的输入缓冲区进行传递。

有关详细信息，请参阅 [KSAUDIOMODULE_PROPERTY](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)。


<a name="span-idportcls_helperspanportcls-helper---audio-module-notifications"></a><span id="PortCls_Helper"></span>PortCls Helper-音频模块通知
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 添加了新的端口接口，以协助驱动程序开发人员向音频模块客户端发送通知。 

#### <a name="portclsh"></a>PortCls：

``` C++
typedef struct _PCNOTIFICATION_BUFFER 
{
    UCHAR NotificationBuffer[1];
} PCNOTIFICATION_BUFFER, *PPCNOTIFICATION_BUFFER;

DECLARE_INTERFACE_(IPortClsNotifications,IUnknown)
{
    DEFINE_ABSTRACT_UNKNOWN()   // For IUnknown

    STDMETHOD_(NTSTATUS, AllocNotificationBuffer)
    (   THIS_
        _In_    POOL_TYPE       PoolType,
        _In_    USHORT          NumberOfBytes,
        _Out_   PPCNOTIFICATION_BUFFER* NotificationBuffer
    )   PURE;
    
    STDMETHOD_(void, FreeNotificationBuffer)
    (   THIS_
        _In_    PPCNOTIFICATION_BUFFER NotificationBuffer
    )   PURE;
    
    STDMETHOD_(void, SendNotificationBuffer)
    (   THIS_
        _In_    const GUID*     NotificationId,
        _In_    PPCNOTIFICATION_BUFFER NotificationBuffer
    )   PURE;
};

//
// Audio module notification definitions.
//
#define STATIC_KSNOTIFICATIONID_AudioModule \
    0x9C2220F0, 0xD9A6, 0x4D5C, 0xA0, 0x36, 0x57, 0x38, 0x57, 0xFD, 0x50, 0xD2
DEFINE_GUIDSTRUCT("9C2220F0-D9A6-4D5C-A036-573857FD50D2", KSNOTIFICATIONID_AudioModule);
#define KSNOTIFICATIONID_AudioModule DEFINE_GUIDNAMED(KSNOTIFICATIONID_AudioModule)

typedef struct _KSAUDIOMODULE_NOTIFICATION {
    union {
        struct {
            GUID        DeviceId;
            GUID        ClassId;
            ULONG       InstanceId;
            ULONG       Reserved;
        } ProviderId;
        LONGLONG        Alignment;
    };
} KSAUDIOMODULE_NOTIFICATION, *PKSAUDIOMODULE_NOTIFICATION;


```
有关详细信息，请参阅：

 [IPortClsNotifications](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsnotifications)
    
 [IPortClsNotifications::AllocNotificationBuffer](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsnotifications-allocnotificationbuffer)

 [IPortClsNotifications::FreeNotificationBuffer](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsnotifications-freenotificationbuffer) 
    
 [IPortClsNotifications::SendNotificationBuffer](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportclsnotifications-sendnotification)   

### <a name="calling-sequence"></a>调用序列

此微型端口将调用其端口来创建和发送通知。  此关系图中显示了一般调用序列。

![AudioIPortClsNotifications 调用序列](images/AudioIPortClsNotificationsCallingSequenceDiagram.png)



