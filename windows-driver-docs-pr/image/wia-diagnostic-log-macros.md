---
title: WIA 诊断日志宏
description: WIA 诊断日志宏
ms.assetid: 8b544045-e9d7-422b-825c-f1a5531e0e11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb6a27689077072b5913631d134205eccb7bc5a1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189365"
---
# <a name="wia-diagnostic-log-macros"></a>WIA 诊断日志宏

> [!NOTE]
> 对于新式 Windows 操作系统上的 WIA 错误处理，请参阅 [Wia 驱动程序错误恢复](wia-driver-error-recovery-for-windows-vista.md)。

诊断日志宏使微型驱动程序可以将跟踪、错误和警告消息记录到 *Wiaservc* 诊断日志文件中。

| 宏 | 描述 |
| --- | --- |
|[WIAS_LERROR](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lerror) | 将类型为 ERROR 的日志语句写入 Wiaservc 诊断日志文件。 |
| [WIAS_LHRESULT](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lhresult) | 将 HRESULT 值转换为字符串，并将字符串写入 Wiaservc 诊断日志文件。 |
| [WIAS_LTRACE](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_ltrace) | 将跟踪类型的日志语句写入 Wiaservc 诊断日志文件。 |
| [WIAS_LWARNING](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lwarning) | 向 Wiaservc 诊断日志文件写入类型为 WARNING 的日志语句。 |
| [WIAS_ERROR](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_error) | 将类型为 ERROR 的日志语句写入 Wiatrace 诊断日志文件。 |
| [WIAS_TRACE](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_trace) | 将跟踪类型的日志语句写入 Wiatrace 诊断日志文件。 |