---
title: 条形码扫描仪事件
description: 使用 ReadFile 了解从设备驱动程序传递到服务 (POS) API 层的点的条形码扫描器事件。
ms.assetid: f0a7a525-8fea-4bce-a817-25c69cd47ddd
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc8a19e092f45b10f3c947cd51e241ca7f6a4349
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590383"
---
# <a name="barcode-scanner-events"></a>条形码扫描仪事件

本部分介绍使用 [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 本部分重点介绍条形码扫描器特定的事件。

## <a name="in-this-section"></a>在此部分中

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