---
title: 上传时的驱动程序行为
description: 上传时的驱动程序行为
ms.assetid: a8edfd88-89b9-4759-b9b3-6f1ff2ae7fc9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2ec498bb21afe07fbafc8012fcc39e12172851b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364497"
---
# <a name="driver-behavior-on-upload"></a>上传时的驱动程序行为


驱动程序的行为取决于正在其调用上传的项的类型。

例如，如果**IWiaTransfer::Upload**正在调用上的"平台"项 (即项其[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性设置为 WIA\_类别\_平板)，将数据上传的确切含义是未定义的因为"平板"项不是数据存储项。 通常情况下，将使用供应商**IWiaTransfer::Upload**以使其扩展或应用程序以与设备通信以某种专有的方式。

但是，如果**IWiaTransfer::Upload**正在调用应用程序的调用最近创建的应用程序项**IWiaItem2::CreateChildItem**上, 传应当为一些新该设备，如文件保存到设备的存储所需的数据项。

**IWiaTransfer**并**IWiaItem2**接口 Microsoft Windows SDK 文档中所述。

 

 




