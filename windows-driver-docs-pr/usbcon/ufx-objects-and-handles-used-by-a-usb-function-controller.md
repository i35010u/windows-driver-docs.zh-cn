---
description: USB 函数类扩展 (UFX) 使用 WDF 对象功能来定义这些特定于 USB 的 UFX 对象。
title: USB 功能客户端驱动程序使用的 UFX 对象和句柄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb8ffb38824cefa0256cc9397c4615b0b5d7cdec
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009791"
---
# <a name="ufx-objects-and-handles-used-by-a-usb-function-client-driver"></a>USB 功能客户端驱动程序使用的 UFX 对象和句柄


**摘要**

-   函数控制器驱动程序使用 UFX 对象来处理与终结点之间的传输。
-   这些对象是 WDF 对象的句柄，由 UFX 在客户端驱动程序请求时创建。 每个对象的生存期由 UFX 管理。

**适用于**

-   Windows 10

**上次更新时间**

-   2015 年 7 月

**重要的 API**

-   [**UfxDeviceCreate**](/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicecreate)
-   [**UfxEndpointCreate**](/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointcreate)

USB 函数类扩展 (UFX) 使用 WDF 对象功能来定义这些特定于 USB 的 UFX 对象。

这些对象是 WDF 对象的句柄，由 UFX 在函数客户端驱动程序请求时创建。 （可选）客户端驱动程序可以将上下文与可以在创建时传递的这些对象相关联。 UFX 创建的每个 WDF 对象可能有两个设备上下文：在对象创建时由 UFX 设置的一个设备上下文;由客户端驱动程序传入的其他设备上下文，在 WDF 对象创建后使用 [**WdfObjectAllocateContext**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext) 在 UFX 中进行设置。

## <a name="usb-device-object"></a>USB 设备对象


**UFXDEVICE**

表示由控制器创建的 USB 设备。 对象负责根据 USB 协议规范管理 USB 状态，并管理与 USB 设备关联的一个或多个终结点。 函数控制器驱动程序通过调用[**UfxDeviceCreate**](/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicecreate)方法在[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调中创建此对象。

[*.EVT \_ UFX \_ 设备 \_ 主机 \_ 连接*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)  
启动与主机的连接。

[*.EVT \_ UFX \_ 设备 \_ 主机 \_ 断开连接*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)  
禁用函数控制器与宿主的通信。

[*.EVT \_ UFX \_ 设备 \_ 寻址*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_addressed)  
在函数控制器上分配一个地址。

[*.EVT \_ UFX \_ 设备 \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)  
创建默认终结点对象。

[*.EVT \_ UFX \_ 设备 \_ 默认 \_ 终结点 \_ 添加*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)  
创建默认终结点对象。

[*.EVT \_ UFX \_ 设备 \_ USB \_ 状态 \_ 更改*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)  
更新 USB 设备的状态。

[*.EVT \_ UFX \_ 设备 \_ 端口 \_ 更改*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change)  
更新 USB 设备连接到的新端口的类型。

[*.EVT \_ UFX \_ 设备 \_ 端口 \_ 检测*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_detect)  
启动端口检测。

[*.EVT \_ UFX \_ 设备 \_ 远程 \_ 唤醒 \_ 信号*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_remote_wakeup_signal)  
在函数控制器上启动远程唤醒。

[*.EVT \_ UFX \_ 设备 \_ 检测 \_ 专有 \_ 充电器*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_detect)  
启动专有充电器检测。

[*.EVT \_ UFX \_ 设备 \_ 专有 \_ 充电器 \_ 重置*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_reset)  
重置专用充电器。

[*.EVT \_ UFX \_ 设备 \_ 专有 \_ 充电器 \_ 集 \_ 属性*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_set_property)  
设置用于启用通过 USB 进行充电的充电器信息。

## <a name="usb-endpoint-object"></a>USB 终结点对象


**UFXENDPOINT**

表示主机与设备之间的逻辑连接。 对象负责将数据传入/传出主机。 对于每个设备对象，可以有一个或多个终结点。 默认终结点始终是控件终结点，rest 是类驱动程序特定的对象。 函数控制器驱动程序通过调用[**UfxEndpointCreate**](/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointcreate)方法在[*.Evt \_ UFX \_ 设备 \_ 终结 \_ 点*](/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)中创建对象。

## <a name="related-topics"></a>相关主题
[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)