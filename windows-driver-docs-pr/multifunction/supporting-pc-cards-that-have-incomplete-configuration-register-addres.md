---
title: 具有不完整的配置的 PC 卡注册地址
description: 支持具有不完整的配置注册地址 PC 卡信息
ms.assetid: 2a708ca5-a119-4ef5-81ee-d9e40e7a5255
keywords:
- 不完整的配置将 WDK 多功能设备注册
- 系统提供多功能总线驱动程序 WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4100642afab95d695ea67b8560d59fa90925d2ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324539"
---
# <a name="pc-cards-with-incomplete-configuration-register-addresses"></a>具有不完整的配置的 PC 卡注册地址


如果多功能的 16 位 PC 卡设备已配置为每个函数的寄存器，但不包含所有属性内存中的指针注册集 (不支持 LONGLINK\_MFC 元组)，可以使用此类设备的供应商系统提供的多功能总线驱动程序 (mf.sys)，但必须提供自定义的 INF 文件和支持各个功能。

在基于 NT 的平台上的此类设备的供应商可以使用多功能设备的系统提供的函数驱动程序。

自定义设备 INF 必须指定 mf.sys 作为设备的功能驱动程序。 然后，系统提供 mf.sys 驱动程序将枚举设备的功能。

请参阅[使用 System-Supplied 多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md)有关使用系统提供 mf.sys 驱动程序详细信息。

此类设备的供应商必须提供以下信息：

-   多功能设备的自定义 INF 文件。 （供应商提供）

    供应商必须提供一个多功能的 INF 文件作为多功能总线驱动程序指定 mf.sys，指定的类"多功能"（使用其关联的 GUID 作为在定义 devguid.h)，并提供缺少的配置注册地址。 查看更多更高版本在本部分中的信息。

-   每个函数的设备的即插即用功能驱动程序。 （供应商提供）

    由于多功能总线驱动程序处理的多功能语义，功能的驱动程序可以是函数打包为单个设备时使用了相同驱动程序。

-   用于设备的每个函数的 INF 文件。 （供应商提供）

    INF 文件可以是函数打包为单个设备时，将使用的相同文件。 INF 文件不需要任何特殊的多功能语义。

这样的多功能设备自定义 INF 必须包含至少一个[ **INF DDInstall.LogConfigOverride 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547339)。 重写部分必须包含**MfCardConfig**对于每个函数，确定位置的每个集配置注册表项。

INF 必须重新提出所指定的设备，因为 INF 中存在替代配置时，如果 PnP 管理器不使用该设备从任何设备资源要求的所有资源要求。

指定**MfCardConfig**条目使用的语法中所述[ **INF LogConfig 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547448)。

例如，考虑以下内容摘自多功能 PC 卡设备包含一个调制解调器和网络适配器的自定义 INF:

```cpp
;...
 
[DDInstall.LogConfigOverride]
LogConfig = DDInstall.Override0
 
[DDInstall.Override0]
IOConfig     =    3F8-3FF                  ; Com1
IOConfig     =    10@100-FFFF%FFF0         ; NIC I/O
IRQConfig    =    3,4,5,7,9,10,11          ; IRQ
MemConfig    =    2000@0-FFFFFFFF%FFFFE000 ; Memory Descriptor 0
MemConfig    =    1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor 1
MfCardConfig =    1000:47:0(A)
MfCardConfig =    1080:47:1
;...
```

该示例演示两个**MfCardConfig**条目，一个用于设备的每个函数。 第一个**MfCardConfig**条目包含以下信息：

<a href="" id="1000--configregbase-"></a>1000 (*ConfigRegBase*)  
指定的偏移量 0x1000 卡的属性内存中的配置寄存器组。 在此示例中，这些寄存器中的信息介绍在卡上的调制解调器函数。

<a href="" id="47--configoptions-"></a>47 (*ConfigOptions*)  
在配置选项注册到指定程序总线驱动程序的十六进制值*ConfigRegBase*偏移量 (0x1000)。

<a href="" id="0--ioconfigindex-"></a>0 (*IoConfigIndex*)  
指定此函数的 I/O 资源在第一个列出**IOConfig**在本部分中的条目。 零索引指示第一个项，它在此示例中为"**IOConfig** = 3F8 3FF"。

<a href="" id="a--attrs-"></a>一个 (*attrs*)  
指示要打开针对此函数，这是典型的调制解调器的音频启用的总线驱动程序。

第二个**MfCardConfig**条目包含有关函数的第二个设备 （网络适配器，在此示例中） 上的信息。 此条目指定的偏移量 0x1080 配置寄存器的第二个集。 总线驱动程序将编写*ConfigOptions* 0x47 到此函数的配置选项寄存器的值。 *IoConfigIndex*值为 1 指示总线驱动程序使用第二个**IOConfig**在本部分中的条目 (**IOConfig** = 10@100-FFFF%fff0) 进行编程的 I/O 基并注册此函数的限制。

包括多个*DDInstall*。 **重写 * * * N* INF 若要指定多个选择的无序 I/O 端口范围中的部分。

如果设备使用不基于一个内存窗口为零， *DDInstall*。 **重写 * * * N*区域还必须包括**PcCardConfig**条目。 如果重写部分同时**MfCardConfig**入口和一个**PcCardConfig**条目，PCMCIA 总线驱动程序将忽略*ConfigIndex*中的值**PcCardConfig**条目，并只需使用*MemoryCardBaseN*信息。 请参阅[支持 PC 卡，具有不完整配置注册](supporting-pc-cards-that-have-incomplete-configuration-registers.md)有关详细信息**PcCardConfig**条目。

 

 




