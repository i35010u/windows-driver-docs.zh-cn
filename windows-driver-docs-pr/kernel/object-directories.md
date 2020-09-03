---
title: 对象目录
description: 对象目录
ms.assetid: b0e0d077-6736-4a54-b1eb-a30962442942
keywords:
- 对象目录 WDK 内核
- 命名对象 WDK 内核
- 目录 WDK 对象
- 顶级对象目录 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07fe246a8e05e3a2079b2774ab79a8c0ea9d0083
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403128"
---
# <a name="object-directories"></a>对象目录





*对象目录*是一个仅用于包含其他命名对象的命名对象。 例如， ** \\ 设备**对象目录包含驱动程序创建的已命名设备对象。

不要将对象目录与文件系统目录混淆。 对象目录仅在对象管理器中存在，并且不与磁盘上的任何目录相对应。 事实上， (文件系统目录表示为文件对象。 ) 

下面列出了包含对象驱动程序可能创建或使用的顶级对象目录：

-   **\\回调**

    系统将在此目录中创建标准的回调对象。 有关详细信息，请参阅 [使用系统定义的回调对象](using-a-system-defined-callback-object.md)。

-   **\\设备**

    驱动程序在此目录中创建命名设备对象。 有关详细信息，请参阅 [命名设备对象](named-device-objects.md)。

-   **\\KernelObjects**

    系统将在此目录中创建标准事件对象。 有关详细信息，请参阅 [标准事件对象](standard-event-objects.md)。

-   **\\DosDevices**

    此目录将设备的 MS-DOS 设备名称存储为对应设备对象的符号链接。 有关详细信息，请参阅 [MS-DOS 设备名称](introduction-to-ms-dos-device-names.md)。

系统会创建其他顶级目录，但它们保留供系统使用。

驱动程序可以通过调用 [**ZwCreateDirectoryObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject) 例程来创建新的对象目录。

 

