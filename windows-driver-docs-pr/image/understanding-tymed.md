---
title: 了解 TYMED
description: 了解 TYMED
ms.assetid: 36110923-c346-4367-8b7d-ef4d003ed88c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 203c64fcc59a56f50264dac7f9ea9487cd65b9d6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184121"
---
# <a name="understanding-tymed"></a>了解 TYMED





TYMED 指定数据传输的类型。 此成员的值派生自 [**WIA \_ IPA \_ TYMED**](./wia-ipa-tymed.md) common item 属性。 指定的数据传输可以是内存回调传输或文件传输。 有关 TYMED XXX 常量的详细信息，请参阅 Microsoft Windows SDK 文档 \_ 。

### <a name="file-transfer-tymed"></a>文件传输 TYMED

在文件传输中，将使用以下值：

<a href="" id="tymed-file"></a>TYMED \_ 文件  
指示一个包含单个映像的文件。

<a href="" id="tymed-multipage-file"></a>TYMED \_ 多页 \_ 文件  
指示一个文件，其中包含多个图像，如多页 .TIF 和类似格式。 这主要用于文档送纸器采集。

### <a name="memory-transfer-tymed"></a>内存传输 TYMED

在内存传输中，将使用以下值：

<a href="" id="tymed-callback"></a>TYMED \_ 回调  
指示一个缓冲区，其中包含一个或多个由其 \_ 消息 \_ 新建页面消息分隔的映像 \_ 。

<a href="" id="tymed-multipage-callback"></a>TYMED \_ 多页 \_ 回调  
指示一个缓冲区，其中包含由其 \_ 消息 " \_ 新建页面消息" 分隔的多个图像 \_ 。 这会生成一个包含多个映像的文件。 这主要用于文档送纸器采集。

 

