---
title: 操作接口
description: 操作接口控制 IWDTFTarget2 接口的实例。 每个插件都必须支持此接口。
keywords:
- Windows 设备测试框架 WDK，操作接口
- WDTF WDK，操作接口
- 操作接口 WDK WDTF
- COM 接口 WDK WDTF
- 接口 WDK WDTF
ms.date: 04/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e6140943bbe05deb2ed59404bb50657af755976
ms.sourcegitcommit: ee1fc949d1ae5eb14df4530758f767702a886e36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2019
ms.locfileid: "71164794"
---
# <a name="action-interfaces"></a>操作接口

操作接口控制[IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2)接口的实例。 每个插件都必须支持此接口。 所有操作接口都直接或间接继承自[IAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iaction)。 

可以通过调用 IWDTFTarget2：： GetInterface 方法检索目标的操作接口。

有两组操作接口：设备操作接口和系统操作接口。

### <a name="device-action-interfaces"></a>设备操作接口

| 接口 | 描述 |
|-|-|
|[IWDTFDriverPackageAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/nn-wdtfdriverpackageaction-iwdtfdriverpackageaction2) |  定义表示导入和预先导入的驱动程序包的驱动程序包的操作和属性。 |
|[IWDTFDriverSetupAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupdeviceaction/nn-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2) | 定义在驱动程序安装过程中控制目标设备的操作。 |
|[IWDTFEnhancedDeviceTestSupportAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportaction2) | 定义支持增强型设备测试（EDT）筛选器驱动程序的操作和属性。 |
|[IWDTFEnhancedDeviceTestSupportActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportactions2) | 定义支持收集增强的设备测试（EDT）操作的操作和属性。 |
|[IWDTFPNPAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpaction2) | 定义即插即用（PNP）设备相关测试接口的操作和属性。 |
|[IWDTFPNPActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpactions2) |定义即插即用（PNP）设备相关测试接口的集合的操作和属性。 |
|[IWDTFSimpleIOEx2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleioex2) | 定义简单同步 i/o 功能测试的操作。 |
|[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) | 定义简单的异步 i/o 功能测试的操作。 |
|[IWDTFSimpleIOStressActions2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressactions2) | 定义简单异步 i/o 功能测试集合的操作。 |
 
### <a name="system-action-interfaces"></a>系统操作接口

| 接口 | 描述 |
|-|-|
|[IWDTFDriverSetupSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupsystemaction/nn-wdtfdriversetupsystemaction-iwdtfdriversetupsystemaction2) | 定义在驱动程序安装过程中控制系统的操作。 |
|[IWDTFSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfsystemaction/nn-wdtfsystemaction-iwdtfsystemaction2) | 定义支持驱动程序测试的操作和属性。 |
 

## <a name="remarks"></a>备注

在 WDTF 中， [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)接口仅实现为众多 SimpleIO 实现周围的包装器。

SimpleIO 可以更轻松地直接使用，而不是通过[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)。 这是因为，方案代码必须保留对其启动的每个[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)实例的引用，并记得在关闭前将其停止。 但是，因为[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)以异步方式运行，因此可以测试事件的组合。 例如， [IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)实例可能会在一段较长时间内开始 i/o 测试，以测试硬件休眠功能。

## <a name="requirements"></a>要求

| Header|
|-|
|[WDTFDriverPackageAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriverpackageaction/index)|
|[WDTFDriverSetupDeviceAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfdriversetupdeviceaction/index)|
|[WDTFInterfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/index) |
|[WDTFEDTAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfedtaction/index) |
|[WDTFPNPAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfpnpaction/index) |


## <a name="see-also"></a>请参阅
[IAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iaction)

[IWDTFTarget2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nn-wdtf-iwdtftarget2) 

[IWDTFTarget2：： GetInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getinterface)

[IWDTFSimpleIOStressAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 
