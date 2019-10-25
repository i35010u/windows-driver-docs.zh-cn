---
title: 半双工模式不适用于随附产品
description: 半双工模式不适用于随附产品
ms.assetid: a586f340-5577-40ba-aa3e-11599f506223
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 072f1ba0bd9dd142e6a053bbce5070107c1768fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837560"
---
# <a name="half-duplex-mode-not-appropriate-for-shipped-products"></a>半双工模式：不适用于随附产品


半双工模式仅适用于将微型端口从 SCSI 端口驱动程序模型初始移植到 Storport 驱动程序模型的过程。 它将端口/微型端口同步限制为 SCSI 端口微型端口的同步，其中使用锁来同步其[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)和中断服务例程的执行。 这会导致在设备 IRQL （DIRQL）上花费更多时间，并减少 i/o 处理中的并发性，从而降低性能。 它与较新的 Storport 接口和优化不兼容，因此不适合在装运产品中使用。

如果继续寄送半双工小型端口，则在将来的 Storport 版本中会出现兼容性问题。

 

 




