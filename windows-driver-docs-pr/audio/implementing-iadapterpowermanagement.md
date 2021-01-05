---
title: 实现 IAdapterPowerManagement
description: 实现 IAdapterPowerManagement
keywords:
- IAdapterPowerManagement
- 适配器驱动程序 WDK 音频，电源管理
- 音频适配器驱动程序 WDK，电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0120dcab9356f4d253d1f1b6f0e3e369d7974a4b
ms.sourcegitcommit: 7bdf85c72841fbc2093c315f900c69d2eef6e3e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2020
ms.locfileid: "97757878"
---
# <a name="implementing-iadapterpowermanagement"></a>实现 IAdapterPowerManagement


## <span id="implementing_iadapterpowermanagement"></span><span id="IMPLEMENTING_IADAPTERPOWERMANAGEMENT"></span>


为驱动程序实现 [IAdapterPowerManagement](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement) 接口时，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 中的示例音频驱动程序中的 **CAdapterCommon** 类的实现。 此类处理设备中断，并执行所有音频适配器驱动程序共用的其他功能。 适配器的 **CAdapterCommon** 类应继承自 **IAdapterPowerManagement** 接口，并支持其 **NonDelegatingQueryInterface** 方法中的此接口。 有关 nondelegating 接口的详细信息，请参阅 **INonDelegatingUnknown** 接口的说明。 )  (

可以使用 \_ 标头文件 Portcls 中的 IMP IAdapterPowerManagement 定义将 [**IAdapterPowerManagement：:P owerchangestate**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-powerchangestate)、 [**IAdapterPowerManagement：： QueryPowerChangeState**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-querypowerchangestate)和 [**IAdapterPowerManagement：： QueryDeviceCapabilities**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-querydevicecapabilities) 方法的函数声明添加到驱动程序的 **CAdapterCommon** 类定义。

在 PortCls 系统驱动程序调用适配器的设备启动例程期间 (参阅 [启动设备](../kernel/starting-a-device.md)) ，适配器应通过调用 [**PcRegisterAdapterPowerManagement**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)向 PortCls 注册其 **IAdapterPowerManagement** 接口。 有关代码示例，请参阅 Sysvad 示例驱动程序中的 **StartDevice** 函数，如 [示例音频驱动](sample-audio-drivers.md)程序中所述。 **PcRegisterAdapterPowerManagement** 函数的第一个参数是指向适配器驱动程序的 **CAdapterCommon** 对象的 **IUnknown** 指针。 PortCls 查询此对象的 **IAdapterPowerManagement** 接口。

当 PortCls 调用适配器驱动程序的 **IAdapterPowerManagement：:P owerchangestate** 方法更改设备的电源状态时，适配器驱动程序应在适配器的 **CAdapterCommon** 对象中缓存设备的新电源状态。 在 **CAdapterCommon：： Init** 调用期间 (查看在 WDK 的示例适配器驱动程序) 的实现，驱动程序应将初始电源状态设置为 [DeviceState](../kernel/devicestate.md)) 中描述的 PowerDeviceD0 (，然后再从成功的初始化中返回。 仅当已知设备处于适当的电源状态时，驱动程序才能写入硬件。 

在关闭以响应 **PowerChangeState** 呼叫之前，适配器驱动程序应将音频输出置于防止扬声器噪音在电源开关关闭时出现的状态。 例如，关闭过程可能包括将 DAC 输出斜向零旋转、关闭 Dac 并为 MIDI 行静音。

 

