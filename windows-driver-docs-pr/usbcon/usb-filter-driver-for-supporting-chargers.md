---
Description: 有关在函数控制器支持 USB 充电器
title: 支持 USB 充电器的 USB 筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fea9c84554a959cfd0734a9fcf5d66916521cfd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356592"
---
# <a name="usb-filter-driver-for-supporting-usb-chargers"></a>支持 USB 充电器的 USB 筛选器驱动程序

编写函数控制器使用现成 Synopsys 支持检测的充电器，筛选器驱动程序和 ChipIdea 驱动程序。 在客户端驱动程序中集成附加充电器/检测的专有函数控制器编写客户端驱动程序，如果通过实现[EVT_UFX_DEVICE_PROPRIETARY_CHARGER_SET_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_set_property)， [EVT_UFX_DEVICE_PROPRIETARY_CHARGER_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_reset)，并[EVT_UFX_DEVICE_DETECT_PROPRIETARY_CHARGER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_detect)。

USB 函数堆栈允许设备，例如电话或平板电脑，收费时连接到主机和 USB 充电 USB 电池充电 (BC) 1.2 规范定义。 

- 有两种类型的端口的设备可以使用针对向收费。 在设备上随设备附带的充电器充电的专用端口 (DCP) 从收费。 或者，设备可以从标准下游端口或在设备连接到 PC 时计费下游端口。 这种情况下都符合[USB BC 1.2 规范](https://www.usb.org/developers/docs/devclass_docs/USB_Battery_Charging_1.2.pdf)。 
- 某些充电器不符合规范。 USB 函数堆栈允许设备将从这些专有 USB 充电器充电。 

若要支持符合规范的和专有充电器，这些操作是必需的。 

- 设备能够检测到的 USB 主机时或附加或分离充电器。 
- 设备是能够检测到不同的 USB 充电 BC 1.2 规范定义的端口。 
- USB 的充电器所定义的业务连续性 1.2 规范，与当前允许的 BC 1.2 规范的最大数量的设备费用。 
- 设备是能够检测到专有 USB 充电器。 
- 对于专有 USB 充电器，确定的设备可以绘制最新的最大数量。 
- 通知操作系统有关的 USB 端口类型的连接。 
- 阻止设备通过 USB 在 OS 中提取当前即使 USB 主机已连接，并且设备已配置本身与主机。 

这些操作由处理[USB 函数类扩展 (UFX) / 客户端驱动程序](developing-windows-drivers-for-usb-function-controllers.md)对和加载为 USB 函数设备堆栈中较低的筛选器的筛选器驱动程序。 该驱动程序管理 USB 充电启动从 USB 端口检测到它可以开始收费和设备可以绘制当前的最长时通知电池堆栈。 

下面是设备堆栈的体系结构表示形式。

![USB 充电](images/charger.png)

当 USB 端口连接到设备时，客户端驱动程序获取通知，通过较低的筛选器驱动程序或中断。 在此期间，客户端驱动程序通过使用 USB 硬件进行通信来执行端口检测并报告给 UFX 的端口类型。 或者，它可以请求筛选器驱动程序。 在这种情况下，筛选器驱动程序协调与 USB 硬件执行 USB 端口检测，并返回到客户端驱动程序和客户端驱动程序检测到的端口类型将其传递给 UFX。 

UFX 根据端口类型，确定当前设备可以绘制，然后将该信息发送到充电聚合驱动程序 (CAD) 的最大数量。 CAD 验证的信息。 如果当前有效，CAD 将请求发送到电池类驱动程序，即开始到指定的最大当前计费。 电池类驱动程序充电将请求转发到电池 miniclass 驱动程序进行处理。 如果计费请求指定专有充电器已附加和电池 miniclass 处理专有充电器，miniclass 驱动程序可以尝试使用它确定合适的最大当前收取费用。 否则，电池 miniclass 可以仅由指定的 CAD 的最大当前收费。

