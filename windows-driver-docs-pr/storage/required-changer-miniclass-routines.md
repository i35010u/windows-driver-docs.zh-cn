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
ms.openlocfilehash: 92d8658dc896b852bb854f887cd0112ed5613852
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575724"
---
# <a name="required-changer-miniclass-routines"></a>必需的更换器微型类例程


## <span id="ddk_required_changer_miniclass_routines_kg"></span><span id="DDK_REQUIRED_CHANGER_MINICLASS_ROUTINES_KG"></span>


换带机 miniclass 驱动程序必须具有由转换器类驱动程序调用以下例程：

-   **DriverEntry** -在 Windows XP 和更高版本操作系统，换带机 miniclass 驱动程序的**DriverEntry**例程调用转换器类驱动程序[ **ChangerClassInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff551413)例程，以初始化的驱动程序。 请参阅[转换器类驱动程序版本差异](differences-in-changer-class-driver-versions.md)有关详细信息。 换带机 miniclass 驱动程序不具有**DriverEntry**例程在 Windows 2000 中。

-   [**ChangerAdditionalExtensionSize** ](https://msdn.microsoft.com/library/windows/hardware/ff551400)指示的额外空间 miniclass 驱动程序需要特定于设备的信息的转换器的设备扩展中的字节数。

-   [**ChangerInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff551431)准备换带机接收其他请求。

-   [**ChangerError** ](https://msdn.microsoft.com/library/windows/hardware/ff551418)执行特定于设备的错误处理后的转换器类驱动程序执行了任何独立于设备的错误处理。

-   [**ChangerExchangeMedium** ](https://msdn.microsoft.com/library/windows/hardware/ff551421)并[ **ChangerMoveMedium** ](https://msdn.microsoft.com/library/windows/hardware/ff551436)换带机中的元素之间移动媒体。

-   [**ChangerReinitializeUnit**](https://msdn.microsoft.com/library/windows/hardware/ff551443)， [ **ChangerSetAccess**](https://msdn.microsoft.com/library/windows/hardware/ff551447)，以及[ **ChangerSetPosition** ](https://msdn.microsoft.com/library/windows/hardware/ff551449)位置元素和控制对其的访问。

-   [**ChangerGetElementStatus**](https://msdn.microsoft.com/library/windows/hardware/ff551424)， [ **ChangerGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff551425)， [ **ChangerGetProductData**](https://msdn.microsoft.com/library/windows/hardware/ff551427)，[ **ChangerGetStatus**](https://msdn.microsoft.com/library/windows/hardware/ff551429)， [ **ChangerInitializeElementStatus**](https://msdn.microsoft.com/library/windows/hardware/ff551433)，并[ **ChangerQueryVolumeTags** ](https://msdn.microsoft.com/library/windows/hardware/ff551440)获取和的情况下**ChangerQueryVolumeTags**，设置各种类型的转换器的信息。

换带机 miniclass 驱动程序例程通常用命令描述符块 (CDB) 合适的命令，生成 SCSI 请求块 (SRB)，并将 Srb 发送到系统端口驱动程序。

如果转换器不支持权限隐含的给定的例程的功能，以便它将返回状态，其驱动程序必须实现例程\_无效\_设备\_请求。

有关所需的详细信息 **换带机 * * * Xxx*例程换带机 miniclass 驱动程序，请参阅[换带机 Miniclass 驱动程序例程](https://msdn.microsoft.com/library/windows/hardware/ff551472)。 有关设备控制请求的特定于转换器的 I/O 控制代码的详细信息，请参阅[换带机 I/O 控制代码](https://msdn.microsoft.com/library/windows/hardware/ff551469)。

 

 




