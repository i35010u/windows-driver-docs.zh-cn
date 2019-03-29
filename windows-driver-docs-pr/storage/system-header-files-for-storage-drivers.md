---
title: 存储驱动程序的系统标头文件
description: 存储驱动程序的系统标头文件
ms.assetid: 2ee83fa4-41df-403e-86b8-b269f5dfbfed
keywords:
- 存储驱动程序 WDK，系统标头文件
- 标头文件 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 780d4af5f6f9135cfce23cfde3fcde1e4b91b765
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567856"
---
# <a name="system-header-files-for-storage-drivers"></a>存储驱动程序的系统标头文件


## <span id="ddk_system_header_files_for_storage_drivers_kg"></span><span id="DDK_SYSTEM_HEADER_FILES_FOR_STORAGE_DRIVERS_KG"></span>


系统提供的存储驱动程序包括标头文件*scsi.h*，它包含的 Cdb SCSI 符合定义和其他结构由大多数 SCSI 兼容的驱动程序。 此标头文件包含*srb.h*，用于定义到下一步低存储类和筛选器驱动程序的系统提供的端口驱动程序提供的接口。

独立于操作系统的 SCSI 微型端口驱动程序，可以将其设计为运行与基于 NT 的操作系统的所有平台和与仅限 x86 的 Microsoft Windows 系统，包括系统提供的标头文件*miniport.h*并*scsi.h*，其中包括*srb.h*。

磁带 miniclass 驱动程序包括*minitape.h*。

媒体更换器 miniclass 驱动程序包括*mcd.h*。

供应商提供的类和筛选器驱动程序还可以将示例文件*classpnp.h*并*classpnp.c*。 这些文件定义了一系列**类**Xxx 例程，可简化设计的类和筛选器驱动程序。 但是， *classpnp.h*并*classpnp.c*是仅示例，并不支持任何版本的 Windows 操作系统中。 因为时应该格外谨慎使用到生产环境的驱动程序，这些文件中的结构和例程声明的一些*classpnp.h*可能不是最新或可能与您的驱动程序在运行的 Windows 的版本不兼容。

 

 




