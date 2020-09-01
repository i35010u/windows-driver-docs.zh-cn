---
title: 内存中传输
description: 内存中传输
ms.assetid: 90238354-e47c-41c7-bb6b-6337f39f63f0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3edf92feb3ae9aaee2b06b6793d66e54216e6eb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190093"
---
# <a name="in-memory-transfers"></a>内存中传输





**注意**   内存中传输适用于 Windows Vista 之前的操作系统。

 

*内存中数据传输*是指将数据从 wia 微型驱动程序传输到 wia 服务分配的内存缓冲区。 启动数据传输的 WIA 应用程序始终决定数据传输缓冲区的大小。 此数据传输缓冲区的大小不能小于微型驱动程序在 " [**WIA \_ IPA \_ buffer \_ size**](./wia-ipa-buffer-size.md) " 属性中定义的值。

WIA 应用程序确定缓冲区大小后，会请求 WIA 服务开始数据传输。 然后，WIA 服务根据前面所述段落) 的约束分配所请求 (大小的内存缓冲区，并请求 WIA 微型驱动程序开始数据传输并将数据放置到提供的缓冲区中。 WIA 微型驱动程序用数据填充缓冲区，并将其返回给 WIA 服务，后者随后将数据返回到请求的 WIA 应用程序。 此过程将重复进行，直到没有更多的数据要传输。

下图演示了图像的内存传输。

![说明映像内存传输的示意图](images/wia-imagedatamem.png)

 

