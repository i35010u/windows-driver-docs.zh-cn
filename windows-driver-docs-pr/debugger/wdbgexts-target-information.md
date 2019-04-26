---
title: WdbgExts 目标信息
description: WdbgExts 目标信息
ms.assetid: 70b26047-2f3a-4d35-861f-a9ca17d1d5f9
keywords:
- WdbgExts 扩展、 目标
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35aea6028bf91426673da3743f34991742e928ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325845"
---
# <a name="wdbgexts-target-information"></a>WdbgExts 目标信息


若要确定是否目标将使用 32 位或 64 位指针的内存地址，请使用函数[ **IsPtr64**](https://msdn.microsoft.com/library/windows/hardware/ff551094)。

有关目标的信息的操作系统，请使用[ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_获取\_内核\_版本**](https://msdn.microsoft.com/library/windows/hardware/ff550918). 若要获取的处理器总数上的目标和找出哪一个是当前的处理器，请使用函数[ **GetKdContext**](https://msdn.microsoft.com/library/windows/hardware/ff546962)。

[ **GetDebuggerData** ](https://msdn.microsoft.com/library/windows/hardware/ff546573)函数将返回 KDDEBUGGER\_DATA64 或 KDDEBUGGER\_DATA32 结构，其中包含有关目标的信息的[调试器引擎](introduction.md#debugger-engine)具有查询或在当前会话过程中确定。 此信息包括特定密钥的目标位置和特定状态的值。

调试器将缓存从目标获取一些信息。 该函数[ **GetDebuggerCacheSize** ](https://msdn.microsoft.com/library/windows/hardware/ff546568)将返回此缓存的大小。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

功能更强大目标 API，请参阅[目标信息](target-information.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)此文档的部分。

 

 





