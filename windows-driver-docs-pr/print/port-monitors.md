---
title: 端口监视器
description: 端口监视器
ms.assetid: 4758ebda-f93e-49fb-8605-17cf43194afc
keywords:
- 打印监视器 WDK，端口监视器
- 端口监视器 WDK 打印
- 有关端口监视器端口监视器 WDK 打印
- 端口监视器 WDK 打印 Dll
- 打印队列 WDK，端口监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 403bda45d6816b3f365a9ebd8962c202e9464777
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370461"
---
# <a name="port-monitors"></a>端口监视器





端口监视器包含用户模式 Dll。 他们负责提供用户模式下打印后台处理程序和访问 I/O 端口硬件的内核模式端口驱动程序之间的通信路径。 通常使用一个端口，监视[ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)， **WriteFile**， **ReadFile**，和**DeviceIOControl**与内核模式端口驱动程序进行通信的 Microsoft Windows SDK 文档中所述的函数。 端口监视器也要负责管理和配置服务器的打印机端口，如中所述[管理端口](managing-a-port.md)。

NT 基于操作系统系统用户的视图的"打印机"实际上是一个或多个物理打印机设备可以连接到的打印队列。 端口是打印队列和单个打印机设备之间的物理连接。 每个端口监视器支持一个或多个类型的端口的一个或多个的实例。 例如 Localmon.dll，[示例端口监视器](sample-port-monitor.md)，可以支持的所有服务器的本地 COM 和 LPT 端口。 (打印文件夹中分配端口为端口监视器，通过调用 Windows SDK 文档**AddPrinter**函数。)

对于表示多个打印机设备 （通过多个端口） 的打印队列，后台处理程序将每个打印作业发送到第一个可用端口。 如果端口监视器指示指定的端口正忙或遇到错误，后台处理程序将重新提交到队列中，指定另一个端口支持的端口监视器作业。

除了 Localmon.dll，Windows 2000 和更高版本的操作系统版本提供几个其他端口监视器。 *Windows 2000 Server Resource Kit*描述了每个这些端口监视器。 （此资源可能不会在某些语言和国家/地区中可用。）

可以编写自定义的端口监视器，以支持其他类型的 I/O 端口硬件。

Windows 2000 和更高版本，则每个端口监视器分为两个 Dll:

<a href="" id="port-monitor-ui-dll-"></a>**端口监视器 UI DLL**   
端口监视器的用户界面 DLL 包含用户界面功能并打印客户端系统上执行。

此 DLL 必须驻留在客户端系统的 System32 子目录。

<a href="" id="port-monitor-server-dll-"></a>**端口监视服务器 DLL**   
端口监视的服务器 DLL 包含端口的通信功能，并在打印服务器上执行。 它必须显示用户界面。

通过调用后台处理程序的 UI DLL 与服务器 DLL 进行通信[ **XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))函数。

一个[示例端口监视器](sample-port-monitor.md)包括 Windows Driver Kit (WDK) 中。

 

 




