---
title: 控制目标
description: 控制目标
ms.assetid: b329e9a2-7d24-4612-9aa1-9d7955a61473
keywords:
- Windows 设备测试框架 WDK，操作接口
- WDTF WDK，操作接口
- Windows 设备测试框架 WDK，可管理的测试
- WDTF WDK，可管理的测试
- 可管理的测试 WDK WDTF
- 操作接口 WDK WDTF
- COM 接口 WDK WDTF
- 接口 WDK WDTF
- 代码模块 WDK WDTF
- 脚本 WDK WDTF
- 同步测试 WDK WDTF
- 异步测试 WDK WDTF
- 测试脚本 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2cd4cfbfd27f5454972005ae5048bfef223b982
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841669"
---
# <a name="controlling-targets"></a>控制目标


WDTF 包括一组在目标上执行特定操作的接口。 WDTF 使用 Windows 注册表将这些接口的目标特定实现映射到实际目标。 可能有一个实现适用于所有目标，或者有多个特定于类的实现。 方案可以使用[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/wdtf/action-interfaces)执行常见活动，而无需了解每个目标的具体信息。

你的方案可以通过调用[**IWDTFTarget2：： GetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getinterface)方法尝试查找其中一个接口的实现。 请注意，并非所有目标对象都支持每个操作接口。 下面的 VBScript 代码示例检索一个接口，该接口可以禁用和启用（以及更多）目标表示的设备。

```cpp
Set Action = Device.GetInterface("PNP")
```

[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)用 WDTF *ProgId*标识。 调用[**HasInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-hasinterface)、 [**GetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getinterface)、 [**GetInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-getinterfaces)和[**GetInterfacesIfExist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-getinterfacesifexist)方法时，必须指定 WDTF *ProgId* 。 有关 WDTF *ProgId*的信息，请参阅**操作接口**。

可以通过插件模型将接口和接口的实现添加到 WDTF。 有关此模型的详细信息，请参阅[扩展框架](extending-the-framework.md)。

## <a name="related-topics"></a>相关主题
[**操作接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[扩展框架](extending-the-framework.md)  
[**GetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-getinterface)  
[**GetInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-getinterfaces)  
[**GetInterfacesIfExist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftargets2-getinterfacesifexist)  
[**HasInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtftarget2-hasinterface)  



