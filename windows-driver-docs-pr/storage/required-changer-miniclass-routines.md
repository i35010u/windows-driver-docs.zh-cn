---
title: 必需的更换器微型类例程
description: 必需的更换器微型类例程
ms.assetid: bd706c00-5f6b-4bda-b6a1-a61046303e12
keywords:
- 更换器驱动程序 WDK 存储，miniclass 驱动程序
- 存储更换器驱动程序 WDK，miniclass 驱动程序
- miniclass 驱动程序 WDK 换带机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b180062444034fadf24cc4889cd4d536f4cec36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356644"
---
# <a name="required-changer-miniclass-routines"></a>必需的更换器微型类例程


## <span id="ddk_required_changer_miniclass_routines_kg"></span><span id="DDK_REQUIRED_CHANGER_MINICLASS_ROUTINES_KG"></span>


换带机 miniclass 驱动程序必须具有由转换器类驱动程序调用以下例程：

-   **DriverEntry** -在 Windows XP 和更高版本操作系统，换带机 miniclass 驱动程序的**DriverEntry**例程调用转换器类驱动程序[ **ChangerClassInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerclassinitialize)例程，以初始化的驱动程序。 请参阅[转换器类驱动程序版本差异](differences-in-changer-class-driver-versions.md)有关详细信息。 换带机 miniclass 驱动程序不具有**DriverEntry**例程在 Windows 2000 中。

-   [**ChangerAdditionalExtensionSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changeradditionalextensionsize)指示的额外空间 miniclass 驱动程序需要特定于设备的信息的转换器的设备扩展中的字节数。

-   [**ChangerInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerinitialize)准备换带机接收其他请求。

-   [**ChangerError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changererror)执行特定于设备的错误处理后的转换器类驱动程序执行了任何独立于设备的错误处理。

-   [**ChangerExchangeMedium** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerexchangemedium)并[ **ChangerMoveMedium** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changermovemedium)换带机中的元素之间移动媒体。

-   [**ChangerReinitializeUnit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerreinitializeunit)， [ **ChangerSetAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changersetaccess)，以及[ **ChangerSetPosition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changersetposition)位置元素和控制对其的访问。

-   [**ChangerGetElementStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changergetelementstatus)， [ **ChangerGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changergetparameters)， [ **ChangerGetProductData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changergetproductdata)，[ **ChangerGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changergetstatus)， [ **ChangerInitializeElementStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerinitializeelementstatus)，并[ **ChangerQueryVolumeTags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mcd/nf-mcd-changerqueryvolumetags)获取和的情况下**ChangerQueryVolumeTags**，设置各种类型的转换器的信息。

换带机 miniclass 驱动程序例程通常用命令描述符块 (CDB) 合适的命令，生成 SCSI 请求块 (SRB)，并将 Srb 发送到系统端口驱动程序。

如果转换器不支持权限隐含的给定的例程的功能，以便它将返回状态，其驱动程序必须实现例程\_无效\_设备\_请求。

有关所需的详细信息 **换带机 * * * Xxx*例程换带机 miniclass 驱动程序，请参阅[换带机 Miniclass 驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 有关设备控制请求的特定于转换器的 I/O 控制代码的详细信息，请参阅[换带机 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

 

 




