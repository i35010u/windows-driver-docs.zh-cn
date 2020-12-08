---
title: 将数据上传到设备
description: 将数据上传到设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c4748810d5606187efdc44fdc0defaacd773b27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796179"
---
# <a name="uploading-data-to-a-device"></a>将数据上传到设备


若要将数据从应用程序传输到设备，必须使用 **IWiaTransfer：：上传** 方法。 应用程序提供数据流，该数据流用作数据源而不是目标。 同样，驱动程序在上载情况下调用 **istream：： Read** 而不是 **Istream：： Write** 。

请注意，此上载过程只能在已存在的项上执行。 如果应用程序尝试将新文件上传到具有存储的设备，则无法完成此过程，因为尚不存在表示该文件的项目。

若要在设备上创建新内容（例如设备存储上的新文件），应用程序应执行以下操作：

1.  通过对将成为项父级的文件夹调用 **IWiaItem2：： CreateChildItem** 来创建 WIA 项。

2.  为 **IWiaTransfer** 调用 **QueryInterface** ，然后调用 **IWiaTransfer：：上传**。

驱动程序应相应地处理对 **IWiaTransfer：：上传** 的调用。 例如，如果 WIA 项为新项，则驱动程序应创建文件，并将 **IWiaTransfer：：上** 提供的源流的内容保存到设备存储中。

Microsoft Windows SDK 文档中介绍了 **IWiaTransfer**、 **IWiaItem2**、 **IwiaDataTransfer** 和 **IStream** 接口。

本节包括：

[上传时的驱动程序行为](driver-behavior-on-upload.md)

 

 




