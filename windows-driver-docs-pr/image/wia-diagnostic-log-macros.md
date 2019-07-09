---
title: WIA 诊断日志宏
description: WIA 诊断日志宏
ms.assetid: 8b544045-e9d7-422b-825c-f1a5531e0e11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a47699622edd7b2cb5116fc338796a8189efd641
ms.sourcegitcommit: 67aadd2adef4c338b703464c377ae8c910f1f5f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67622668"
---
# <a name="wia-diagnostic-log-macros"></a>WIA 诊断日志宏

> [!NOTE]
> WIA 的错误处理更现代的 Windows 操作系统上，请参阅[WIA 驱动程序错误恢复](wia-driver-error-recovery-for-windows-vista.md)。

诊断日志宏启用为日志跟踪、 错误和警告消息的微型驱动程序*Wiaservc.log*诊断日志文件。

| 宏 | 描述 |
| --- | --- |
|[WIAS_LERROR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lerror) | 类型错误的日志语句写入 Wiaservc.log 诊断日志文件。 |
| [WIAS_LHRESULT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lhresult) | HRESULT 值转换为一个字符串，并将字符串写入到 Wiaservc.log 诊断日志文件。 |
| [WIAS_LTRACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_ltrace) | Wiaservc.log 诊断日志文件中写入跟踪类型的日志语句。 |
| [WIAS_LWARNING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_lwarning) | 写入警告 Wiaservc.log 诊断日志文件的类型的日志语句。 |
| [WIAS_ERROR](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_error) | 类型错误的日志语句写入 Wiatrace.log 诊断日志文件。 |
| [WIAS_TRACE](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wias_trace) | Wiatrace.log 诊断日志文件中写入跟踪类型的日志语句。 |
