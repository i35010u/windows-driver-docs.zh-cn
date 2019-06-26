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
ms.openlocfilehash: 9cfd3480d7f509280c5cbd43f2e925b784d80747
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369007"
---
# <a name="adding-a-port"></a>添加端口





添加端口组成，存储端口的名称和端口监视器服务器 DLL 的本地存储中或在注册表中的用户可修改的配置信息。

当应用程序调用打印后台处理程序的端口函数 （Microsoft Windows SDK 文档中所述） 时，它作为函数参数指定端口监视器的名称。 后台处理程序调用[ **AddPortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)端口监视器指定的端口监视器的 UI DLL 中包含的函数。

端口监视器 UI DLL 的[ **AddPortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)函数应执行以下操作：

1.  调用打印后台处理程序的 OpenPrinter 函数 （Windows SDK 文档中介绍），这会导致[ **XcvOpenPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvopenport)中端口监视服务器 DLL 调用的函数。

2.  调用打印后台处理程序的[ **XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))函数多次，以请求端口监视服务器 DLL 添加端口和 UI DLL 和 DLL 的服务器之间传输的配置信息。 **XcvData**函数将调用服务器 DLL 的[ **XcvDataPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvdataport)函数。 [ **AddPortUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)函数通常可获取配置信息从用户的显示对话框。

3.  调用打印后台处理程序的 ClosePrinter 函数 （Windows SDK 文档中介绍），这会导致[ **XcvClosePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-xcvcloseport)中端口监视服务器 DLL 调用的函数。

有关这些操作的详细信息，请参阅的说明[ **AddPortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)。 另请参阅[存储端口的配置信息](storing-port-configuration-information.md)。

端口监视器[ **EnumPorts** ](https://docs.microsoft.com/previous-versions/ff548754(v=vs.85))函数必须枚举已添加的所有端口。 后台处理程序可以调用每个端口监视器**EnumPorts**函数来确定支持的打印服务器上的端口集。

 

 




