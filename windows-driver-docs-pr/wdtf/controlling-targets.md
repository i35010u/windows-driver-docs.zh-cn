---
title: 控制目标
description: 控制目标
ms.assetid: b329e9a2-7d24-4612-9aa1-9d7955a61473
keywords:
- Windows 设备测试框架 WDK，操作接口
- WDTF WDK，操作接口
- Windows 设备测试框架 WDK、 可管理测试
- WDTF WDK、 可管理测试
- 可管理测试 WDK WDTF
- 操作接口 WDK WDTF
- COM 接口 WDK WDTF
- WDK WDTF 接口
- 代码模块 WDK WDTF
- 脚本 WDK WDTF
- 同步测试 WDK WDTF
- 异步测试 WDK WDTF
- 测试脚本 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa6cc73847ce6876bedba58888b0f472ee7052b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348035"
---
# <a name="controlling-targets"></a>控制目标


WDTF 包括一组在目标执行特定操作的接口。 WDTF 使用 Windows 注册表将这些接口的特定于目标的实现映射到实际目标。 可能有一种实现的所有目标或多个特定于类的实现。 可以使用方案[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/wdtf/action-interfaces)而无需知道每个目标的具体情况执行常见的活动。

你的方案可以尝试通过调用找到一个实现，这些接口之一[ **IWDTFTarget2::GetInterface** ](https://msdn.microsoft.com/library/windows/hardware/hh439398)方法。 请注意，并非所有目标对象都支持每个操作的接口。 下面的 VBScript 代码示例检索可以禁用和启用的接口 （以及更多） 的设备的目标表示。

```cpp
Set Action = Device.GetInterface("PNP")
```

[**操作接口**](https://msdn.microsoft.com/library/windows/hardware/ff538355) WDTF 标识*ProgId*。 必须指定 WDTF *ProgId*当你调用[ **HasInterface**](https://msdn.microsoft.com/library/windows/hardware/hh439447)， [ **GetInterface**](https://msdn.microsoft.com/library/windows/hardware/hh439398)，[ **GetInterfaces**](https://msdn.microsoft.com/library/windows/hardware/hh439475)，并[ **GetInterfacesIfExist** ](https://msdn.microsoft.com/library/windows/hardware/hh439478)方法。 璝惠 WDTF *ProgId*，请参阅**操作接口**。

通过插件模型，可以向 WDTF 添加接口和接口的实现。 有关此模型的详细信息，请参阅[扩展框架](extending-the-framework.md)。

## <a name="related-topics"></a>相关主题
[**操作接口**](https://msdn.microsoft.com/library/windows/hardware/ff538355)  
[扩展框架](extending-the-framework.md)  
[**GetInterface**](https://msdn.microsoft.com/library/windows/hardware/hh439398)  
[**GetInterfaces**](https://msdn.microsoft.com/library/windows/hardware/hh439475)  
[**GetInterfacesIfExist**](https://msdn.microsoft.com/library/windows/hardware/hh439478)  
[**HasInterface**](https://msdn.microsoft.com/library/windows/hardware/hh439447)  



