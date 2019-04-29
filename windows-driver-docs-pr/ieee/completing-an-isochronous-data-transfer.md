---
title: 完成常时等量数据传输
description: 完成常时等量数据传输
ms.assetid: 1fc98e1b-4dd5-4358-aa23-86fcbbf33967
keywords:
- 同步 I/O WDK IEEE 1394 总线，完成传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d067da9616af8750db5e27f30322c1c29cc81ef1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376700"
---
# <a name="completing-an-isochronous-data-transfer"></a>完成常时等量数据传输





一旦设备不再需要将数据传输，该驱动程序必须通知总线操作已完成，而且然后释放它分配设置时的同步资源。

驱动程序必须执行以下步骤来清理：

1.  如果该驱动程序已开始同步操作通过[**请求\_ISOCH\_侦听**](https://msdn.microsoft.com/library/windows/hardware/ff537655)或者[**请求\_ISOCH\_交流**](https://msdn.microsoft.com/library/windows/hardware/ff537660)总线请求时，必须颁发[**请求\_ISOCH\_停止**](https://msdn.microsoft.com/library/windows/hardware/ff537659)请求发出信号总线若要停止同步操作的驱动程序。

2.  必须通过使用分离附加到资源句柄保留任何缓冲区[**请求\_ISOCH\_分离\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff537651)请求。

3.  如果该驱动程序已分配的资源句柄，则它必须释放它通过[**请求\_ISOCH\_免费\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff537654)请求。

4.  如果该驱动程序有一个分配的通道，它必须释放它通过[**请求\_ISOCH\_免费\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff537653)请求。

5.  该驱动程序必须解除分配它已经分配了通过使用任何带宽[**请求\_ISOCH\_免费\_带宽**](https://msdn.microsoft.com/library/windows/hardware/ff537652)请求。

 

 




