---
Description: The client driver can participate in the policy decisions for USB Type-C connectors.
title: 写入 USB 类型 C 策略管理器客户端驱动程序
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: cd587e74ed4541f06974a0b4fda43f740315677b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555653"
---
# <a name="write-a-usb-type-c-policy-manager-client-driver"></a>写入 USB 类型 C 策略管理器客户端驱动程序

提供 Microsoft USB 类型 C 策略管理器监视 USB 类型 C 连接器的活动。 Windows，版本 1809，引入了一组编程接口，可用于编写到策略管理器中的客户端驱动程序 (称为_PM 客户端驱动程序_本主题中)。 客户端驱动程序可以参与 USB 类型 C 连接器的策略决策。 此设置后，你可以选择要写入的内核模式导出驱动程序或用户模式驱动程序。

策略管理器获取和协调从 USB 连接器管理器 (UCM)、 USB 主控制器和 USB 函数和 PM 客户端驱动程序的信息。 当需要 UI 通知时，策略管理器将请求发送到系统外壳。

![Architechtural 框图 USB 策略管理器](images/pmclient.png)

有关驱动程序的完整视图，请参阅[体系结构：Windows 系统的 USB 类型 C 设计](https://docs.microsoft.com/windows-hardware/drivers/usbcon/architecture--usb-type-c-in-a-windows-system)。

## <a name="important-apis"></a>重要的 API
PM Api 中声明[Usbpmapi.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi)标头。
 
## <a name="1-client-registration"></a>1：客户端注册

1. 客户端驱动程序调用[ **UsbPm_Register** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_register)注册驱动程序的回调函数。
2. 客户端驱动程序将等待一个事件从策略管理器。 
    > 成功**UsbPm_Register**调用并不能保证客户端驱动程序已请求访问。 准备就绪，策略管理器时，驱动程序的[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)获取调用使用了**PolicyManagerArrival**作为指示的实际事件数据授予访问权限。
3. **UsbPm_Register**调用返回的注册句柄。
    > 客户端驱动程序可能会收到**EVT_USBPM_EVENT_CALLBACK**甚至之前**UsbPm_Register**返回。

## <a name="2-hub-arrival"></a>2：中心到达

1. 当 UCMCX 设备到达时，策略管理器会通知和跟踪的每个中心上的所有连接器的属性和状态以及所有中心句柄。
2. 客户端驱动程序[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)获取调用使用了**HubArrivalRemoval**作为事件数据。 在调用还包含中心句柄。
3. 在客户端驱动程序的实现中的**EVT_USBPM_EVENT_CALLBACK**，驱动程序调用[ **UsbPm_RetrieveHubProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrievehubproperties)的中心，获取连接器数然后调用[ **UsbPm_RetrieveConnectorProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)并[ **UsbPm_RetrieveConnectorState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorstate)可获得更多功能有关每个连接器的信息。

## <a name="3-connector-state-change"></a>3：连接器的状态更改 
1. 由于连接器状态更改，例如，键入 C 附加/分离，PD 协定协商，策略管理器更新的每个连接器状态信息。 
2. 客户端驱动程序[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)获取调用使用了**ConnectorStateChange**作为事件数据。 在调用还包含连接器句柄。
3. 客户端驱动程序的完成例程还调用，并相应地采取操作。
4. 在客户端驱动程序的实现中的**EVT_USBPM_EVENT_CALLBACK**，驱动程序调用[ **UsbPm_RetrieveConnectorProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)。 使用给定的连接器句柄 driverto 获取最新的连接器状态、 对其进行检查，可能决定更新其本地副本。  
 
## <a name="4-change-initiated-by-the-client-driver"></a>4:更改由客户端驱动程序启动

1. 若要请求更改客户端驱动程序调用[ **UsbPm_AssignConnectorPowerLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_assignconnectorpowerlevel)。
    > 客户端驱动程序可能会调用此函数中的**EVT_USBPM_EVENT_CALLBACK**注册使用回调**UsbPm_Register**。

2. 策略管理器将请求转发到 USB 连接器管理器 (UCM)。 UcmCx 的客户端驱动程序采取相应的措施，以更改请求的状态。
3. 客户端驱动程序[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)获取调用使用了**ConnectorStateChange**作为事件数据。 在调用还包含连接器句柄。
4. 客户端驱动程序的完成例程还调用，并相应地采取操作。
5. 在回调中，客户端驱动程序调用[ **UsbPm_RetrieveConnectorState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)与给定的连接器句柄以获取最新的连接器状态，对其进行检查，并可能会决定更新其本地副本。

 
## <a name="5-hub-removal"></a>5:中心删除

1. UCM 通知策略管理器删除 UcmCx 设备 （不 UcmCx 设备上单个连接器） 时。 策略管理器从其中心集合中移除该中心。
2. 客户端驱动程序[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)实现获取调用使用了**HubRemoval**作为事件数据。 在调用还包含中心句柄。
3. 在客户端驱动程序的实现中的**EVT_USBPM_EVENT_CALLBACK**，客户端驱动程序执行的清理任务为中心和要删除的连接器。 该驱动程序可以调用[ **UsbPm_RetrieveHubProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrievehubproperties)并[ **UsbPm_RetrieveConnectorProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)获取中心的属性和连接器。
 
## <a name="6-client-deregistration"></a>6:客户端注销 
1. 客户端驱动程序调用[ **UsbPm_Deregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_register)驱动程序不再需要的任何通知。
2. 策略管理器将客户端句柄注册标记为取消注册并不会调用**EVT_USBPM_EVENT_CALLBACK**回调。

## <a name="see-also"></a>另请参阅

[编写 USB 类型 C 连接器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)

[写入 USB 类型 C 端口控制器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-usb-type-c-port-controller-driver)

[编写函数 USB 控制器客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/function-client-driver)
