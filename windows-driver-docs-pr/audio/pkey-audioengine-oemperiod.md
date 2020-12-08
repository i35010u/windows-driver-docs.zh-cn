---
title: PKEY \_ AudioEngine \_ OEMPeriod
description: PKEY \_ AudioEngine \_ OEMPeriod
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf63970d5447f81cdb3af698bfa31b87249da6c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800915"
---
# <a name="pkey_audioengine_oemperiod"></a>PKEY \_ AudioEngine \_ OEMPeriod


Windows 音频引擎按预定的时间间隔运行，这称为音频引擎的 *周期* 。 在 windows 7 和更高版本的 Windows 中，默认情况下，音频引擎运行时的周期为10ms。 在 Windows 7 中，你可以使用一个 INF 文件和一个新的注册表项 **PKEY \_ AudioEngine \_ OEMPeriod** 来自定义你的音频设备驱动程序的周期。 这是每个终结点的设置。

INF 文件中的以下摘录演示了如何使用 [**Inf AddReg 指令**](../install/inf-addreg-directive.md) 来自定义音频设备驱动程序的周期。

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

周期被指定为 VT \_ BLOB。 有效周期范围为 50000-90000 (9ms) ，甚至 10000 HNSTIME 单元边界， (例如50000、60000、70000、80000或 90000) 。

在前面摘录的 INF 文件中，提供以下 REG \_ 二进制数据进行自定义：

8ms 的周期以 HNSTIME 单位表示为80000。 在十六进制表示法中，此值表示为0x013880。 当此十六进制值一次写入 (半字节) 的四位时，将首先包含最低有效位，结果为80，38，01。 这是作为 REG BINARY 数据类型提供的值 \_ 。

周期指定为 VT \_ BLOB 数据类型。 这由十进制值65表示。 在十六进制格式65中，值为41，前面的 INF 文件摘录显示了 \_ 具有第一个值41的 REG BINARY 数据序列。

 

