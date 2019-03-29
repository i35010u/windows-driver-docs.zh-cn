---
Description: UCX manages the creation of endpoint objects, and notifies the host controller to program or deprogram endpoints into the USB host controller.
title: 在 USB 主控制器驱动程序中配置 USB 终结点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29d469172f86af57ac941a33bdb8f94da19e0c4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567401"
---
# <a name="configure-usb-endpoints-in-a-usb-host-controller-driver"></a>在 USB 主控制器驱动程序中配置 USB 终结点


UCX 管理终结点对象的创建，并通知主机控制器进行编程或 USB 主控制器到 deprogram 终结点。

尽管终结点进行编程，它还由 UCX 管理。 终结点更改的状态为设备连接到和总线，从断开连接体验的 power 事件如挂起和重置，并且接受新创建的终结点，例如备用设置更改。

## <a name="endpoint-configuration"></a>终结点配置


UCX 调用由主机控制器驱动程序，以通知驱动程序时终结点必须编程到 USB 主控制器，或释放实现的回调函数。 当[ *EVT\_UCX\_USBDEVICE\_启用*](https://msdn.microsoft.com/library/windows/hardware/mt187841)是调用，该驱动程序执行到设备的默认终结点的传输中准备控制器。 准备在控制器包括编程的默认终结点。 当[ *EVT\_UCX\_USBDEVICE\_禁用*](https://msdn.microsoft.com/library/windows/hardware/mt187840)是调用，该驱动程序 deprograms 默认终结点并释放与关联的其他控制器资源设备。 当[ *EVT\_UCX\_USBDEVICE\_终结点\_配置*](https://msdn.microsoft.com/library/windows/hardware/mt187842)是调用，该驱动程序提供的非默认终结点进行编程到列表在控制器和给定的非默认终结点以从控制器中删除另一个列表。 主机控制器驱动程序到控制器，然后程序指定非默认终结点，还从控制器中删除 （在其他列表中指定） 的非默认终结点。

## <a name="queue-state-management"></a>队列状态管理


UCX 调用回调函数实现的主机控制器驱动程序来执行对终结点队列状态的更改。 该驱动程序然后将相应的操作即可提供给 UCX，终结点队列和驱动程序中维护任何第二个级别队列上。 终结点队列被中止，或在这些情况下清除：

-   USB 设备客户端驱动程序将发送 URB\_函数\_中止\_管道请求。
-   在挂起。
-   当设备连接到，在中心检测到设备断开连接。
-   在选择界面设置请求。

若要通知的队列中止或清除有关主机控制器驱动程序，UCX 调用[ *EVT\_UCX\_终结点\_中止*](https://msdn.microsoft.com/library/windows/hardware/mt187825)或[ *EVT\_UCX\_终结点\_清除*](https://msdn.microsoft.com/library/windows/hardware/mt187827)。 如果在以后某个时刻终结点队列所需的 UCX，然后 UCX 调用[ *EVT\_UCX\_终结点\_启动*](https://msdn.microsoft.com/library/windows/hardware/mt187829)回调，从而通知要启动的驱动程序队列。

## <a name="transfer-cancellation"></a>传输取消


任何控制器主机控制器驱动程序为其声明 GUID\_USB\_功能\_清除\_TT\_缓冲区\_ON\_异步\_传输\_取消，该驱动程序必须调用[ **UcxEndpointNeedToCancelTransfers** ](https://msdn.microsoft.com/library/windows/hardware/mt188042)并实现[ *EVT\_UCX\_终结点\_确定\_TO\_取消\_传输*](https://msdn.microsoft.com/library/windows/hardware/mt187826)用于取消异步 （大容量或控件） USB 传输，到完全 USB 或位于低速设备事务转换器 (TT) 中心。 在所有其他情况下，该驱动程序可以选择调用**UcxEndpointNeedToCancelTransfers**若要获取*EVT\_UCX\_终结点\_确定\_TO\_取消\_传输*通知，指示此终结点上允许，正在取消传输和驱动程序可以继续将取消传输。 或者，驱动程序可以取消传输，而无需调用直接**UcxEndpointNeedToCancelTransfers**。

如果主机控制器驱动程序始终失败的请求此 GUID，它可以完全忽略这些两个函数调用。

如果该驱动程序永远不会调用[ **UcxEndpointNeedToCancelTransfers**](https://msdn.microsoft.com/library/windows/hardware/mt188042)，在驱动程序[ *EVT\_UCX\_终结点\_确定\_向\_取消\_传输*](https://msdn.microsoft.com/library/windows/hardware/mt187826)回调不会调用和回调注册期间可以为 NULL。

如果打算使用该驱动程序[ **UcxEndpointNeedToCancelTransfers**](https://msdn.microsoft.com/library/windows/hardware/mt188042)，驱动程序必须调用到控制器进行编程，然后取消了传输时，该方法然后等待[ *EVT\_UCX\_终结点\_确定\_TO\_取消\_传输*](https://msdn.microsoft.com/library/windows/hardware/mt187826)之前完成它。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)  



