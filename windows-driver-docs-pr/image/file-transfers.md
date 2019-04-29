---
title: 文件传输
description: 文件传输
ms.assetid: 1c776dc5-982a-4652-bc03-f334fda30055
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bce86a0d42156ad8e0ba0f770388b899a17fa660
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323190"
---
# <a name="file-transfers"></a>文件传输





**请注意**  文件传输适用于 Windows Vista 之前的操作系统。

 

一个*文件数据传输*是图像数据从 WIA 微型驱动程序到 WIA 服务创建的文件的传输。 启动数据传输的 WIA 应用程序向 WIA 服务指示它已准备好执行的文件传输。

WIA 服务然后会创建一个文件，并指示 WIA 微型驱动程序将数据传输到该文件。 WIA 微型驱动程序与设备联系通过请求进行传输的数据。 微型驱动程序需要自己的内存，因此无法获得的数据放入缓冲区较低级别总线驱动程序堆栈。 在 WIA 微型驱动程序在其缓冲区中接收数据，它使用[ **wiasWriteBufToFile** ](https://msdn.microsoft.com/library/windows/hardware/ff549473) WIA 服务库函数，其内存缓冲区中传递。 然后，WIA 服务库将 WIA 微型驱动程序的内存缓冲区的内容写入到 WIA 服务创建，如下图所示的文件。

![说明 wia 驱动程序文件数据传输的关系图](images/wia-imagedatafile.png)

使用**wiasWriteBufToFile**大多数文件传输的服务库函数。 使用[ **wiasWritePageBufToFile** ](https://msdn.microsoft.com/library/windows/hardware/ff549484)服务库函数，仅对驱动程序需要 WIA 的服务来编写多页的 TIFF 文件。 他们编写多页的 TIFF 文件时使用他们自己 TIFF 标头的驱动程序应使用**wiasWriteBufToFile**。

 

 




