---
title: 有关 ISensorDriver
description: 有关 ISensorDriver
ms.assetid: 2c51c235-e402-4f89-bff5-39af87d95e19
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0e56cb8067e009a760f6f6edaf87836d03fa3d9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525087"
---
# <a name="about-isensordriver"></a>有关 ISensorDriver


传感器驱动程序必须实现[ISensorDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nn-sensorsclassextension-isensordriver)接口。 通过此接口，该驱动程序提供有关哪些传感器类型、 属性、 数据字段和事件支持传感器，以及实际的属性值和传感器数据的信息。 类扩展调用回调方法来处理 I/O 请求，以指定的属性的 API 层请求，来管理客户端连接，并订阅事件的列表。

## <a name="method-to-enumerate-sensors"></a>方法用于枚举传感器

类扩展将始终首先通过调用枚举设备可用的传感器[ **ISensorDriver::OnGetSupportedSensorObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedsensorobjects)。 对于每个传感器，您的驱动程序必须返回[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)对象，其中包含字符串 ID （唯一的设备） 和其他必需的属性值。

## <a name="methods-to-manage-client-connections"></a>方法，用于管理客户端连接

为了通知客户端应用程序的连接和断开连接，传感器类扩展的驱动程序将调用[ **ISensorDriver::OnClientConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientconnect)并[ **ISensorDriver::OnClientDisconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientdisconnect)。 这些回调方法传递两个参数： 一个指向[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)接口和传感器 id。 您的驱动程序应使用唯一的 ID 作为此接口指针来表示每个客户端应用程序。 传感器 ID 包含一个字符串，标识客户端希望连接或断开连接的传感器。 这些值非常有用，因为你可能想要维护客户端和与其连接，以便你可以管理传感器上的设置的传感器的列表。 例如，你可能如何设置当前报告间隔时从多个客户端提供冲突的值的启发式方法。 此外可以使用此信息做出有关电源管理。 例如，如果没有客户端连接，您可以将传感器硬件放入节能模式。

## <a name="methods-to-manage-event-subscribers"></a>方法，用于管理事件订阅服务器

传感器类扩展调用方法，以帮助管理事件的客户端应用程序。 [**ISensorDriver::OnGetSupportedEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)检索驱动程序可以引发的事件的列表。 [**ISensorDriver::OnClientSubscribeToEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientsubscribetoevents)并[ **ISensorDriver::OnClientUnsubscribeFromEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onclientunsubscribefromevents)提供驱动程序特定的通知应用程序已请求可以接收或取消事件通知。 只有已连接的客户端可以订阅或取消订阅事件。

## <a name="methods-to-manage-data-and-properties"></a>方法，用于管理数据和属性

客户端应用程序还可以检索为传感器数据**数据字段**，或**属性**其中包含有关传感器设备的元数据。 若要检索的受支持的数据字段或属性的列表，传感器类扩展调用[ **ISensorDriver::OnGetSupportedDataFields** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupporteddatafields)或[ **ISensorDriver::OnGetSupportedProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedproperties)。 若要检索的数据字段或属性值，类扩展调用[ **ISensorDriver::OnGetDataFields** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetdatafields)或[ **ISensorDriver::OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties). 有关可以设置属性，类扩展调用[ **ISensorDriver::OnSetProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onsetproperties)提供新的属性值。

## <a name="methods-to-manage-wpd-commands"></a>方法，用于管理 WPD 命令

传感器类扩展时收到通过 I/O 控制命令[ **ISensorClassExtension::ProcessIoControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-processiocontrol)对于其中它不提供一个处理程序，它调用[ **ISensorDriver::OnProcessWpdMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-onprocesswpdmessage)。 此回调方法发出信号，驱动程序，WPD 命令尚未处理，并使该驱动程序有机会处理命令。 这意味着您可以创建自定义 WPD 命令和驱动程序，以扩展传感器平台功能中提供自定义处理程序。

 

 




