---
title: 删除端口
description: 删除端口
ms.assetid: 0d491368-e529-4f04-a323-678e31a862c3
keywords:
- 端口管理 WDK 打印，删除端口
- 正在删除打印端口
- 删除打印端口
- DeletePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e42208e39f06de3ac4c56b92e3e6ae9b91949c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562815"
---
# <a name="deleting-a-port"></a>删除端口





删除端口组成，从端口监视器服务器 DLL 的本地存储或从注册表中删除端口的存储的名称和用户可修改的配置信息。

当应用程序调用打印后台处理程序的**DeletePort**函数 （Microsoft Windows SDK 文档中介绍）， **DeletePort**函数调用[ **DeletePortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff547432)端口监视器 UI DLL 的适当的端口监视器中包含的函数。

端口监视器 UI DLL 的**DeletePortUI**函数应执行以下操作：

1.  调用打印后台处理程序的**OpenPrinter**函数 （Windows SDK 文档中介绍），这会导致[ **XcvOpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564259)端口监视服务器 DLL 中的函数若要调用。

2.  调用打印后台处理程序的[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)函数的一个或多个时间，以请求端口监视服务器 DLL 以删除该端口。 **XcvData**函数将调用服务器 DLL 的[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)函数。

3.  调用打印后台处理程序的**ClosePrinter**函数 （Windows SDK 文档中介绍），这会导致[ **XcvClosePort** ](https://msdn.microsoft.com/library/windows/hardware/ff564254)端口监视服务器中的函数若要调用的 DLL。

有关这些操作的详细信息，请参阅的说明[ **DeletePortUI**](https://msdn.microsoft.com/library/windows/hardware/ff547432)。

 

 




