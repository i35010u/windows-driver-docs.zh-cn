---
title: 关于传感器驱动程序事件
description: 关于传感器驱动程序事件
ms.assetid: 1e747743-f701-4854-92be-7b55c39fee08
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 220fbe45f14159e2277f74690a499cf2dd88a3b8
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010571"
---
# <a name="about-sensor-driver-events"></a>关于传感器驱动程序事件


应用程序可以通过两种方式从传感器接收信息：通过请求特定属性或数据字段同步，或通过订阅传感器驱动程序引发的事件以异步方式接收。

传感器驱动程序可能会引发 **状态更改事件**，这些事件会通知应用程序有关设备中的转换的新操作条件以及其他类型的事件通知。 你的驱动程序应为设备提供的每个传感器引发不同的事件。

**注意**   请勿使用[**IWDFDevice：:P ostevent**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-postevent)引发传感器事件。 传感器平台不会将此类事件转发到连接的客户端程序。

 

## <a name="state-change-events"></a>状态更改事件

传感器驱动程序通过调用传感器类扩展的 [**ISensorClassExtension：:P oststatechange**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange) 方法来引发状态更改事件。 例如，已完成传感器初始化的驱动程序将调用此方法，以向名为 "传感器状态就绪" 的新 [**SensorState**](/windows-hardware/drivers/ddi/sensorsclassextension/ne-sensorsclassextension-__midl___midl_itf_windowssensorclassextension_0000_0000_0001) 值发出信号 \_ \_ 。

## <a name="event-constants"></a>事件常量

传感器平台为驱动程序事件定义以下常量。

**传感器事件类型**

传感器平台定义以下传感器事件类型标识符。

| 名称 | 描述 |
| --- | --- |
| SENSOR_EVENT_DATA_UPDATED | 指示新数据可用。
| SENSOR_EVENT_PROPERTY_CHANGED| 指示属性值已更改。|
| SENSOR_EVENT_STATE_CHANGED| 指示操作状态的更改，例如，从 SENSOR_STATE_INITIALIZING 更改为 SENSOR_STATE_READY。|


**传感器事件 PROPERTYKEYs**

传感器平台定义了以下 **PROPERTYKEYs** 来识别传感器事件的参数。

| 名称 | 描述 |
| --- | --- |
| SENSOR_EVENT_PARAMETER_EVENT_ID| 指示 IPortableDeviceValues 中的 GUID 值是事件类型 ID，如 SENSOR_EVENT_DATA_UPDATED。|
| SENSOR_EVENT_PARAMETER_STATE| 指示 IPortableDeviceValues 中的无符号整数值为传感器状态，如 SENSOR_STATE_READY。<br>**注意** 若要引发状态更改事件，请调用 [ISensorClass 扩展：:P oststatechange](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)。 无需显式指定 SENSOR_EVENT_PARAMETER_STATE 引发事件。|

## <a name="other-events"></a>其他事件

传感器驱动程序通过调用传感器类扩展的 [**ISensorClassExtension：:P ostevent**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent) 方法来引发所有其他类型的事件。 此方法提供了一种通用的可扩展方法，用于引发与操作状态无关的传感器事件。 对 **PostEvent** 的每次调用都包含指向 [IPortableDeviceValuesCollection](https://go.microsoft.com/fwlink/p/?linkid=131487)的指针。 此集合中的每个[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)对象都包含 "传感器**GUID** \_ 事件 \_ 参数 \_ 事件 ID" \_ 属性（用于标识事件类型）和可选数据字段值（其中包含事件数据）的 GUID 值。 例如，具有新城市数据的 GPS 驱动程序将使用更新的传感器 \_ 事件 \_ 数据 \_ 事件 ID，并为传感器 \_ 数据 \_ 类型 \_ city 属性键提供一个字符串值。

驱动程序发布事件后，传感器类扩展会将事件和任何关联的数据转发到传感器 API。

可以在名为 "传感器" 的文件中找到平台定义的常量的定义。 有关平台定义的传感器常量的详细信息，请参阅 [常量](about-sensor-constants.md)。

## <a name="managing-sensor-driver-events"></a>管理传感器驱动程序事件

在您的驱动程序接受事件请求之前，它应创建一个单独的线程来生成和发布事件。 通过使用线程，可以帮助防止经常发生的事件过程阻止同步过程，例如数据请求回调。 有关引发数据更新事件的 thread 类的示例，请参阅 [引发数据更新事件](raising-events.md)。

仅当至少一个客户端应用程序请求了事件通知时，传感器才应引发事件。 当应用程序请求事件通知（包括状态更改事件）时，传感器类扩展会通过 [**ISensorDriver：： OnClientSubscribeToEvents**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)通知驱动程序。 此方法提供一个 [IWDFFile](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile) 指针，该指针标识应用程序和一个字符串，该字符串标识应用程序为其请求事件通知的传感器。 你可以使用 IWDFFile 指针作为唯一标识符，以帮助跟踪已订阅事件的应用程序。 尽管你的传感器无法向特定客户端发出事件，但你可能需要跟踪哪个应用程序设置了某些属性的值，如传感器 \_ 属性 \_ 当前 \_ 报表 \_ 间隔或传感器 \_ 属性 \_ 更改 \_ 敏感度。

例如，如果多个客户端应用程序为传感器 \_ 属性 "当前报表间隔" 设置不同的值 \_ \_ \_ ，则可以应用一条规则，将事件频率设置为请求的最短间隔。 但是，您的传感器可能需要在每次新客户端订阅事件或取消订阅现有客户端时调整时间间隔。 有关报表间隔的详细信息（包括代码示例），请参阅 [筛选数据](filtering-data.md)。

### <a name="sensor-events-and-data-privacy"></a>传感器事件和数据隐私

与其他数据请求类似，事件通知请求通过使用传感器类扩展来保证安全。 类扩展只允许请求此数据的用户的位置数据。

>[!CAUTION]
> 请确保使用传感器类扩展来处理传感器的所有 i/o 请求。 这样做将不太可能显示用户的隐私信息。

 

有关数据隐私的详细信息，请参阅 [传感器和位置平台中的隐私和安全](../gnss/privacy-and-security-in-the-sensor-and-location-platform.md)

## <a name="related-topics"></a>相关主题
[**传感器属性**](./sensor-properties.md)