---
title: HwStartIo 期间的性能提示完成请求
description: HwStartIo 期间的性能提示完成请求
ms.assetid: b1a3feff-ca18-4757-a336-c70ada998ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2306eb8a287161add12ab2578b8fdeff45258f6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842729"
---
# <a name="performance-tip-completing-requests-during-hwstartio"></a>性能提示：在 HwStartIo 期间完成请求


通过完成在其[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)例程中准备完成的未完成 i/o 请求，微型端口可以花费更少的时间来处理设备 IRQL （DIRQL），从而提高系统响应能力，还可以利用新的 Storport 优化进一步提高系统响应能力和 i/o 吞吐量。 要点是尝试在中断处理程序中尽量少地花费时间。 若要利用新的 Storport 优化，可使用小型端口：

-   必须通过 StorPortInitializePerfOpts 启用 DPC 重定向[](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitializeperfopts)

-   必须在其[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)例程中使用[**StorPortNotification （NotificationType = RequestComplete）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification)来向 Storport 通知已完成的 i/o 请求

-   应通过设置 STOR\_PERF\_优化\_，使其在 StartIo 过程中完成，方法是在对[**StorPortInitializePerfOpts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitializeperfopts)例程的调用中将\_StartIo 标志设置为\_完成\_

-   必须确定在应用优化之前应存在的工作负荷的特征（例如，请求大小和吞吐量）。

在[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)例程中，当启动请求的 i/o 操作后，微型端口应检查已完成的请求。

 

 




