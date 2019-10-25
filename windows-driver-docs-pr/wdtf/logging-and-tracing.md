---
title: WDTF 对象日志记录
description: WDTF 对象日志记录
ms.assetid: A99E62D1-31A2-46B5-841B-F3969854E39A
keywords:
- 记录 WDK WDTF
- 跟踪 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adb9620eb10f19ee5716571fefdc6829324eb6f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844818"
---
# <a name="wdtf-object-logging"></a>WDTF 对象日志记录





WDTF 对象*日志记录*是 WDTF 中的一项功能，它允许 WDTF 对象自动将日志消息写入公用日志文件。 对象日志记录文件的名称称为 TestTextLog。 WDTF 对象日志记录具有两个主要优势。 它通过使用 WDTF 对象方法记录高级方法调用、方法的参数和该方法的结果，简化了测试脚本的创作。 WDTF 对象日志记录还通过提供用于写入公用日志消息的一致机制来改善诊断。

默认情况下，WDTF 对象日志记录处于禁用状态。 可以通过调用[**IWDTFConfig2：： EnableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfconfig2-enableobjectlogging)方法启用对象日志记录。 启用日志记录后，可以通过调用方法[**IWDTFAction2：： EnableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfaction2-enableobjectlogging)， [**IWDTFAction2：:D isableobjectlogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfaction2-disableobjectlogging)， [**IWDTFActions2：：为特定操作或操作集合暂时禁用或重新启用该日志记录。EnableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[**IWDTFActions2：:D isableobjectlogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

WDTF 写入日志文件的日志消息具有常见模式。

```cpp
<OBJECT_NAME> : <TYPE> : - <METHOD_NAME>(<METHOD_PARAMS>) <Additional Info>
<OBJECT_NAME> : <TYPE> : Target: <DisplayName>
```

下面的示例演示为示例系统启用日志记录时，对**DeviceDepot （"Volume：："）** 的调用的日志记录输出。

```cpp
[ Output ]

WDTF_TARGETS    : INFO  :  - Query("Volume::")
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: HL-DT-ST RW/DVD MU10N ATA Device
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
```

如果启用对象日志记录，则默认情况下会启用对象错误日志记录。 否则，错误日志记录默认为禁用。 与对象日志记录一样，可以通过调用方法[**IWDTFConfig2：： EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfconfig2-enableobjecterrorlogging)， [**IWDTFConfig2：:D isableobjecterrorlogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfconfig2-disableobjecterrorlogging)， [**IWDTFAction2：： EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfaction2-enableobjecterrorlogging)启用/禁用错误日志记录， [**IWDTFAction2：:D isableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfaction2-disableobjecterrorlogging)、 [**IWDTFActions2：： EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[**IWDTFActions2：:D isableobjecterrorlogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

对于错误日志记录，WDTF 写入日志文件的日志消息具有以下模式。 查找关键字 "错误"，跳转到日志中的第一个错误。

``` syntax
<OBJECT_NAME> : <TYPE> : - <METHOD_NAME>(<METHOD_PARAMS>) <Additional Info>
<OBJECT_NAME> : <TYPE> : Target: <DisplayName>
<OBJECT_NAME> : ERROR : Status: <ErrorString>
```

你仍可以通过调用[**IWDTFLog2：： OutputInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtflog2-outputinfo)或[**IWDTFLog2：： OutputError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtflog2-outputerror)方法，将自定义消息写入日志文件。

有关可用对象的列表，请参阅[WDTF Object Name tags](wdtf-object-name-tags.md)。

## <a name="related-topics"></a>相关主题
[WDTF 对象名称标记](wdtf-object-name-tags.md)  
[启用和查看 WDTF 跟踪](viewing-wdtf-traces.md)  



