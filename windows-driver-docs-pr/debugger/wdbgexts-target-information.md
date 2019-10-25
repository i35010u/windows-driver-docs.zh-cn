---
title: WdbgExts 目标信息
description: WdbgExts 目标信息
ms.assetid: 70b26047-2f3a-4d35-861f-a9ca17d1d5f9
keywords:
- WdbgExts 扩展，目标
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eae7908748b84fec52256707293aae253e72aaa3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834172"
---
# <a name="wdbgexts-target-information"></a>WdbgExts 目标信息


若要确定目标是否对内存地址使用32位或64位指针，请使用函数[**IsPtr64**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-isptr64)。

有关目标操作系统的信息，请使用[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[**IG\_获取\_内核\_版本**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_dbgkd_get_version64)。 若要获取目标上的处理器总数并找出当前处理器的数量，请使用函数[**GetKdContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getkdcontext)。

[**GetDebuggerData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getdebuggerdata)函数将返回 KDDEBUGGER\_DATA64 或 KDDEBUGGER\_DATA32 结构，该结构包含有关[调试器引擎](introduction.md#debugger-engine)在当前会话期间查询或确定的目标的信息。 此信息包括特定的密钥目标位置和特定状态值。

调试器会缓存从目标获取的某些信息。 函数[**GetDebuggerCacheSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getdebuggercachesize)将返回此缓存的大小。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关更强大的目标 API，请参阅本文档的[使用调试器引擎 API](using-the-debugger-engine-api.md)部分中的[目标信息](target-information.md)。

 

 





