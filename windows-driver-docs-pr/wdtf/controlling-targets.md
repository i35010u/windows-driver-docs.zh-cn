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
ms.openlocfilehash: 89efc921278fe25516a1173fd3cd530e27928357
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386256"
---
# <a name="controlling-targets"></a>控制目标


WDTF 包括一组在目标执行特定操作的接口。 WDTF 使用 Windows 注册表将这些接口的特定于目标的实现映射到实际目标。 可能有一种实现的所有目标或多个特定于类的实现。 可以使用方案[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/wdtf/action-interfaces)而无需知道每个目标的具体情况执行常见的活动。

你的方案可以尝试通过调用找到一个实现，这些接口之一[ **IWDTFTarget2::GetInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getinterface)方法。 请注意，并非所有目标对象都支持每个操作的接口。 下面的 VBScript 代码示例检索可以禁用和启用的接口 （以及更多） 的设备的目标表示。

```cpp
Set Action = Device.GetInterface("PNP")
```

[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) WDTF 标识*ProgId*。 必须指定 WDTF *ProgId*当你调用[ **HasInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-hasinterface)， [ **GetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getinterface)，[ **GetInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftargets2-getinterfaces)，并[ **GetInterfacesIfExist** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftargets2-getinterfacesifexist)方法。 璝惠 WDTF *ProgId*，请参阅**操作接口**。

通过插件模型，可以向 WDTF 添加接口和接口的实现。 有关此模型的详细信息，请参阅[扩展框架](extending-the-framework.md)。

## <a name="related-topics"></a>相关主题
[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[扩展框架](extending-the-framework.md)  
[**GetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-getinterface)  
[**GetInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftargets2-getinterfaces)  
[**GetInterfacesIfExist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftargets2-getinterfacesifexist)  
[**HasInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdtf/nf-wdtf-iwdtftarget2-hasinterface)  



