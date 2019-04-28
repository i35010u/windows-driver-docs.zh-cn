---
title: 操作接口
description: 操作接口控制 IWDTFTarget2 接口的实例。 每个插件必须支持此接口。
keywords:
- Windows 设备测试框架 WDK，操作接口
- WDTF WDK，操作接口
- 操作接口 WDK WDTF
- COM 接口 WDK WDTF
- WDK WDTF 接口
ms.date: 04/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 60b71582afea95abed27dd36b46904c8bbd0d52b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347973"
---
# <a name="action-interfaces"></a>操作接口

操作接口控制的实例[IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2)接口。 每个插件必须支持此接口。 所有操作接口都继承自[IAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iaction)，直接或间接。 

可以通过调用 IWDTFTarget2::GetInterface 方法来检索目标的操作接口。

有两个组的操作接口： 设备操作接口和系统操作接口。

### <a name="device-action-interfaces"></a>设备操作接口

| 接口 | 描述 |
|-|-|
|[IWDTFDriverPackageAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/nn-wdtfdriverpackageaction-iwdtfdriverpackageaction2) |  定义操作和表示导入的和预先导入驱动程序包的驱动程序包的属性。 |
|[IWDTFDriverSetupAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupdeviceaction/nn-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2) | 定义控制目标设备驱动程序安装过程的操作。 |
|[IWDTFEnhancedDeviceTestSupportAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportaction2) | 定义操作和支持增强的设备测试 (EDT) 筛选器驱动程序的属性。 |
|[IWDTFEnhancedDeviceTestSupportActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportactions2) | 定义操作和支持的增强型设备测试 (EDT) 操作的集合的属性。 |
|[IWDTFPNPAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpaction2) | 定义操作和插即用 (PNP) 设备相关的测试接口的属性。 |
|[IWDTFPNPActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpactions2) |定义操作和插即用 (PNP) 设备相关的测试接口的集合的属性。 |
|[IWDTFSimpleIOEx2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleioex2) | 定义一个简单的同步 I/O 功能测试的操作。 |
|[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) | 定义一个简单的异步 I/O 功能测试的操作。 |
|[IWDTFSimpleIOStressActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressactions2) | 定义一系列简单的异步 I/O 功能测试的操作。 |
 
### <a name="system-action-interfaces"></a>系统操作接口

| 接口 | 描述 |
|-|-|
|[IWDTFDriverSetupSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupsystemaction/nn-wdtfdriversetupsystemaction-iwdtfdriversetupsystemaction2) | 定义在驱动程序安装过程控制系统的操作。 |
|[IWDTFSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfsystemaction/nn-wdtfsystemaction-iwdtfsystemaction2) | 定义操作和支持驱动程序测试的属性。 |
 

## <a name="remarks"></a>备注

在 WDTF， [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)接口作为许多 SimpleIO 实现的包装实现一次。

SimpleIO 可更轻松地直接使用，而不通过[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)。 这是因为方案代码必须保持对每个引用[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)它启动，并记得在关闭前停止的实例。 但是，由于[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)以异步方式运行它使您能够测试事件的组合。 例如， [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)实例无法启动 I/O 长时间来测试硬件睡眠功能测试。

## <a name="requirements"></a>要求

| Header|
|-|
|[WDTFDriverPackageAction.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/index)|
|[WDTFDriverSetupDeviceAction.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupdeviceaction/index)|
|[WDTFInterfaces.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/index) |
|[WDTFEDTAction.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/index) |
|[WDTFPNPAction.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/index) |


## <a name="see-also"></a>请参阅
[IAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iaction)

[IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2) 

[IWDTFTarget2::GetInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getinterface)

[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 
