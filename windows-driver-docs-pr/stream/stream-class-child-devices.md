---
title: 流类子设备
description: 流类子设备
ms.assetid: 2885a77d-5e39-4730-b715-99f0a426f273
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，子设备
- 流式处理微型驱动程序 WDK Windows 2000 内核，子设备
- 微型驱动程序 WDK Windows 2000 内核流式处理，子设备
- 子设备 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2193cb84d3c7713ce0b74b403f4dcea1308d84f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371206"
---
# <a name="stream-class-child-devices"></a>流类子设备





本部分适用于 Microsoft Windows Server 2003 和早期版本的操作系统，仅当在该平台上安装了 DirectX 9.0 或更高版本。

如果你的流类设备将置于**Enum**注册表项下其设备的密钥，流类的分支中充当了创建每个密钥中的子设备的总线枚举器在设备**枚举**分支。

中**AddReg**部分中的驱动程序的 INF 文件中，供应商提供的值*pnpid*的类型 REG\_下每个条目的 SZ**枚举**。 Stream 类使用此字符串值来构造 (PnP) 插硬件 ID 对于每个单独的子设备。

早于 DirectX 9.0 版本中流类创建窗体的子设备硬件 ID"AVStream\\*&lt;pnpid&gt;*"(其中&lt;pnpid&gt;的值*pnpid*特定设备)。

例如，供应商指定中的以下**AddReg** INF 文件的部分：

```INF
[MyTVDevice.AddReg]
HKR,"ENUM\CrossbarDevice",pnpid,,"MyCrossbar"
HKR,"ENUM\TunerDevice",pnpid,,"MyTuner"
```

相应地，stream 类将创建两个子设备与下列设备 Id:

Stream\\MyCrossbar

Stream\\MyTuner

若要解决从指定相同的两个不同的子设备可能的多义性*pnpid*值，DirectX 9.0 和更高版本更改为每个子设备报告的 Id。 为父设备报告的每个硬件 ID，stream 类创建以下形式的子设备 ID:

Stream\\*&lt;pnpid&gt;*\#*&lt;修改父硬件 ID&gt;*

已修改的父硬件 ID 是父硬件 ID 与每个反斜杠 (**\\**) 字符替换为的数字符号 (**\#**)。

如果生成的字符串太长，stream 类终止 ID 字符串最多\_设备\_ID\_LEN 字符，包括**NULL**终止符。 在 Windows Server 2003 中，此限制设置为在 200 个字符*cfgmgr32.h*。

例如，父设备报告的以下硬件 Id:

PCI\\VEN\_XXXX&DEV\_YYYY&SUBSYS\_ZZZZZZZZ&REV\_VV

PCI\\VEN\_XXXX&DEV\_YYYY&SUBSYS\_ZZZZZZZZ

具有的设备*pnpid*键**MyCrossbar**，流类创建以下子设备硬件 Id:

Stream\\MyCrossbar\#PCI\#VEN\_XXXX&DEV\_YYYY&SUBSYS\_ZZZZZZZZ&REV\_VV

Stream\\MyCrossbar\#PCI\#VEN\_XXXX&DEV\_YYYY&SUBSYS\_ZZZZZZZZ

Stream 类为父设备所报告的兼容 Id 使用相同的过程。 Stream 类创建窗体的子设备的兼容 ID:

Stream\\*&lt;pnpid&gt;*\#*&lt;修改父兼容 ID&gt;*

兼容 Id 的名称修改和长度规则是相同的硬件 Id。

例如，如果父设备描述以前报告以下兼容 Id:

PCI\\VEN\_XXXX&DEV\_YYYY&REV\_VV

PCI\\VEN\_XXXX&DEV\_YYYY

PCI\\VEN\_XXXX&CC\_ZZZZZZ

PCI\\VEN\_XXXX&CC\_ZZZZ

PCI\\VEN\_XXXX

PCI\\CC\_ZZZZZZ

PCI\\CC\_ZZZZ

**MyCrossbar**子设备将报告流类通过以下兼容 Id:

Stream\\MyCrossbar\#PCI\#VEN\_XXXX&DEV\_YYYY&REV\_VV

Stream\\MyCrossbar\#PCI\#VEN\_XXXX&DEV\_YYYY

Stream\\MyCrossbar\#PCI\#VEN\_XXXX&CC\_ZZZZZZ

Stream\\MyCrossbar\#PCI\#VEN\_XXXX&CC\_ZZZZ

Stream\\MyCrossbar\#PCI\#VEN\_XXXX

Stream\\MyCrossbar\#PCI\#CC\_ZZZZZZ

Stream\\MyCrossbar\#PCI\#CC\_ZZZZ

Stream\\MyCrossbar

**请注意**  在 DirectX 9.0 或更高版本，旧的硬件 ID，Stream\\*&lt;pnpid&gt;*，仍报告为最低排名兼容 id。 因此，旧驱动程序可继续使用未修改这些平台上。
但是，截至 DirectX 9.0 版本中，Microsoft 建议的供应商编写*利用流类总线枚举器的新的或修改驱动程序使用的新的硬件 ID 格式*。 驱动程序可以支持通过在 INF 文件中的兼容 Id 列表中包含旧的 ID 运行早期版本的流类的平台。

 

 

 




