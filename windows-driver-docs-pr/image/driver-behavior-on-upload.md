---
title: 上传时的驱动程序行为
description: 上传时的驱动程序行为
ms.assetid: a8edfd88-89b9-4759-b9b3-6f1ff2ae7fc9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31b268a8c7cfc2a005d741ad0f05ecaae7a0d674
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192505"
---
# <a name="driver-behavior-on-upload"></a>上传时的驱动程序行为


驱动程序的行为取决于要对其调用上传的项目的类型。

例如，如果在 "平板" 项上调用 **IWiaTransfer：：上传** (即，其 [**WIA \_ IPA \_ ITEM \_ CATEGORY**](./wia-ipa-item-category.md) 属性设置为 wia \_ 类别平板) 的项，则 \_ 上传数据的确切含义是不确定的，因为 "平板" 项不是一个数据存储项。 通常情况下，供应商将使用 **IWiaTransfer：：上传** 来使其扩展或应用程序能够以某种专有方式与设备进行通信。

但是，如果在由应用程序调用**IWiaItem2：： CreateChildItem**最近创建的应用程序项上调用**IWiaTransfer：：上传**，则上传应表示需要保存到设备存储的设备（例如文件）的一些新数据项。

Microsoft Windows SDK 文档中介绍了 **IWiaTransfer** 和 **IWiaItem2** 接口。

 

