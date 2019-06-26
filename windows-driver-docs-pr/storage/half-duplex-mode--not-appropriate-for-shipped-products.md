---
title: 半双工模式不适用于已发布产品
description: 半双工模式不适用于已发布产品
ms.assetid: a586f340-5577-40ba-aa3e-11599f506223
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdacb9244eacd7a83b78cd8737732219cfc4c208
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378513"
---
# <a name="half-duplex-mode-not-appropriate-for-shipped-products"></a>半双工模式：不适合寄送的产品


半双工模式用于仅在初始移植到 Storport 驱动程序模型微型端口从 SCSI 端口驱动程序模型。 它将限制为 SCSI 端口微型端口，其中使用锁来同步执行的端口/微型端口同步其[ **StartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)和中断服务例程。 这会导致花费更多时间在设备的 IRQL (DIRQL)，并减少 I/O 处理，从而导致较低的性能中的并发。 它与较新 Storport 接口和优化，不兼容，因此不适合在发运产品的使用。

如果您继续半双工微型端口，则可能会与 Storport 的未来版本的兼容性问题。

 

 




