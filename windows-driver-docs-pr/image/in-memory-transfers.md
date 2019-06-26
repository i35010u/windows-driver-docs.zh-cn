---
title: 内存中传输
description: 内存中传输
ms.assetid: 90238354-e47c-41c7-bb6b-6337f39f63f0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92daf150e4ad8698181938978c09d2917d3f2337
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373527"
---
# <a name="in-memory-transfers"></a>内存中传输





**请注意**  内存中传输适用于 Windows Vista 之前的操作系统。

 

*内存中数据传输*是图像 WIA 微型驱动程序中的数据处理到 WIA 服务已分配的内存缓冲区的传输。 始终启动数据传输的 WIA 应用程序确定的数据传输缓冲区的大小。 此数据传输缓冲区的大小不能为微型驱动程序定义中的值小于[ **WIA\_IPA\_缓冲区\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-buffer-size)属性。

WIA 应用程序确定缓冲区大小后，它将请求 WIA 服务以开始数据传输。 WIA 服务然后会分配的内存缓冲区的请求的大小 （根据前面段落所述的约束） 和请求 WIA 微型驱动程序开始数据传输，并将数据放到所提供的缓冲区。 WIA 微型驱动程序的数据填充缓冲区，并将其返回到 WIA 服务，然后将数据返回到发出请求的 WIA 应用程序。 重复此过程，直到没有更多的数据传输。

下图说明了映像的内存传输。

![说明图像内存传输的关系图](images/wia-imagedatamem.png)

 

 




