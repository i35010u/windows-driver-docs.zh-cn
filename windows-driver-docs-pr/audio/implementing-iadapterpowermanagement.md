---
title: 实现 IAdapterPowerManagement
description: 实现 IAdapterPowerManagement
ms.assetid: 654b86a7-845c-415b-99e4-c7be92cb9b9c
keywords:
- IAdapterPowerManagement
- 适配器驱动程序 WDK 音频，电源管理
- 音频适配器驱动程序 WDK，电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31ed7462867aff11015e49b61ad34c25b35d7c63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833237"
---
# <a name="implementing-iadapterpowermanagement"></a>实现 IAdapterPowerManagement


## <span id="implementing_iadapterpowermanagement"></span><span id="IMPLEMENTING_IADAPTERPOWERMANAGEMENT"></span>


为驱动程序实现[IAdapterPowerManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement)接口时，请参阅 Microsoft Windows 驱动程序工具包（WDK）中的示例音频驱动程序中的**CAdapterCommon**类的实现。 此类处理设备中断，并执行所有音频适配器驱动程序共用的其他功能。 适配器的**CAdapterCommon**类应继承自**IAdapterPowerManagement**接口，并支持其**NonDelegatingQueryInterface**方法中的此接口。 （有关 nondelegating 接口的详细信息，请参阅**INonDelegatingUnknown**接口的说明。）

可以使用标头文件 Portcls 中的 IMP\_IAdapterPowerManagement 定义添加 IAdapterPowerManagement 的函数声明[ **：:P owerchangestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-powerchangestate)、 [**IAdapterPowerManagement：： QueryPowerChangeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-querypowerchangestate)和[**IAdapterPowerManagement：： QueryDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iadapterpowermanagement-querydevicecapabilities)方法用于驱动程序的**CAdapterCommon**类定义。

在 PortCls 系统驱动程序调用适配器的设备启动例程（请参阅[启动设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)）期间，适配器应通过调用[**PcRegisterAdapterPowerManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)向 PortCls 注册其**IAdapterPowerManagement**接口。 有关代码示例，请参阅 WDK 中 Sb16 示例适配器驱动程序中的**StartDevice**函数。 **PcRegisterAdapterPowerManagement**函数的第一个参数是指向适配器驱动程序的**CAdapterCommon**对象的**IUnknown**指针。 PortCls 查询此对象的**IAdapterPowerManagement**接口。

当 PortCls 调用适配器驱动程序的**IAdapterPowerManagement：:P owerchangestate**方法更改设备的电源状态时，适配器驱动程序应在适配器的**CAdapterCommon**对象中缓存设备的新电源状态。 在**CAdapterCommon：： Init**调用期间（请参阅 WDK 的示例适配器驱动程序中的实现），驱动程序应在成功初始化之前将初始电源状态设置为 PowerDeviceD0 （如[DeviceState](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate)中所述）. 仅当已知设备处于适当的电源状态时，驱动程序才能写入硬件。 例如，在 WDK 的 Sb16 示例驱动程序中，驱动程序只会在 PowerDeviceD0 状态下写入硬件。

在关闭以响应**PowerChangeState**呼叫之前，适配器驱动程序应将音频输出置于防止扬声器噪音在电源开关关闭时出现的状态。 例如，关闭过程可能包括将 DAC 输出斜向零旋转、关闭 Dac 并为 MIDI 行静音。

 

 




