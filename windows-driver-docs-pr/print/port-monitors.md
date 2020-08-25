---
title: 端口监视器
description: 端口监视器
ms.assetid: 4758ebda-f93e-49fb-8605-17cf43194afc
keywords:
- 打印监视器 WDK，端口监视器
- 端口监视 WDK 打印
- 端口监视 WDK 打印，关于端口监视器
- 端口监视 WDK 打印，Dll
- 打印队列 WDK，端口监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75ec11a2b8b511b770b00673e95822fdb2f3f5e8
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802403"
---
# <a name="port-monitors"></a>端口监视器





端口监视器由用户模式 Dll 组成。 它们负责提供用户模式打印后台处理程序与访问 i/o 端口硬件的内核模式端口驱动程序之间的通信路径。 端口监视器通常使用 Microsoft Windows SDK 文档中所述的 [**CreateFile**](https://docs.microsoft.com/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **WriteFile**、 **ReadFile**和 **DeviceIOControl** 函数来与内核模式端口驱动程序通信。 端口监视器还负责管理和配置服务器的打印机端口，如 [管理端口](managing-a-port.md)中所述。

"打印机" 的基于 NT 的操作系统用户视图实际上是一个打印队列，可以将一个或多个物理打印机设备连接到该队列。 端口是打印队列和单个打印机设备之间的物理连接。 每个端口监视器支持一个或多个类型的端口的一个或多个实例。 例如 Localmon.dll， [示例端口监视器](sample-port-monitor.md)可支持服务器的所有本地 COM 和 LPT 端口。  (打印文件夹，可通过调用 Windows SDK 文档的 **interactivesession.addprinter** 函数将端口分配给端口监视器。 ) 

对于表示多个打印机设备的打印队列 (通过多个端口) ，后台处理程序将每个打印作业发送到第一个可用端口。 如果端口监视器指示指定的端口正忙或遇到错误，则后台处理程序会将作业重新提交到队列，同时指定端口监视器支持的其他端口。

除了 Localmon.dll 之外，Windows 2000 和更高版本的操作系统版本还提供多个其他端口监视器。 *Windows 2000 服务器资源工具包*介绍了其中的每个端口监视器。  (此资源可能在某些语言和国家/地区不可用。 ) 

可以编写自定义端口监视器以支持其他类型的 i/o 端口硬件。

对于 Windows 2000 和更高版本，每个端口监视器均分为两个 Dll：

<a href="" id="port-monitor-ui-dll-"></a>**端口监视器 UI DLL**   
端口监视器的用户界面 DLL 包含用户界面功能，并在打印客户端系统上执行。

此 DLL 必须位于客户端系统的 System32 子目录下。

<a href="" id="port-monitor-server-dll-"></a>**端口监视器服务器 DLL**   
端口监视器的服务器 DLL 包含端口通信功能，并在打印服务器上执行。 它不能显示用户界面。

UI DLL 通过调用后台处理程序的 [**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85)) 函数与服务器 dll 通信。

Windows 驱动程序工具包中包含了一个 [示例端口监视器](sample-port-monitor.md) (WDK) 。

 

 




