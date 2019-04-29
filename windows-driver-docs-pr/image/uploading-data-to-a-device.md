---
title: 将数据上传到设备
description: 将数据上传到设备
ms.assetid: 50fc5f56-3758-4151-9748-dd88544006f1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c4360ef2d67d65fb65d7cc23399b63cee95fb8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383706"
---
# <a name="uploading-data-to-a-device"></a>将数据上传到设备


若要将数据传输到设备应用程序中，必须使用**IWiaTransfer::Upload**方法。 该应用程序提供数据流，将其用作数据源而不是目标。 同样，驱动程序调用**IStream::Read**而不是**IStream::Write**中上传这种情况。

请注意，可以仅在已存在的项上执行此上传过程。 如果应用程序尝试将新文件上传到设备的存储，因为没有项来表示该文件尚不能完成此过程。

若要在设备上，如设备存储中，新的文件创建新的内容应用程序应当：

1.  通过调用创建 WIA 项**IWiaItem2::CreateChildItem**上将成为项的父级的文件夹。

2.  调用**QueryInterface**有关**IWiaTransfer**，然后调用**IWiaTransfer::Upload**。

该驱动程序应处理对**IWiaTransfer::Upload**相应地。 例如，如果 WIA 项是新项，该驱动程序应创建文件并保存源流中提供的内容**IWiaTransfer::Upload**到设备存储。

**IWiaTransfer**， **IWiaItem2**， **IwiaDataTransfer**，以及**IStream**接口在 Microsoft Windows SDK 中所述文档。

本部分包括：

[上传的驱动程序行为](driver-behavior-on-upload.md)

 

 




