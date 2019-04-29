---
title: 条形码扫描仪事件
description: 介绍从传递的设备驱动程序到点的服务 (POS) API 层通过 ReadFile 的事件。
ms.assetid: f0a7a525-8fea-4bce-a817-25c69cd47ddd
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5bdcc7015e81ec91a46e2481c2e7753b889c3ddf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358673"
---
# <a name="barcode-scanner-events"></a>条形码扫描仪事件

本部分介绍从设备驱动程序到点的服务 (POS) API 层通过使用传递的事件[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)。 本部分重点介绍特定于条码扫描器的事件。

## <a name="in-this-section"></a>本节内容

[BarcodeScannerDataReceived](barcodescannerdatareceived.md)  
在成功扫描事件后发生。

[BarcodeScannerErrorOccurred](barcodescannererroroccurred.md)  
当出现错误，例如扫描错误时发生。

[BarcodeScannerImagePreviewReceived](barcodescannerimagepreviewreceived.md)  
当设备接收扫描的位图图像时发生。

[BarcodeScannerTriggerPressed](barcodescannertriggerpressed.md)  
条形码扫描程序触发器按下时发生。

[BarcodeScannerTriggerReleased](barcodescannertriggerreleased.md)  
当释放条形码扫描程序触发器时发生。
