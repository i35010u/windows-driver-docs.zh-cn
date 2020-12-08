---
title: 存储驱动程序的系统标头文件
description: 存储驱动程序的系统标头文件
keywords:
- 存储驱动程序 WDK，系统头文件
- 标头文件 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20891b3c8b3c5c4258497e7368fb42f602679ebc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834919"
---
# <a name="system-header-files-for-storage-drivers"></a>存储驱动程序的系统标头文件


## <span id="ddk_system_header_files_for_storage_drivers_kg"></span><span id="DDK_SYSTEM_HEADER_FILES_FOR_STORAGE_DRIVERS_KG"></span>


系统提供的存储驱动程序包括头文件 *scsi-3*，其中包含适用于 CDBS 的 scsi 兼容定义和与大多数符合 scsi 标准的驱动程序所使用的其他结构。 此标头文件包含 *srb*，它定义由系统提供的端口驱动程序提供给下一个较低存储类和筛选器驱动程序的接口。

独立于操作系统的 SCSI 微型端口驱动程序可设计为在基于 NT 的 *操作系统和仅* 限 X86 的 Microsoft Windows 系统的所有平台上运行，包括系统提供的标头文件 srb 和 *scsi-3*，其中包括 *srb.h*。

磁带 miniclass 驱动程序包括 *minitape*。

媒体转换器 miniclass 驱动程序包括 *mcd*。

供应商提供的类和筛选器驱动程序还可以合并示例文件 *classpnp* 和 *classpnp*。 这些文件定义了一系列 **类** Xxx 例程，可简化类和筛选器驱动程序的设计。 但是， *classpnp* 和 *classpnp* 只是示例，在任何 Windows 操作系统版本中都不受支持。 在生产驱动程序中使用这些文件时要格外小心，因为 *classpnp* 中的某些结构和例程声明可能不是最新的，或者可能与你的驱动程序运行所在的 Windows 版本不兼容。

 

 




