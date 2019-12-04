---
title: WIA 诊断日志宏
description: WIA 诊断日志宏
ms.assetid: 8b544045-e9d7-422b-825c-f1a5531e0e11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82c1c8af3f3d7b4b3a14b30ab64a6f33de751bb8
ms.sourcegitcommit: 1585a52e762226b01c7369371727746487cc57bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74796643"
---
# <a name="wia-diagnostic-log-macros"></a>WIA 诊断日志宏

> [!NOTE]
> 对于新式 Windows 操作系统上的 WIA 错误处理，请参阅[Wia 驱动程序错误恢复](wia-driver-error-recovery-for-windows-vista.md)。

诊断日志宏使微型驱动程序可以将跟踪、错误和警告消息记录到*Wiaservc*诊断日志文件中。

| 宏 | 描述 |
| --- | --- |
|[WIAS_LERROR](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lerror) | 将类型为 ERROR 的日志语句写入 Wiaservc 诊断日志文件。 |
| [WIAS_LHRESULT](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lhresult) | 将 HRESULT 值转换为字符串，并将字符串写入 Wiaservc 诊断日志文件。 |
| [WIAS_LTRACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_ltrace) | 将跟踪类型的日志语句写入 Wiaservc 诊断日志文件。 |
| [WIAS_LWARNING](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_lwarning) | 向 Wiaservc 诊断日志文件写入类型为 WARNING 的日志语句。 |
| [WIAS_ERROR](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_error) | 将类型为 ERROR 的日志语句写入 Wiatrace 诊断日志文件。 |
| [WIAS_TRACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wias_trace) | 将跟踪类型的日志语句写入 Wiatrace 诊断日志文件。 |
