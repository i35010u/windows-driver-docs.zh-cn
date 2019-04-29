---
title: 转换打印监视器以便与群集打印服务器配合使用
description: 转换打印监视器以便与群集打印服务器配合使用
ms.assetid: 6b374d61-bb2b-42a4-9609-3cde9b82bb2b
keywords:
- 打印监视器 WDK、 群集打印服务器
- 群集打印服务器 WDK
- 聚类分析 WDK 的打印服务器
- 将转换为群集打印服务器的打印监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbb874569adeaf200cc00a20256ca711a4bd7e03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365695"
---
# <a name="converting-print-monitors-for-use-with-clustered-print-servers"></a>转换打印监视器以便与群集打印服务器配合使用





打印服务器群集是 Windows 2000 的新功能。 必须修改用于在 Windows 2000 （或更高版本） 群集上运行任何打印机端口监视器，使其可以从多个后台处理程序实例 （该节点的后台处理程序和群集后台处理程序） 调用。 必须执行以下步骤：

-   监视器[ **InitializePrintMonitor** ](https://msdn.microsoft.com/library/windows/hardware/ff551600)函数必须将其替换[ **InitializePrintMonitor2** ](https://msdn.microsoft.com/library/windows/hardware/ff551605)函数。 后一个函数返回一个监视器实例句柄。

-   全局范围内存储的变量必须移至本地分配的内存，并且此内存必须与返回的监视器句柄相关联[ **InitializePrintMonitor2**](https://msdn.microsoft.com/library/windows/hardware/ff551605)。

-   对 Win32 注册表 API 必须替换为对后台处理程序的注册表函数的调用的调用，其中的地址传递到的监视器[ **MONITORREG** ](https://msdn.microsoft.com/library/windows/hardware/ff557537)结构。 (请参阅[将端口配置信息存储](storing-port-configuration-information.md)。)

-   端口监视器必须划分端口监视器 UI DLL 和端口监视服务器 DLL。 UI DLL 必须通过调用后台处理程序的通信与服务器 DLL [ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)函数。

-   一个[**关闭**](https://msdn.microsoft.com/library/windows/hardware/ff562646)函数必须进行添加。

可以仅在非群集环境中使用不会转换的打印监视器。 它们不能用于群集服务器。

打印机端口监视运行 Windows 2000 的计算机的群集节点上运行或更高版本具有后所做的连接 （不论是通过网络或本地） 端口监视器应返回在合理时间内执行后台处理程序的调用。 （后台处理程序资源超时的默认值为 180 秒。 请参阅[设置端口超时值](setting-port-time-out-values.md)有关详细信息。)

从一个群集节点故障转移到另一个时，后台处理程序必须等待所有当前打印作业完成或失败。 如果挂起的打印作业都保存在超过后台处理程序资源超时的端口监视器，后台处理程序可能会附带回到联机状态未完成状态，暂时缺少的打印机。 这可能会影响具有连接到这些缺少的打印机的用户。

 

 




