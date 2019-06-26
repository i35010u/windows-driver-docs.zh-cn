---
title: 关于传感器驱动程序事件
description: 关于传感器驱动程序事件
ms.assetid: 1e747743-f701-4854-92be-7b55c39fee08
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f30b0c6a0d3f7af4e2945df5f2b4e3c944fc627f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384512"
---
# <a name="about-sensor-driver-events"></a>关于传感器驱动程序事件


应用程序可以从以下两种方式的传感器接收的信息： 通过请求特定的属性或数据字段同步，或以异步方式，通过由传感器驱动程序引发的事件订阅。

传感器驱动程序可以引发**状态更改事件**，通知的设备中转换到新的运行条件，以及其他种类的事件通知的应用程序。 您的驱动程序应引发你的设备提供了每个传感器的单独事件。

**请注意**  不要使用[ **IWDFDevice::PostEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-postevent)引发传感器事件。 传感器平台不会将转发到连接的客户端程序的此类事件。

 

## <a name="state-change-events"></a>状态更改事件

传感器驱动程序通过调用传感器类扩展引发状态更改事件[ **ISensorClassExtension::PostStateChange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)方法。 例如，已完成初始化传感器驱动程序会调用此方法用信号通知的新[ **SensorState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001)名为传感器值\_状态\_准备就绪。

## <a name="event-constants"></a>事件常量

传感器平台定义以下常量的驱动程序的事件。

**传感器事件类型**

传感器平台定义以下传感器事件类型标识符。

| 名称 | 描述 |
| --- | --- |
| SENSOR_EVENT_DATA_UPDATED | 指示新数据可用。
| SENSOR_EVENT_PROPERTY_CHANGED| 指示属性值更改。|
| SENSOR_EVENT_STATE_CHANGED| 例如，到 SENSOR_STATE_READY SENSOR_STATE_INITIALIZING 从指示操作状态的更改。|


**传感器事件 PROPERTYKEYs**

传感器平台定义了以下**PROPERTYKEYs**来标识传感器事件参数。

| 名称 | 描述 |
| --- | --- |
| SENSOR_EVENT_PARAMETER_EVENT_ID| 指示 IPortableDeviceValues 中的 GUID 值为事件类型 ID，如 SENSOR_EVENT_DATA_UPDATED。|
| SENSOR_EVENT_PARAMETER_STATE| 指示 IPortableDeviceValues 中的无符号的整数值是传感器状态，例如 SENSOR_STATE_READY。<br>**请注意**以引发状态更改事件，调用[ISensorClass Extension::PostStateChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)。 无需显式指定 SENSOR_EVENT_PARAMETER_STATE 来引发事件。|

## <a name="other-events"></a>其他事件

传感器驱动程序通过调用传感器类扩展引发的事件的所有其他类型[ **ISensorClassExtension::PostEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)方法。 此方法提供了一种泛型可扩展的方式来引发传感器事件不相关的操作状态。 每次调用**得到**包含一个指向[IPortableDeviceValuesCollection](https://go.microsoft.com/fwlink/p/?linkid=131487)。 每个[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)对象在此集合中的包含**GUID**传感器值\_事件\_参数\_事件\_ID属性，用于标识事件类型，并包含事件数据的可选数据字段值。 例如，具有新的城市数据的 GPS 驱动程序将使用传感器\_事件\_数据\_更新事件 ID，并提供一个字符串值，传感器\_数据\_类型\_CITY 属性键。

您的驱动程序会将事件发布后，传感器类扩展将事件和任何关联的数据转发到传感器 API。

您可以在名为 Sensors.h 的文件中找到平台定义的常量的定义。 有关平台定义传感器常量的详细信息，请参阅[常量](about-sensor-constants.md)。

## <a name="managing-sensor-driver-events"></a>管理传感器驱动程序事件

您的驱动程序接受事件的请求之前，它应创建单独的线程来生成和发布事件。 通过使用一个线程，可以帮助防止频繁事件过程中阻止同步过程，例如数据请求回调。 引发数据更新事件的线程类的示例，请参阅[Raising Data-Updated 事件](raising-events.md)。

仅当至少一个客户端应用程序已请求事件通知，您的传感器应引发事件。 传感器类扩展在应用程序请求事件通知，包括状态更改事件时通知该驱动程序通过[ **ISensorDriver::OnClientSubscribeToEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)。 此方法提供[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)标识应用程序和一个字符串，标识应用程序正在为其请求事件通知的传感器的指针。 可以使用 IWDFFile 指针作为唯一标识符，以帮助跟踪已订阅事件的应用程序。 尽管您的传感器无法引发事件发送到特定的客户端，您可能需要跟踪的哪些应用程序集的特定值的属性，例如传感器\_属性\_当前\_报表\_时间间隔或传感器\_属性\_更改\_敏感度。

例如，如果多个客户端应用程序将不同的值设置为传感器\_属性\_当前\_报表\_间隔，可应用到具有的最短间隔设置的事件频率的规则已请求。 但是，您的传感器可能需要调整每个时间间隔的新客户端订阅的事件或现有的客户端取消订阅。 有关报表的时间间隔，包括代码示例，请参阅[筛选数据](filtering-data.md)。

### <a name="sensor-events-and-data-privacy"></a>传感器事件和数据隐私

等其他数据请求，为事件通知的请求都通过使用传感器类扩展的安全。 类扩展允许仅为用户请求此数据的位置数据。

>[!CAUTION]
> 请确保使用传感器类扩展来处理所有 I/O 请求的传感器。 通过执行此操作，您不太可能，以显示用户的私人信息。

 

有关数据隐私的详细信息，请参阅[隐私和安全的传感器和位置平台](https://docs.microsoft.com/windows-hardware/drivers/gnss/privacy-and-security-in-the-sensor-and-location-platform)

## <a name="related-topics"></a>相关主题
[**传感器属性**](https://docs.microsoft.com/windows-hardware/drivers/sensors/sensor-properties)



