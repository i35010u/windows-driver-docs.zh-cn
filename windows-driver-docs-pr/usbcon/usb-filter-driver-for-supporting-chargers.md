---
description: 支持函数控制器的 USB 充电器
title: 支持 USB 充电器的 USB 筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d663f2ab584bf929fa1230818c014f22ca92730
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968628"
---
# <a name="usb-filter-driver-for-supporting-usb-chargers"></a>支持 USB 充电器的 USB 筛选器驱动程序

如果函数控制器使用机箱中的 Synopsys 和 ChipIdea 驱动程序，则编写支持检测充电器的筛选器驱动程序。 如果要为专用功能控制器编写客户端驱动程序，通过实现 [EVT_UFX_DEVICE_PROPRIETARY_CHARGER_SET_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_set_property)、 [EVT_UFX_DEVICE_PROPRIETARY_CHARGER_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_reset)和 [EVT_UFX_DEVICE_DETECT_PROPRIETARY_CHARGER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_detect)，可以在客户端驱动程序中集成 "充电器/附加检测"。

USB 函数堆栈允许设备（如电话或平板电脑）在连接到由 USB 电池充电 (BC) 1.2 规范定义的主机和 USB 充电器时进行收费。 

- 设备可用于充电两种类型的端口。 设备可以从设备附带的充电器)  (DCP 进行收费。 或者，在设备连接到 PC 时，该设备可以从标准下游端口或向下游端口充电。 这两种情况都符合 [USB BC 1.2 规范](https://www.usb.org/developers/docs/devclass_docs/USB_Battery_Charging_1.2.pdf)。 
- 某些充电器不遵循规范。 USB 函数堆栈允许设备从这些专用 USB 充电器中收取费用。 

若要支持符合规范和专用的充电器，需要执行这些操作。 

- 设备能够检测连接或断开 USB 主机或充电器的时间。 
- 设备能够检测 BC 1.2 规范定义的不同 USB 充电端口。 
- 对于由 BC 1.2 规范定义的 USB 充电器，设备会按 BC 1.2 规范允许的最大当前数量收费。 
- 设备能够检测专用 USB 充电器。 
- 对于专用 USB 充电器，确定设备可绘制的最大当前数量。 
- 通知操作系统有关连接的 USB 端口类型。 
- 即使连接了 USB 主机并且设备自行配置了主机，也会阻止设备在操作系统中通过 USB 拉取电流。 

这些操作由 [usb 函数类扩展处理 (UFX) /client 驱动程序](developing-windows-drivers-for-usb-function-controllers.md) 对和在 USB function 设备堆栈中加载为较低筛选器的筛选器驱动程序。 驱动程序管理从 USB 端口检测开始的 USB 充电，以便在电池堆栈可以开始充电时通知电池堆栈，并且设备可绘制的最大电流量。 

下面是设备堆栈的结构表示形式。

![USB 充电](images/charger.png)

将 USB 端口连接到设备后，客户端驱动程序将获得由较低筛选器驱动程序或中断通知。 目前，客户端驱动程序通过与 USB 硬件通信来执行端口检测，并向 UFX 报告端口类型。 或者，它可以请求筛选器驱动程序。 在这种情况下，筛选器驱动程序与 USB 硬件协调以执行 USB 端口检测，并将检测到的端口类型返回到客户端驱动程序，客户端驱动程序将它传递给 UFX。 

根据端口类型，UFX 确定设备可绘制的最大当前数量，并将该信息发送给计费聚合驱动程序 (CAD) 。 CAD 验证信息。 如果当前有效，则 CAD 会将请求发送到电池类驱动程序，开始充电到指定的最大电流。 电池类驱动程序将充电请求转发给电池 miniclass 驱动程序进行处理。 如果充电请求指定了专有充电器已附加，并且电池 miniclass 处理专用的充电器，则 miniclass 驱动程序可以尝试根据它确定的最大电流进行收费。 否则，电池 miniclass 只能向 CAD 指定的最大值收费。

