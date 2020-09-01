---
title: HwStartIo 期间的性能提示完成请求
description: HwStartIo 期间的性能提示完成请求
ms.assetid: b1a3feff-ca18-4757-a336-c70ada998ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b10b3f792cf1da558496ec47f3ff507c7edc983
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184385"
---
# <a name="performance-tip-completing-requests-during-hwstartio"></a>性能提示：在 HwStartIo 期间完成请求


通过完成在其 [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) 例程中准备完成的未完成 i/o 请求，微型端口可以花费更少的时间来处理设备 IRQL (DIRQL) ，从而提高系统响应能力，还可以利用新的 Storport 优化，进一步提高系统响应能力和 i/o 吞吐量。 要点是尝试在中断处理程序中尽量少地花费时间。 若要利用新的 Storport 优化，可使用小型端口：

-   必须通过 StorPortInitializePerfOpts 启用 DPC 重定向[ **StorPortInitializePerfOpts**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitializeperfopts)

-   必须使用 [**StorPortNotification (NotificationType = RequestComplete) **](/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification) ，而在其 [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) 例程中，以便向 Storport 通知已完成的 i/o 请求

-   应通过 \_ \_ \_ \_ \_ \_ 在调用 [**StorPortInitializePerfOpts**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitializeperfopts) 例程的调用中将 STOR PERF OPTIMIZE FOR StartIo 设置为在 StartIo 标志

-   必须确定工作负荷的特征 (例如，在应用优化之前应存在的请求大小和吞吐量) 。

在 [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) 例程中，当启动请求的 i/o 操作后，微型端口应检查已完成的请求。

 

