---
title: 不完整配置注册地址的 PC 卡
description: 有关支持不完整配置注册地址的 PC 卡的信息
ms.assetid: 2a708ca5-a119-4ef5-81ee-d9e40e7a5255
keywords:
- 不完整的配置注册 WDK 多功能设备
- 系统提供的多功能总线驱动程序 WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 684e7b23201065adc64733b42a1b394041af36ab
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185901"
---
# <a name="pc-cards-with-incomplete-configuration-register-addresses"></a>不完整配置注册地址的 PC 卡


如果多功能16位 PC 卡设备具有每个函数的配置寄存器，但没有在属性内存中包含指向所有寄存器集的指针 (不支持 LONGLINK \_ MFC 元组) ，此类设备的供应商可以使用系统提供的多功能总线驱动程序 ( # A0) ，但必须提供自定义 INF 文件并支持各个函数。

在基于 NT 的平台上，此类设备的供应商可以对多功能设备使用系统提供的函数驱动程序。

设备的自定义 INF 必须指定 mf.sys 作为设备的函数驱动程序。 系统提供的 mf.sys 驱动程序将枚举设备的功能。

有关使用系统提供的 mf.sys 驱动程序的详细信息，请参阅 [使用系统提供的多功能总线驱动程序](using-the-system-supplied-multifunction-bus-driver.md) 。

此类设备的供应商必须提供以下各项：

-   多功能设备的自定义 INF 文件。  (供应商提供的) 

    供应商必须提供一个多功能 INF 文件，该文件指定 mf.sys 作为多功能总线驱动程序，指定类 "多功能" (及其关联的 GUID （如 devguid) 中所定义），并提供 (es) 的配置寄存器地址。 请参阅本节后面部分的详细信息。

-   设备的每个功能的 PnP 函数驱动程序。  (供应商提供的) 

    由于多功能总线驱动程序处理多功能语义，因此函数驱动程序可以是将函数打包为单个设备时使用的相同驱动程序。

-   设备的每个功能的 INF 文件。  (供应商提供的) 

    INF 文件可以是在将函数打包为单个设备时使用的相同文件。 INF 文件不需要任何特殊的多功能语义。

此类多功能设备的自定义 INF 必须包含至少一个 [**INF DDInstall. LogConfigOverride 部分**](../install/inf-ddinstall-logconfigoverride-section.md)。 重写节必须包含每个函数的 **MfCardConfig** 项，以标识每组配置寄存器的位置。

INF 必须重述设备指定的所有资源要求，因为如果 INF 中存在替代配置，则 PnP 管理器不会使用设备提供的任何设备资源要求。

使用[**INF LogConfig 指令**](../install/inf-logconfig-directive.md)中描述的语法指定**MfCardConfig**项。

例如，请考虑以下针对包含调制解调器和网络适配器的多功能 PC 卡设备的自定义 INF 摘录：

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

该示例显示两个 **MfCardConfig** 条目，每个条目对应于设备的每个功能。 第一个 **MfCardConfig** 项包含以下信息：

<a href="" id="1000--configregbase-"></a>1000 (*ConfigRegBase*)   
指定卡的属性内存中有一组配置寄存器，偏移0x1000。 在此示例中，这些寄存器中的信息描述了卡上的调制解调器功能。

<a href="" id="47--configoptions-"></a>47 (*ConfigOptions*)   
指定总线驱动程序的十六进制值，以在 *ConfigRegBase* 的偏移量 (0x1000) 中计划到配置选项注册。

<a href="" id="0--ioconfigindex-"></a>0 (*IoConfigIndex*)   
指定此函数的 i/o 资源列在此部分的第一个 **IOConfig** 条目中。 零的索引指示第一个条目，在此示例中为 "**IOConfig** = 3F8-3FF"。

<a href="" id="a--attrs-"></a> (*attrs*)   
指示总线驱动程序为此功能启用 "音频启用"，这是调制解调器的典型功能。

第二个 **MfCardConfig** 项包含有关网络适配器 (设备上的第二个函数的信息，在此示例中) 。 此项指定在偏移0x1080 有另一组配置寄存器。 总线驱动程序会将0x47 的 *ConfigOptions* 值写入此函数的配置选项 register。 *IoConfigIndex*的值指示总线驱动程序使用此部分中的第二个**IOConfig**条目 (**IOConfig** = 10@100-FFFF % FFF0) 为此函数编程和限制寄存器。

在 INF 中包含多个 *DDInstall*. **Override * * N* 节，以指定多个非顺序 i/o 端口范围的选择。

如果设备使用的内存窗口不是基于零的，则 *DDInstall*. **Override * * N* 节 (s) 还必须包含 **PcCardConfig** 项。 如果 override 节同时具有**MfCardConfig**条目和**PcCardConfig**条目，则 PCMCIA 总线驱动程序将忽略**PcCardConfig**条目中的*ConfigIndex*值，只使用*MemoryCardBaseN*信息。 有关**PcCardConfig**条目的详细信息，请参阅[支持不完整的配置注册的 PC 卡](supporting-pc-cards-that-have-incomplete-configuration-registers.md)。

 

