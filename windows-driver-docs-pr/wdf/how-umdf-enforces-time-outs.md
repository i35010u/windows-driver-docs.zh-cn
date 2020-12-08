---
title: UMDF 中的主机进程超时
description: UMDF 中的主机进程超时
keywords:
- User-Mode Driver Framework WDK，超时
- UMDF WDK，超时
- 用户模式驱动程序 WDK UMDF，超时
- 超时 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c51173d5f64f85d3a9e78adae5f68adb48807996
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814721"
---
# <a name="host-process-timeouts-in-umdf"></a>UMDF 中的主机进程超时


当反射器向驱动程序主机进程发送关键请求时，主机将启动内部计时器。 默认超时间隔为60秒。 关键请求包括即插即用、电源和 i/o 取消。

只要 User-Mode Driver Framework (UMDF) 驱动程序定期执行操作来完成请求，则反射器会延长超时期限。 例如，对于删除请求，驱动程序需要按固定的时间间隔从删除回调中返回。

如果超时时间已到，则反射器会生成一个 WER 错误报告，终止主机进程，并尝试重新启动设备。 有关自动重新启动的信息，请参阅 [在 UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。

有关此报表中的字段的信息，请参阅 [在 WER 报表中访问 UMDF 元数据](accessing-umdf-metadata-in-wer-reports.md)。

超时过期是反射器终止宿主进程的最常见原因。

您可以通过使用 [WDF 验证程序控件应用程序](../devtest/wdf-verifier-control-application.md)来延长超时期限。

 

