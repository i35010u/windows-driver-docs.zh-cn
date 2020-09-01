---
title: 条形码扫描仪事件
description: 使用 ReadFile 描述从设备驱动程序传递到服务 (POS) API 层的点的事件。
ms.assetid: f0a7a525-8fea-4bce-a817-25c69cd47ddd
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: caff693ed643e151953e3693713e0355e38172df
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192267"
---
# <a name="barcode-scanner-events"></a>条形码扫描仪事件

本部分介绍使用 [ReadFile](/windows/desktop/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 本部分重点介绍条形码扫描器特定的事件。

## <a name="in-this-section"></a>本节内容

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