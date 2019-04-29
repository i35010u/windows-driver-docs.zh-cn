---
title: 添加端口
description: 添加端口
ms.assetid: ec908ddd-761b-4a82-8fc3-ac45c39a0571
keywords:
- 端口管理 WDK 打印、 添加端口
- 添加端口
- AddPort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 613cb46a4fd7c383c008c7212bc4fd928dc36c67
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390622"
---
# <a name="adding-a-port"></a>添加端口





添加端口组成，存储端口的名称和端口监视器服务器 DLL 的本地存储中或在注册表中的用户可修改的配置信息。

当应用程序调用打印后台处理程序的端口函数 （Microsoft Windows SDK 文档中所述） 时，它作为函数参数指定端口监视器的名称。 后台处理程序调用[ **AddPortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff545026)端口监视器指定的端口监视器的 UI DLL 中包含的函数。

端口监视器 UI DLL 的[ **AddPortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff545026)函数应执行以下操作：

1.  调用打印后台处理程序的 OpenPrinter 函数 （Windows SDK 文档中介绍），这会导致[ **XcvOpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564259)中端口监视服务器 DLL 调用的函数。

2.  调用打印后台处理程序的[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)函数多次，以请求端口监视服务器 DLL 添加端口和 UI DLL 和 DLL 的服务器之间传输的配置信息。 **XcvData**函数将调用服务器 DLL 的[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)函数。 [ **AddPortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff545026)函数通常可获取配置信息从用户的显示对话框。

3.  调用打印后台处理程序的 ClosePrinter 函数 （Windows SDK 文档中介绍），这会导致[ **XcvClosePort** ](https://msdn.microsoft.com/library/windows/hardware/ff564254)中端口监视服务器 DLL 调用的函数。

有关这些操作的详细信息，请参阅的说明[ **AddPortUI**](https://msdn.microsoft.com/library/windows/hardware/ff545026)。 另请参阅[存储端口的配置信息](storing-port-configuration-information.md)。

端口监视器[ **EnumPorts** ](https://msdn.microsoft.com/library/windows/hardware/ff548754)函数必须枚举已添加的所有端口。 后台处理程序可以调用每个端口监视器**EnumPorts**函数来确定支持的打印服务器上的端口集。

 

 




