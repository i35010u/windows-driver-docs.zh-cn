---
title: 删除端口
description: 删除端口
ms.assetid: 0d491368-e529-4f04-a323-678e31a862c3
keywords:
- 端口管理 WDK 打印，删除端口
- 删除打印端口
- 删除打印端口
- DeletePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e3c494d631b54abcff1275b063a8f7126793d96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838882"
---
# <a name="deleting-a-port"></a>删除端口





删除端口包括从端口监视器服务器 DLL 的本地存储或注册表中删除端口的存储名称和用户可修改的配置信息。

当应用程序调用打印后台处理程序的**DeletePort**函数（如 Microsoft Windows SDK 文档中所述）时， **DeletePort**函数会调用的端口监视器 UI DLL 中包含的[**DeletePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui)函数适当的端口监视器。

端口监视器 UI DLL 的**DeletePortUI**函数应执行以下操作：

1.  调用打印后台处理程序的**OpenPrinter**函数（如 Windows SDK 文档中所述），这会导致调用端口监视器服务器 DLL 中的[**XcvOpenPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport)函数。

2.  一次或多次调用打印后台处理程序的[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))函数，请求端口监视器服务器 DLL 删除该端口。 **XcvData**函数调用服务器 DLL 的[**XcvDataPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)函数。

3.  调用打印后台处理程序的**ClosePrinter**函数（如 Windows SDK 文档中所述），这会导致调用端口监视器服务器 DLL 中的[**XcvClosePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport)函数。

有关这些操作的详细信息，请参阅[**DeletePortUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui)的说明。

 

 




