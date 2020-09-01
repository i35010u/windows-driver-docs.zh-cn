---
title: 必需的更换器微型类例程
description: 必需的更换器微型类例程
ms.assetid: bd706c00-5f6b-4bda-b6a1-a61046303e12
keywords:
- 转换器驱动程序 WDK 存储，miniclass 驱动程序
- 存储更换器驱动程序 WDK、miniclass 驱动程序
- miniclass 驱动程序 WDK 转换器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d807a34699b8dbe8c86166d2d7d75621f95c9d58
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191115"
---
# <a name="required-changer-miniclass-routines"></a>必需的更换器微型类例程


## <span id="ddk_required_changer_miniclass_routines_kg"></span><span id="DDK_REQUIRED_CHANGER_MINICLASS_ROUTINES_KG"></span>


转换器 miniclass 驱动程序必须具有以下由转换器类驱动程序调用的例程：

-   **DriverEntry** --在 Windows XP 及更高版本的操作系统中，转换器 miniclass 驱动程序的 **DriverEntry** 例程会调用变换器类驱动程序的 [**ChangerClassInitialize**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize) 例程来初始化该驱动程序。 有关详细信息，请参阅 [转换器类驱动程序版本中的差异](differences-in-changer-class-driver-versions.md) 。 转换器 miniclass 驱动程序在 Windows 2000 中没有 **DriverEntry** 例程。

-   [**ChangerAdditionalExtensionSize**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changeradditionalextensionsize) 指示 miniclass 驱动程序在设备特定信息的设备扩展中所需的额外空间字节数。

-   [**ChangerInitialize**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerinitialize) 准备转换器以接收其他请求。

-   在变换器类驱动程序执行任何与设备无关的错误处理后， [**ChangerError**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changererror)执行特定于设备的错误处理。

-   [**ChangerExchangeMedium**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerexchangemedium) 和 [**ChangerMoveMedium**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changermovemedium) 在变换器中的元素之间移动媒体。

-   [**ChangerReinitializeUnit**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerreinitializeunit)、 [**ChangerSetAccess**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changersetaccess)和 [**ChangerSetPosition**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changersetposition) position 元素，并控制对它们的访问。

-   [**ChangerGetElementStatus**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changergetelementstatus)、 [**ChangerGetParameters**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changergetparameters)、 [**ChangerGetProductData**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changergetproductdata)、 [**ChangerGetStatus**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changergetstatus)、 [**ChangerInitializeElementStatus**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerinitializeelementstatus)和 [**ChangerQueryVolumeTags**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerqueryvolumetags) 获取和，对于 **ChangerQueryVolumeTags**，请设置各种类型的转换器信息。

转换器 miniclass 驱动程序例程通常 (SRB)  (CDB) 为相应的命令生成 SCSI 请求块，并将 SRBs 发送到系统端口驱动程序。

如果转换器不支持给定例程隐含的功能，则其驱动程序必须实现例程，使其返回状态 " \_ 无效 \_ 设备请求" \_ 。

有关 miniclass 驱动程序的必需 **变换器 * * * Xxx* 例程的详细信息，请参阅 [转换器 Miniclass 驱动程序例程](/windows-hardware/drivers/ddi/index)。 有关设备控制请求的更换器特定 i/o 控制代码的详细信息，请参阅 [转换器 I/o 控制代码](/windows-hardware/drivers/ddi/index)。

 

