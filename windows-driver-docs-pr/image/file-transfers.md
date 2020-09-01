---
title: 文件传输
description: 文件传输
ms.assetid: 1c776dc5-982a-4652-bc03-f334fda30055
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19cfe9fcc224ea8be12c53ae1424f9c0f8691410
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192081"
---
# <a name="file-transfers"></a>文件传输





**注意**   文件传输适用于 Windows Vista 之前的操作系统。

 

*文件数据传输*是将来自 wia 微型驱动程序的图像数据传输到 wia 服务创建的文件中。 启动数据传输的 WIA 应用程序向 WIA 服务指示它已准备好执行文件传输。

然后，WIA 服务将创建一个文件，并指示 WIA 微型驱动程序将数据传输到该文件中。 WIA 微型驱动程序通过请求要传输的数据与设备联系。 微型驱动程序需要自己的内存，因此较低级别的总线驱动程序堆栈可以将获取的数据放置到缓冲区中。 当 WIA 微型驱动程序接收到其缓冲区中的数据时，它将使用 [**wiasWriteBufToFile**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritebuftofile) WIA 服务库函数并传入其内存缓冲区。 WIA 服务库随后会将 WIA 微型驱动程序的内存缓冲区的内容写入 WIA 服务创建的文件中，如下图所示。

![阐释 wia 驱动程序文件数据传输的示意图](images/wia-imagedatafile.png)

将 **wiasWriteBufToFile** 服务库功能用于大多数文件传输。 仅对需要 WIA 服务写入多页 TIFF 文件的驱动程序使用 [**wiasWritePageBufToFile**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepagebuftofile) 服务库函数。 使用其自己的 TIFF 标头的驱动程序在编写多页 TIFF 文件时，应使用 **wiasWriteBufToFile**。

 

