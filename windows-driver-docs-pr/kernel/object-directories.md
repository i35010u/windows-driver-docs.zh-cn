---
title: 对象目录
description: 对象目录
ms.assetid: b0e0d077-6736-4a54-b1eb-a30962442942
keywords:
- 对象目录 WDK 内核
- 命名的对象 WDK 内核
- 目录 WDK 对象
- 顶级对象目录 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28fe256e7ea82465e2d1e3f111483654b1d715c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365385"
---
# <a name="object-directories"></a>对象目录





*对象目录*仅用于包含其他命名的对象命名的对象。 例如， **\\设备**对象目录包含由驱动程序创建的已命名的设备对象。

不要混淆对象目录与文件系统目录。 对象目录仅存在于对象管理器，并不对应于磁盘上的任何目录。 （文件系统目录，实际上，表示为文件对象。）

下面是包含驱动程序可能会创建或使用的对象的顶级对象目录的列表：

-   **\\回调**

    系统会在此目录中创建标准的回调对象。 有关详细信息，请参阅[使用系统定义的回调对象](using-a-system-defined-callback-object.md)。

-   **\\设备**

    驱动程序在此目录中创建命名的设备对象。 有关详细信息，请参阅[名为设备对象](named-device-objects.md)。

-   **\\KernelObjects**

    系统会在此目录中创建标准事件对象。 有关详细信息，请参阅[标准事件对象](standard-event-objects.md)。

-   **\\DosDevices**

    此目录将设备的 MS-DOS 设备名称存储为相应的设备对象的符号链接。 有关详细信息，请参阅[MS-DOS 设备名称](ms-dos-device-names.md)。

系统会创建其他顶级目录，但它们是保留供系统使用。

驱动程序可以通过调用创建新对象目录[ **ZwCreateDirectoryObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)例程。

 

 




