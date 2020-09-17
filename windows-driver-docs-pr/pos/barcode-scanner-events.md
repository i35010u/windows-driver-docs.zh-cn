---
title: 条形码扫描仪事件
description: 使用 ReadFile 描述从设备驱动程序传递到服务 (POS) API 层的点的事件。
ms.assetid: f0a7a525-8fea-4bce-a817-25c69cd47ddd
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: c8958410ac383d3919f6843e5b11024212eb655c
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715884"
---
# <a name="barcode-scanner-events"></a>条形码扫描仪事件

本部分介绍使用 [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 本部分重点介绍条形码扫描器特定的事件。

## <a name="in-this-section"></a>在本节中

[BarcodeScannerDataReceived](barcodescannerdatareceived.md)  
在成功扫描事件之后发生。

[BarcodeScannerErrorOccurred](barcodescannererroroccurred.md)  
出现错误（例如扫描错误）时发生。

[BarcodeScannerImagePreviewReceived](barcodescannerimagepreviewreceived.md)  
在设备接收扫描的位图图像时发生。

[BarcodeScannerTriggerPressed](barcodescannertriggerpressed.md)  
按下条形码扫描器触发器时发生。

[BarcodeScannerTriggerReleased](barcodescannertriggerreleased.md)  
在释放条形码扫描器触发器时发生。