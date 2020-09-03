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
ms.openlocfilehash: ae759e53dfcec14efd2c9df085ec6f22bbcf4e31
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403552"
---
# <a name="action-interfaces"></a>操作接口

操作接口控制 [IWDTFTarget2](/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2) 接口的实例。 每个插件都必须支持此接口。 所有操作接口都直接或间接继承自 [IAction](/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iaction)。 

可以通过调用 IWDTFTarget2：： GetInterface 方法检索目标的操作接口。

有两组操作接口：设备操作接口和系统操作接口。

### <a name="device-action-interfaces"></a>设备操作接口

| 接口 | 说明 |
|-|-|
|[IWDTFDriverPackageAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriverpackageaction/nn-wdtfdriverpackageaction-iwdtfdriverpackageaction2) |  定义表示导入和预先导入的驱动程序包的驱动程序包的操作和属性。 |
|[IWDTFDriverSetupAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/nn-wdtfdriversetupdeviceaction-iwdtfdriversetupaction2) | 定义在驱动程序安装过程中控制目标设备的操作。 |
|[IWDTFEnhancedDeviceTestSupportAction2](/windows-hardware/drivers/ddi/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportaction2) | 定义支持增强型设备测试 (EDT) 筛选器驱动程序的操作和属性。 |
|[IWDTFEnhancedDeviceTestSupportActions2](/windows-hardware/drivers/ddi/wdtfedtaction/nn-wdtfedtaction-iwdtfenhanceddevicetestsupportactions2) | 定义支持 (EDT) 操作的增强型设备测试集合的操作和属性。 |
|[IWDTFPNPAction2](/windows-hardware/drivers/ddi/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpaction2) | 为即插即用 (PNP) 设备相关测试接口定义操作和属性。 |
|[IWDTFPNPActions2](/windows-hardware/drivers/ddi/wdtfpnpaction/nn-wdtfpnpaction-iwdtfpnpactions2) |定义 (PNP) 设备相关测试接口的即插即用集合的操作和属性。 |
|[IWDTFSimpleIOEx2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleioex2) | 定义简单同步 i/o 功能测试的操作。 |
|[IWDTFSimpleIOStressAction2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) | 定义简单的异步 i/o 功能测试的操作。 |
|[IWDTFSimpleIOStressActions2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressactions2) | 定义简单异步 i/o 功能测试集合的操作。 |
 
### <a name="system-action-interfaces"></a>系统操作接口

| 接口 | 说明 |
|-|-|
|[IWDTFDriverSetupSystemAction2](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupsystemaction/nn-wdtfdriversetupsystemaction-iwdtfdriversetupsystemaction2) | 定义在驱动程序安装过程中控制系统的操作。 |
|[IWDTFSystemAction2](/windows-hardware/drivers/ddi/wdtfsystemaction/nn-wdtfsystemaction-iwdtfsystemaction2) | 定义支持驱动程序测试的操作和属性。 |
 

## <a name="remarks"></a>备注

在 WDTF 中， [IWDTFSimpleIOStressAction2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 接口仅实现为众多 SimpleIO 实现周围的包装器。

SimpleIO 可以更轻松地直接使用，而不是通过 [IWDTFSimpleIOStressAction2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)。 这是因为，方案代码必须保留对其启动的每个 [IWDTFSimpleIOStressAction2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 实例的引用，并记得在关闭前将其停止。 但是，因为 [IWDTFSimpleIOStressAction2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 以异步方式运行，因此可以测试事件的组合。 例如， [IWDTFSimpleIOStressAction2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2) 实例可能会在一段较长时间内开始 i/o 测试，以测试硬件休眠功能。

## <a name="requirements"></a>要求

| Header|
|-|
|[WDTFDriverPackageAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriverpackageaction/index)|
|[WDTFDriverSetupDeviceAction](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtfdriversetupdeviceaction/index)|
|[WDTFInterfaces](/windows-hardware/drivers/ddi/wdtfinterfaces/index) |
|[WDTFEDTAction](/windows-hardware/drivers/ddi/wdtfedtaction/index) |
|[WDTFPNPAction](/windows-hardware/drivers/ddi/wdtfpnpaction/index) |


## <a name="see-also"></a>另请参阅
[IAction](/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iaction)

[IWDTFTarget2](/windows-hardware/drivers/ddi/wdtf/nn-wdtf-iwdtftarget2) 

[IWDTFTarget2：： GetInterface](/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getinterface)

[IWDTFSimpleIOStressAction2](/windows-hardware/drivers/ddi/wdtfinterfaces/nn-wdtfinterfaces-iwdtfsimpleiostressaction2)