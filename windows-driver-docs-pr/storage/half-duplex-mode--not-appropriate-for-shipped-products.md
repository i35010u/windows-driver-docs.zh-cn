---
title: Half-Duplex 模式不适用于随附产品
description: Half-Duplex 模式不适用于随附产品
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0652441050a61aee320f76cd6ab3bbb5265f0cfa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804541"
---
# <a name="half-duplex-mode-not-appropriate-for-shipped-products"></a>Half-Duplex 模式：不适用于已发布产品


半双工模式仅适用于将微型端口从 SCSI 端口驱动程序模型初始移植到 Storport 驱动程序模型的过程。 它将端口/微型端口同步限制为 SCSI 端口微型端口的同步，其中使用锁来同步其 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 和中断服务例程的执行。 这会导致花费更多时间在设备 IRQL (DIRQL) 并减少 i/o 处理中的并发性，从而降低性能。 它与较新的 Storport 接口和优化不兼容，因此不适合在装运产品中使用。

如果继续寄送半双工小型端口，则在将来的 Storport 版本中会出现兼容性问题。

 

