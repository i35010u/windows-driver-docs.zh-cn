---
title: PKEY\_AudioEngine\_OEMPeriod
description: PKEY\_AudioEngine\_OEMPeriod
ms.assetid: e0cefdbf-7016-4609-a898-592a40b5d430
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76934a2d8fec0ffb775ffef355a32619966d4ec5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555431"
---
# <a name="pkeyaudioengineoemperiod"></a>PKEY\_AudioEngine\_OEMPeriod


音频引擎运行在 Windows 预先确定的间隔称为*周期*的音频引擎。 在 Windows 7 和更高版本的 Windows 中，音频引擎默认情况下运行周期的 10 毫秒。 在 Windows 7 中，您可以使用一个 INF 文件和新的注册表项**主键\_AudioEngine\_OEMPeriod**、 自定义音频设备驱动程序的周期。 这是每个终结点设置。

以下内容摘自一个 INF 文件演示如何使用[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)自定义音频设备驱动程序的周期。

```inf
[Version]
Signature="$CHICAGO$"
Class=MEDIA
Provider=%MSFT%
...
[USBAudio]
Include=ks.inf, wdmaudio.inf, wdma_usb.inf
Needs=KS.Registration, WDMAUDIO.Registration, USBAudio.CopyList, USBAudioOEM.AddReg

[USBAudio.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,"GLOBAL",USBAudio.Interface
AddInterface=%KSCATEGORY_RENDER%,"GLOBAL",USBAudio.Interface

[USBAudio.Interface]
AddReg=USBAudio.Interface.AddReg, OEMSettingsOverride.AddReg
...
;;
;; All EP\\0 entries in the same grouping
;;
;; Set default periodicity to 8ms
;;
;; 0x013880 == 80000 (HNSTIME) == 8ms
;;
[OEMSettingsOverride.AddReg]
HKR,"EP\\0", %PKEY_AudioEndpoint_Association%,,%KSNODETYPE_ANY%
HKR,"EP\\0", %PKEY_AudioEngine_OEMPeriod%, %REG_BINARY%, 41,00,63,00,08,00,00,00,80,38,01,00,00,00,00,00

[Strings]
PKEY_AudioEndpoint_Association = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},2"
PKEY_AudioEngine_OEMPeriod = "{E4870E26-3CC5-4CD2-BA46-CA0A9A70ED04},6"
REG_BINARY          = "0x00000001"
```

周期被指定为 VT\_BLOB。 和有效周期范围为 50000-90000 (5 9ms) 甚至 10000 HNSTIME 单元边界 （例如，50000、 60000、 70000、 80000 或 90000） 上。

在前面的摘录中从 INF 文件中，以下 REG\_二进制数据提供自定义项：

8 毫秒的周期表示为 80000 HNSTIME 单位。 以十六进制表示法中，此值表示为 0x013880 中。 该十六进制值编写一次的四位 （半字节），最低有效位与第一次，结果时 80,38,01。 这是作为注册表提供的值\_二进制数据类型。

周期被指定为 VT\_BLOB 数据类型。 这被表示十进制值为 65。 以十六进制格式 65 为由值 41 和前面的 INF 文件摘录显示了 REG\_41 其第一个值的二进制数据序列。

 

 





