---
title: 关于 ISensorDriver
description: 关于 ISensorDriver
ms.assetid: 2c51c235-e402-4f89-bff5-39af87d95e19
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: a9eefc1906a8cb2656fdf4bef40fc92e2e9c46c9
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009871"
---
# <a name="about-isensordriver"></a>关于 ISensorDriver


传感器驱动程序必须实现 [ISensorDriver](/windows-hardware/drivers/ddi/sensorsclassextension/nn-sensorsclassextension-isensordriver) 接口。 通过此接口，驱动程序提供有关传感器支持哪些传感器类型、属性、数据字段和事件以及实际属性值和传感器数据的信息。 类扩展调用回调方法来处理 i/o 请求、指定 API 层请求的属性列表、管理客户端连接以及订阅事件。

## <a name="method-to-enumerate-sensors"></a>枚举传感器的方法

类扩展将始终先通过调用 [**ISensorDriver：： OnGetSupportedSensorObjects**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedsensorobjects)枚举设备的可用传感器。 对于每个传感器，驱动程序必须返回一个 [IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486) 对象，该对象包含) 设备和其他必需属性值 (唯一的字符串 ID。

## <a name="methods-to-manage-client-connections"></a>用于管理客户端连接的方法

为了通知驱动程序连接和断开连接的客户端应用程序，传感器类扩展调用 [**ISensorDriver：： OnClientConnect**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientconnect) 和 [**ISensorDriver：：传感器**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientdisconnect)。 这些回调方法传递两个参数：指向 [IWDFFile](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile) 接口和传感器 ID 的指针。 驱动程序应使用此接口指针作为唯一 ID 来表示每个客户端应用程序。 传感器 ID 包含一个字符串，该字符串用于标识客户端想要连接或断开连接到的传感器。 这些值非常有用，因为您可能需要维护客户端及其连接到的传感器的列表，以便您可以管理传感器上的设置。 例如，如果给定多个客户端的冲突值，则可以使用试探法来设置当前报表时间间隔。 你还可以使用此信息来做出有关电源管理的决策。 例如，如果未连接任何客户端，则可以将传感器硬件置于省电模式。

## <a name="methods-to-manage-event-subscribers"></a>用于管理事件订阅服务器的方法

传感器类扩展调用方法来帮助客户端应用程序管理事件。 [**ISensorDriver：： OnGetSupportedEvents**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents) 检索驱动程序可以引发的事件列表。 [**ISensorDriver：： OnClientSubscribeToEvents**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents) 和 [**ISensorDriver：： OnClientUnsubscribeFromEvents**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientunsubscribefromevents) 在特定应用程序请求接收或取消事件通知时向驱动程序提供通知。 只有已连接的客户端才能订阅或取消订阅事件。

## <a name="methods-to-manage-data-and-properties"></a>用于管理数据和属性的方法

客户端应用程序还可以将传感器数据作为 **数据字段**或包含有关传感器设备的元数据的 **属性** 进行检索。 若要检索支持的数据字段或属性的列表，传感器类扩展将调用 [**ISensorDriver：： OnGetSupportedDataFields**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupporteddatafields) 或 [**ISensorDriver：： OnGetSupportedProperties**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedproperties)。 若要检索数据字段或属性值，类扩展将调用 [**ISensorDriver：： OnGetDataFields**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields) 或 [**ISensorDriver：： OnGetProperties**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)。 对于可以设置的属性，类扩展将调用 [**ISensorDriver：： OnSetProperties**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onsetproperties) 以提供新的属性值。

## <a name="methods-to-manage-wpd-commands"></a>用于管理 WPD 命令的方法

当传感器类扩展通过 [**ISensorClassExtension：:P rocessiocontrol**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-processiocontrol) 接收到不提供处理程序的 i/o 控制命令时，它将调用 [**ISensorDriver：： OnProcessWpdMessage**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-onprocesswpdmessage)。 此回调方法发出信号，指示驱动程序未处理 WPD 命令，并为驱动程序提供处理命令的机会。 这意味着，你可以创建自定义 WPD 命令，并在驱动程序中提供自定义处理程序，以扩展传感器平台功能。

 

