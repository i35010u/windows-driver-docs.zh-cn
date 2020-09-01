---
title: 创建标准资源映射
description: 创建标准资源映射
ms.assetid: 97d95481-5290-41d3-a6e6-7cc142d4c2e8
keywords:
- 标准资源映射 WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 547d6e03ba257f947cafb47fad85cf7f93fc1076
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186443"
---
# <a name="creating-standard-resource-maps"></a>创建标准资源映射





如果多功能设备的 INF 包含[**Inf DDInstall. LogConfigOverride 部分**](../install/inf-ddinstall-logconfigoverride-section.md)，则父资源在 inf 的*日志配置-节*部分中显示时，将隐式编号为00到*Nn* ， (参见[**inf LogConfig 指令**](../install/inf-logconfig-directive.md)) 。 例如，请考虑使用以下 INF *DDInstall*的多功能电脑卡。**LogConfigOverride** 部分：

```cpp
[DDInstall.LogConfigOverride]
LogConfig = DDInstall.Override0
 
[DDInstall.Override0]    ;com2
IOConfig=2f8-2ff                      ; resource 00
IOConfig=20@100-FFFF%FFE0             ; resource 01
IRQConfig=3,4,5,7,9,10,11             ; resource 02
MemConfig=4000@0-FFFFFFFF%FFFFC000    ; resource 03
PcCardConfig=41:100000(W)             ; resource 04
```

在此示例中，设备包含5个资源，编号为00到04。 如果有多个 *DDInstall*。**LogConfigOverride** 部分，资源必须在每个部分中按相同顺序列出。

如果 (Child0000 的一个子函数) 需要上面列出的第一个和第三个资源，则该子级的资源映射将为：00，02。 如果 (Child00001 的另一个子函数) 需要全部五个资源，则其资源映射将为：00、01、02、03、04。 在此示例中，资源 00 (**IoConfig = 2f8-2ff**) 和 02 (**IRQConfig = 3、4、5、7、9、10、11**) 共享。 这些资源映射将在 INF 中指定，如下所示：

```cpp
[DDInstall.RegHW]
    ; for each "child" function list hardware ID and resource map
HKR,Child0000,HardwareID,,child0000-hardware-ID
HKR,Child0000,ResourceMap,1,00,02                 ; map for Child0000
HKR,Child0001,HardwareID,,child0001-hardware-ID
HKR,Child0001,ResourceMap,1,00,01,02,03,04        ; map for Child0001
```

**Windows.applicationmodel.resources.core.resourcemap**参数后的 "1" 指定注册表项为 REG \_ BINARY 数据类型。 "1" 后面的数字是资源映射值。

如果没有 *DDInstall*。**LogConfigOverride** 在 INF 中，父资源按照基础总线驱动程序构建资源需求的顺序进行编号。 对于 PC 卡，总线驱动程序按以下顺序报告资源： IRQ、i/o 端口和内存地址。 对于多个 i/o 和内存需求，它们按与卡上的元组相同的顺序进行编号。 其他总线驱动程序可能会按其他顺序列出资源。

 

