---
title: AVStream 子设备
description: AVStream 子设备
ms.assetid: 4b2528d7-acc7-40eb-a351-64d8564c7a13
keywords:
- 子设备 WDK AVStream
- AVStream 子设备 WDK
- 总线枚举 WDK AVStream
- 硬件 Id WDK AVStream
- 标识符 WDK AVStream
- 兼容 Id WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90e2811f7ce6aceafd4a4e94893f1623c2afd3b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362257"
---
# <a name="avstream-child-devices"></a>AVStream 子设备





本部分适用于 Microsoft Windows Server 2003 和早期版本的操作系统，仅当在该平台上安装了 DirectX 9.0 或更高版本。

AVStream 客户端可创建子设备中的每个键的总线枚举器设备，作为**枚举**分支。 若要执行此操作，将置于**枚举**注册表项下的设备密钥的分支。

具体来说，在**AddReg**部分中的驱动程序的 INF 文件中，供应商提供的值*pnpid*的类型 REG\_下每个条目的 SZ**枚举**。 AVStream 使用此字符串值来构造 (PnP) 插硬件 ID 对于每个单独的子设备。

早于 DirectX 9.0 版本中 AVStream 创建子设备硬件 ID 的窗体"AVStream\\*&lt;pnpid&gt;*"(其中&lt;pnpid&gt; 的值*pnpid*特定设备)。

例如，供应商指定中的以下**AddReg** INF 文件的部分：

```INF
[MyTVDevice.AddReg]
HKR,"ENUM\CrossbarDevice",pnpid,,"MyCrossbar"
HKR,"ENUM\TunerDevice",pnpid,,"MyTuner"
```

相应地，AVStream 与下列设备 Id 创建两个子设备：

AVStream\\MyCrossbar

AVStream\\MyTuner

若要解决从指定相同的两个不同的子设备可能的多义性*pnpid*值，DirectX 9.0 和更高版本更改为每个子设备报告的 Id。 对于父设备报告的每个硬件 ID，AVStream 中以下窗体中创建子设备的 ID:

AVStream\\*&lt;pnpid&gt;*\#*&lt;修改父硬件 ID&gt;*

已修改的父硬件 ID 是父硬件 ID 与每个反斜杠 (**\\**) 字符替换为的数字符号 (**\#**)。

如果生成的字符串太长，AVStream 终止 ID 字符串最多\_设备\_ID\_LEN 字符，包括**NULL**终止符。 在 Windows Server 2003 中，此限制设置为在 200 个字符*cfgmgr32.h*。

例如，父设备报告的以下硬件 Id:

PCI\\VEN\_XXXX&DEV\_YYYY&SUBSYS\_ZZZZZZZZ&REV\_VV

PCI\\VEN\_XXXX&DEV\_YYYY&SUBSYS\_ZZZZZZZZ

具有的设备*pnpid*键**MyCrossbar**，AVStream 创建以下子设备硬件 Id:

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX&DEV\_YYYY&SUBSYS\_ZZZZZZZZ&REV\_VV

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX&DEV\_YYYY&SUBSYS\_ZZZZZZZZ

AVStream 为父设备所报告的兼容 Id 使用相同的过程。 AVStream 创建窗体的子设备的兼容 ID:

AVStream\\*&lt;pnpid&gt;*\#*&lt;修改父兼容 ID&gt;*

兼容 Id 的名称修改和长度规则是相同的硬件 Id。

例如，如果前面所述的父设备报告了以下兼容 Id:

PCI\\VEN\_XXXX&DEV\_YYYY&REV\_VV

PCI\\VEN\_XXXX&DEV\_YYYY

PCI\\VEN\_XXXX&CC\_ZZZZZZ

PCI\\VEN\_XXXX&CC\_ZZZZ

PCI\\VEN\_XXXX

PCI\\CC\_ZZZZZZ

PCI\\CC\_ZZZZ

**MyCrossbar**子设备将报告通过 AVStream 以下兼容 Id:

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX&DEV\_YYYY&REV\_VV

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX&DEV\_YYYY

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX&CC\_ZZZZZZ

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX&CC\_ZZZZ

AVStream\\MyCrossbar\#PCI\#VEN\_XXXX

AVStream\\MyCrossbar\#PCI\#CC\_ZZZZZZ

AVStream\\MyCrossbar\#PCI\#CC\_ZZZZ

AVStream\\MyCrossbar

**请注意**  在 DirectX 9.0 或更高版本，旧的硬件 ID，AVStream\\*&lt;pnpid&gt;*，仍报告为最低排名兼容 id。 因此，旧驱动程序可继续使用未修改这些平台上。
但是，截至 DirectX 9.0 版本中，Microsoft 建议编写利用 AVStream 类总线枚举器的新的或修改驱动程序的供应商使用的新的硬件 ID 格式。 驱动程序可以支持通过在 INF 文件中的兼容 Id 列表中包含旧的 ID 运行早期版本的 AVStream 的平台。

 

 

 




