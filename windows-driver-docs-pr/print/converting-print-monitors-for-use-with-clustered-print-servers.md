---
title: 转换打印监视器以便与群集打印服务器配合使用
description: 转换打印监视器以便与群集打印服务器配合使用
keywords:
- 打印监视器 WDK、群集打印服务器
- 群集打印服务器 WDK
- 打印服务器群集 WDK
- 转换群集打印服务器的打印监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 163af4489d79e182abfb1f5a738951f19e4c8bb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797507"
---
# <a name="converting-print-monitors-for-use-with-clustered-print-servers"></a>转换打印监视器以便与群集打印服务器配合使用





打印服务器的群集是 Windows 2000 的一项新功能。 要在 Windows 2000 (或) 更高版本上运行的任何打印机端口监视器都必须进行修改，以便可以从节点的后台处理程序 (多个后台处理程序实例中调用该打印机，并) 群集后台处理程序。 必须执行以下步骤：

-   监视器的 [**InitializePrintMonitor**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor) 函数必须替换为 [**InitializePrintMonitor2**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2) 函数。 后一种函数返回监视器实例句柄。

-   必须将全局存储的变量移到本地分配的内存，并且此内存必须与 [**InitializePrintMonitor2**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)返回的监视器句柄相关联。

-   必须使用对后台处理程序的注册表函数（被传递到 [**MONITORREG**](/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitorreg) 结构中的监视器的地址）的调用替换对 WIN32 注册表 API 的调用。  (参阅 [存储端口配置信息](storing-port-configuration-information.md)。 ) 

-   端口监视器必须分为端口监视器 UI DLL 和端口监视器服务器 DLL。 UI DLL 必须通过调用后台处理程序的 [**XcvData**](/previous-versions/ff564255(v=vs.85)) 函数与服务器 dll 通信。

-   必须添加 [**Shutdown**](/previous-versions/ff562646(v=vs.85)) 函数。

未转换的打印监视器只能在非群集环境中使用。 它们不能与群集服务器一起使用。

在运行 Windows 2000 或更高版本的计算机上运行 Windows 或更高版本的群集节点上运行的打印机端口监视器已建立连接 (在网络上或在本地) ，端口监视器应在合理的时间内由后台处理程序发出的调用返回。  (后台处理程序资源超时的默认值为180秒。 有关详细信息，请参阅 [设置端口 Time-Out 值](setting-port-time-out-values.md) 。 ) 

当从一个群集节点故障转移到另一个群集节点发生故障时，后台处理程序必须等待所有当前打印作业完成或失败。 如果挂起的打印作业在端口监视器中保留的时间超过了后台处理程序资源超时时间，则后台处理程序可能会以不完整状态恢复联机状态，同时临时丢失打印机。 这可能会影响连接到缺少打印机的用户。

 

