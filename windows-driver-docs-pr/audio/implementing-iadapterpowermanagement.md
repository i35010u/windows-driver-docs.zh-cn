---
title: 实现 IAdapterPowerManagement
description: 实现 IAdapterPowerManagement
ms.assetid: 654b86a7-845c-415b-99e4-c7be92cb9b9c
keywords:
- IAdapterPowerManagement
- 适配器驱动程序 WDK 音频，电源管理
- 音频适配器驱动程序 WDK、 电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0842559071363d3b53072d8b6326082b65d4a32f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333635"
---
# <a name="implementing-iadapterpowermanagement"></a>实现 IAdapterPowerManagement


## <span id="implementing_iadapterpowermanagement"></span><span id="IMPLEMENTING_IADAPTERPOWERMANAGEMENT"></span>


在实现时[IAdapterPowerManagement](https://msdn.microsoft.com/library/windows/hardware/ff536485)您的驱动程序的接口，请参阅的实现**CAdapterCommon**类中的示例音频驱动程序在 Microsoft Windows 驱动程序工具包 （WDK)。 此类处理设备中断并执行通用音频适配器的所有驱动程序的其他功能。 您的适配器**CAdapterCommon**类应继承自**IAdapterPowerManagement**接口，并支持此接口在其**NonDelegatingQueryInterface**方法。 (有关 nondelegating 接口的详细信息，请参阅的说明**INonDelegatingUnknown**接口。)

可以使用 IMP\_IAdapterPowerManagement 定义与标头文件添加的函数声明的 Portcls.h [ **IAdapterPowerManagement::PowerChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff536488)， [**IAdapterPowerManagement::QueryPowerChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff536490)，和[ **IAdapterPowerManagement::QueryDeviceCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff536489)方法为您的驱动程序**CAdapterCommon**类定义。

适配器的设备启动例程 PortCls 系统驱动程序的调用 (请参阅[启动设备](https://msdn.microsoft.com/library/windows/hardware/ff563849))，适配器应注册其**IAdapterPowerManagement** PortCls 接口通过调用[ **PcRegisterAdapterPowerManagement**](https://msdn.microsoft.com/library/windows/hardware/ff537724)。 有关代码示例，请参阅**StartDevice** Sb16 示例适配器驱动程序在 WDK 中的函数。 **PcRegisterAdapterPowerManagement**函数的第一个参数是**IUnknown**指向适配器驱动程序**CAdapterCommon**对象。 此对象查询 PortCls 及其**IAdapterPowerManagement**接口。

当 PortCls 调用适配器驱动程序**IAdapterPowerManagement::PowerChangeState**方法来更改设备的电源状态，则适配器驱动程序应缓存在适配器中的设备的新电源状态**CAdapterCommon**对象。 期间**CAdapterCommon::Init**调用 （请参阅 WDK 示例适配器驱动程序中的实现），该驱动程序应将初始电源状态设置为 PowerDeviceD0 (中所述[DeviceState](https://msdn.microsoft.com/library/windows/hardware/ff543087)) 之前返回从成功初始化。 仅当已知要处于相应的电源状态，驱动程序应该写入硬件。 在 WDK 中的 Sb16 示例驱动程序，例如，驱动程序将写入到仅在 PowerDeviceD0 状态中的硬件。

之前关闭响应**PowerChangeState**调用时，适配器驱动程序应置于音频输出演讲者干扰可防止发生的电源开关时的状态。 例如，关闭过程中可能包括比较 DAC 输出到零，关闭 Dac，并静音 MIDI 行。

 

 




