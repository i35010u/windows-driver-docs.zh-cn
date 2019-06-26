---
Description: USB 函数类扩展 (UFX) 使用 WDF 对象功能来定义这些特定于 USB 的 UFX 对象。
title: USB 功能客户端驱动程序使用的 UFX 对象和句柄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c99693017de0ea34f12eed8c5c94213f75330ccd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368773"
---
# <a name="ufx-objects-and-handles-used-by-a-usb-function-client-driver"></a>USB 功能客户端驱动程序使用的 UFX 对象和句柄


**摘要**

-   UFX 对象由函数控制器驱动程序中用于处理传输在终结点。
-   这些对象是 WDF 对象的句柄，并且通过 UFX 创建客户端驱动程序的请求。 每个对象的生存期由 UFX 管理。

**适用于**

-   Windows 10

**上次更新时间**

-   2015 年 7 月

**重要的 API**

-   [**UfxDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicecreate)
-   [**UfxEndpointCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxendpointcreate)

USB 函数类扩展 (UFX) 使用 WDF 对象功能来定义这些特定于 USB 的 UFX 对象。

这些对象是 WDF 对象的句柄，并且通过 UFX 创建功能的客户端驱动程序的请求。 （可选） 客户端驱动程序可以与这些对象可以在创建时传递关联上下文。 创建 UFX 的每个 WDF 对象可能具有两个设备上下文：在对象创建时; 由 UFX 设置的一个设备上下文其他的设备上下文由客户端驱动程序传递和通过设置中 UFX [ **WdfObjectAllocateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectallocatecontext) WDF 对象创建后。

## <a name="usb-device-object"></a>USB 设备对象


**UFXDEVICE**

表示由控制器创建的 USB 设备。 该对象负责管理根据 USB 协议规范的 USB 状态以及管理与 USB 设备相关联的一个或多个终结点。 函数控制器驱动程序创建此对象内的[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)通过调用回调[ **UfxDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicecreate)方法。

[*EVT\_UFX\_设备\_主机\_连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)  
启动了与主机的连接。

[*EVT\_UFX\_设备\_主机\_断开连接*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)  
禁用与主机的函数控制器的通信。

[*EVT\_UFX\_DEVICE\_ADDRESSED*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_addressed)  
将分配函数控制器上的地址。

[*EVT\_UFX\_DEVICE\_ENDPOINT\_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)  
创建默认终结点对象。

[*EVT\_UFX\_DEVICE\_DEFAULT\_ENDPOINT\_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)  
创建默认终结点对象。

[*EVT\_UFX\_DEVICE\_USB\_STATE\_CHANGE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)  
更新的 USB 设备的状态。

[*EVT\_UFX\_设备\_端口\_更改*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_port_change)  
更新 USB 设备连接到的新端口的类型。

[*EVT\_UFX\_DEVICE\_PORT\_DETECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_port_detect)  
启动端口检测。

[*EVT\_UFX\_DEVICE\_REMOTE\_WAKEUP\_SIGNAL*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_remote_wakeup_signal)  
启动远程唤醒函数控制器上。

[*EVT\_UFX\_DEVICE\_DETECT\_PROPRIETARY\_CHARGER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_detect)  
启动专有充电器检测。

[*EVT\_UFX\_DEVICE\_PROPRIETARY\_CHARGER\_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_reset)  
重置专有充电器。

[*EVT\_UFX\_设备\_专有\_充电器\_设置\_属性*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_set_property)  
设置用于启用通过 USB 充电的充电器信息。

## <a name="usb-endpoint-object"></a>USB 终结点对象


**UFXENDPOINT**

表示主机和设备之间的逻辑连接。 该对象负责与主机的数据传输。 为每个设备对象可以有一个或多个终结点。 默认终结点始终控制终结点，而 rest 则类驱动程序特定对象。 函数控制器驱动程序创建中的对象[ *EVT\_UFX\_设备\_终结点\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)回调通过调用[ **UfxEndpointCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxendpointcreate)方法。

## <a name="related-topics"></a>相关主题
[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)  



