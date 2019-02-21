---
title: 创建标准版资源映射
description: 创建标准版资源映射
ms.assetid: 97d95481-5290-41d3-a6e6-7cc142d4c2e8
keywords:
- 标准版资源映射 WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0610e483cd324a8a16b76442e4213599489cc656
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525539"
---
# <a name="creating-standard-resource-maps"></a>创建标准版资源映射





如果包含的多功能设备 INF [ **INF DDInstall.LogConfigOverride 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547339)，父资源是通过隐式编号的 00 *nn*出现在 INF*日志配置节*部分 (请参阅[ **INF LogConfig 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547448))。 例如，考虑使用以下 INF 多功能 PC 卡*DDInstall*。**LogConfigOverride**部分：

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

在此示例中的设备有五个资源，这是通过 04 编号的 00。 如果有多个*DDInstall*。**LogConfigOverride**部分中，必须在每个部分中的顺序列出的资源。

如果一个子函数 (Child0000) 要求上面列出的第一个和第三个资源，将为此子资源映射：00,02. 如果另一个子函数 (Child00001) 要求所有五个资源，则会在其资源映射：00,01,02,03,04. 在此示例中，资源 00 (**IoConfig = 2f8 2ff**) 和 02 (**IRQConfig = 3、 4、 5、 7、 9、 10、 11**) 共享。 这些资源映射会 INF 中，如下所示指定：

```cpp
[DDInstall.RegHW]
    ; for each "child" function list hardware ID and resource map
HKR,Child0000,HardwareID,,child0000-hardware-ID
HKR,Child0000,ResourceMap,1,00,02                 ; map for Child0000
HKR,Child0001,HardwareID,,child0001-hardware-ID
HKR,Child0001,ResourceMap,1,00,01,02,03,04        ; map for Child0001
```

"1"的以下**ResourceMap**参数指定的注册表项是 REG\_二进制数据类型。 后面"1"的数字是资源的映射值。

如果有任何*DDInstall*。**LogConfigOverride** INF 中的部分，父资源的资源要求通过为基础的总线驱动程序构造的顺序进行编号。 对于 PC 卡总线驱动程序会报告此订单中的资源：IRQ、 I/O 端口、 内存地址。 有关多个 I/O 和内存要求，这些编号在卡上的元组的顺序相同。 其他总线驱动程序可能还会列出其他订单中的资源。

 

 




