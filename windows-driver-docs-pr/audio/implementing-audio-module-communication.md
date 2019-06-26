---
title: 实现音频模块通信
description: 音频模块是不同的音频处理逻辑执行相对原子的函数。
ms.date: 07/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f6d887cab55793345dd36fc677004cdd577d863
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359916"
---
<a name="implementing-audio-module-communication"></a>实现音频模块通信
========================================================================================

音频模块是不同的音频处理逻辑执行相对原子的函数。 音频模块可以驻留在音频驱动程序或音频 DSP 中。 示例音频模块是基于 DSP 的音频处理。

从 Windows 10 版本 1703年，有 Api 和 DDIs 以支持从通用 Windows 平台 (UWP) 应用程序和内核模式设备驱动程序的通信。

本主题提供有关内核设备驱动程序中实现音频模块通信信息。 

有关如何将命令发送和接收来自音频设备模块使用的 UWP 应用的更改通知的信息，请参阅[配置和查询音频设备模块](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)。

## <a name="why-use-audio-modules"></a>为何使用音频模块？

通常，Oem 捆绑他们使客户能够针对控制此音频系统的各个方面的系统上配置应用程序和调整其首选项。 音频子系统可以包含各种组件，如主机上音频处理对象，如智能 a m p （全部除了本身的音频编解码器外） 的专用的硬件以及硬件 DSP 处理。 在大多数情况下会创建这些组件并由不同供应商销售。 从历史上看，Ihv 已创建其自己专用的 Api 来与另一个集成和各个组件之间发送信息。 现有的 WIN32 配置应用程序，则也可以利用这些私有 Api。

[通用 Windows 平台 (UWP)](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)，提供了一组 Api，使单个应用程序在各种设备之间运行。 UWP 还引入了新外观和体验已不再是在 Windows 10 上运行的应用程序的客户期望。 许多 Oem 想要生成 UWP 上的音频配置应用程序。 但是，UWP （AppContainer 沙盒） 的核心安全功能阻止从应用程序到音频的子系统中的其他组件进行通信。 这会使配置应用程序在 UWP 中无法访问以前使用的专用 Api。 

从 Windows 10 版本 1703年，音频模块 UWP API 允许配置与通过新的 KS 属性集发现模块中的内核和硬件层进行通信的应用程序和用户模式组件。
音频 IHV 和 Isv 可以编写应用程序和服务可以与他们使用妥善定义的接口由 Windows 提供的硬件模块进行通信。 有关音频模块 API 的详细信息，请参阅[Windows.Media.Devices Namespace](https://docs.microsoft.com/uwp/api/Windows.Media.Devices)


<a name="span-idaudiomoduledefinitionsspanaudio-module-definitions"></a><span id="Audio_Module_Definitions"></span>音频模块定义
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
这些定义是特定于音频模块。

术语 | 定义
------------ | -------------
音频模块    | 音频处理逻辑执行相对原子的函数的非重复块。 可以驻留在音频驱动程序或音频 DSP 中。 示例音频模块将音频处理对象 (APO)。


<a name="span-idcommondefinitionsspancommon-audio-definitions"></a><span id="Common_Definitions"></span>通用音频定义
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
使用音频驱动程序时，通常使用这些定义。

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
音频模块将支持的 Windows 机制来发送音频组件的用户模式和内核模式之间的消息放入位置。 一个重要的区别是音频模块标准化传输管道。 它不会通过该传输建立通信协议，并且依赖于 Isv 和 Ihv，若要定义的协议。 其目的是允许现有第三方设计，以迁移轻松音频模块很少更改。

<Diagram Pending>

音频模块 API 通过两种不同的目标方法提供对模块的访问： KS wave 筛选器和初始化的 KS 插针 （流）。 放置和对特定模块的访问是特定于实现的。

有和其他应用程序将仅能够通过筛选器句柄访问可用的模块。 在流上加载单个不是唯一有权访问该流的对象目标音频模块。

A p o s 有关详细信息，请参阅[Windows 音频处理对象](https://docs.microsoft.com/windows-hardware/drivers/audio/windows-audio-processing-objects)。

### <a name="sending-commands"></a>发送命令

音频模块客户端的途径来查询和更改的参数是将命令发送到音频的子系统中的内核和硬件组件中的音频模块。 音频模块 API 的命令结构松散定义，并可进行形式化模块发现和标识其自身的方式。 但是，详细的命令结构必须设计和实施所涉及的 ISV 和 IHV 建立可以发送哪些消息的协议和预期的响应。

### <a name="module-notifications-to-audio-module-clients"></a>向音频模块的客户端模块通知

音频的微型端口还具有一种方法通知并将信息传递给音频模块的客户端，如果客户端已订阅特定模块上的通知。 这些通知中传递的信息不由音频模块 API，而是由 ISV 和/或 IHV 定义。

### <a name="enable-disable-and-general-topology-information"></a>启用、 禁用和常规拓扑信息

音频模块 Api 定义如何枚举和将命令发送到模块。 但是，这些 Api 未显式定义音频模块的客户端如何启用或禁用特定模块。 此外，它不会建立一种方法供客户端查找拓扑信息或与另一个相关的模块的位置。 Ihv 和 Isv 可以确定此功能是否需要判定如何实现它。

建议的方法公开了全局驱动程序模块。 全局驱动程序模块会处理这些拓扑特定请求的自定义命令。

<a name="span-idaudiomoduleddisspanaudio-module-ddis"></a><span id="Audio_Module_DDIs"></span>音频模块 DDIs
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
**内核流式处理音频模块属性** 

新 KS 属性集，由标识[KSPROPSETID_AudioModule](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audiomodule)，已为特定于音频模块的三个属性定义。 

PortCls 微型端口驱动程序需要直接处理每个属性的响应可以提供任何帮助程序接口。

#### <a name="ksmediah"></a>ksmedia.h:

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

为支持[KSPROPERTY_AUDIOMODULE_DESCRIPTORS](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiomodule-descriptors)属性标识为音频模块识别驱动程序。 该属性将通过筛选器或 pin 句柄查询和 KSPROPERTY 传递作为 DeviceIoControl 调用的输入缓冲区。 [KSAUDIOMODULE_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)已定义来描述每个模块中的音频硬件。 为此请求的响应中返回这些描述符的数组

#### <a name="ksmediah"></a>ksmedia.h:

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
有关详细信息，请参阅[KSAUDIOMODULE_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_descriptor)。

### <a name="audio-module-command"></a>音频的模块命令

为支持[KSPROPERTY_AUDIOMODULE_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiomodule-command)属性允许音频模块客户端发送自定义命令来查询和设置音频模块的参数。 可以通过筛选器或 pin 句柄发送该属性和一个[KSAUDIOMODULE_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_property)作为 DeviceIoControl 调用的输入缓冲区传递。 客户端可以根据需要发送的其他信息立即旁边[KSAUDIOMODULE_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_property)将自定义命令发送到输入缓冲区中。

#### <a name="ksmediah"></a>ksmedia.h:

``` C++
#define AUDIOMODULE_MAX_DATA_SIZE 64000

typedef struct _KSPAUDIOMODULE_PROPERTY
{
    KSPROPERTY Property;
    GUID       ClassId;
    ULONG      InstanceId;
} KSAUDIOMODULE_PROPERTY, *PKSPAUDIOMODULE_PROPERTY;

```
有关详细信息，请参阅[KSAUDIOMODULE_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_property)。


### <a name="audio-module-notification-device-id"></a>音频模块通知设备 ID

为支持[KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiomodule-notification-device-id)需启用到信号通知微型端口，并将信息传递到音频模块的客户端。 此 ID 的生存期取决于正在公开和活动到 Windows 音频堆栈的音频设备的生存期。 可以通过筛选器或 pin 句柄发送该属性，并作为 DeviceIoControl 调用的输入缓冲区传递 KSPROPERTY。

有关详细信息，请参阅[KSAUDIOMODULE_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudiomodule_property)。


<a name="span-idportclshelperspanportcls-helper---audio-module-notifications"></a><span id="PortCls_Helper"></span>PortCls Helper-音频模块通知
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 添加了新的端口接口，以帮助驱动程序开发人员将通知发送到音频模块的客户端。 

#### <a name="portclsh"></a>PortCls.h:

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

 [IPortClsNotifications](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsnotifications)
    
 [IPortClsNotifications::AllocNotificationBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsnotifications-allocnotificationbuffer)

 [IPortClsNotifications::FreeNotificationBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsnotifications-freenotificationbuffer)   
    
 [IPortClsNotifications::SendNotificationBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportclsnotifications-sendnotification) 

### <a name="calling-sequence"></a>调用序列

微型端口将调入其端口来创建和发送通知。  在此图中显示的常规调用序列。

![AudioIPortClsNotifications 调用序列](images/AudioIPortClsNotificationsCallingSequenceDiagram.png)



 



