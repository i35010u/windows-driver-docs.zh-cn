---
title: WdbgExts 目标信息
description: WdbgExts 目标信息
ms.assetid: 70b26047-2f3a-4d35-861f-a9ca17d1d5f9
keywords:
- WdbgExts 扩展、 目标
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bfddb923f583615f4f929a042ab0d752cd6caa6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369423"
---
# <a name="wdbgexts-target-information"></a>WdbgExts 目标信息


若要确定是否目标将使用 32 位或 64 位指针的内存地址，请使用函数[ **IsPtr64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-isptr64)。

有关目标的信息的操作系统，请使用[ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_获取\_内核\_版本**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_dbgkd_get_version64). 若要获取的处理器总数上的目标和找出哪一个是当前的处理器，请使用函数[ **GetKdContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getkdcontext)。

[ **GetDebuggerData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getdebuggerdata)函数将返回 KDDEBUGGER\_DATA64 或 KDDEBUGGER\_DATA32 结构，其中包含有关目标的信息的[调试器引擎](introduction.md#debugger-engine)具有查询或在当前会话过程中确定。 此信息包括特定密钥的目标位置和特定状态的值。

调试器将缓存从目标获取一些信息。 该函数[ **GetDebuggerCacheSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getdebuggercachesize)将返回此缓存的大小。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

功能更强大目标 API，请参阅[目标信息](target-information.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)此文档的部分。

 

 





