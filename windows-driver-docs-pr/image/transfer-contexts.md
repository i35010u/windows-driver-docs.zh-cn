---
title: 传输上下文
description: 传输上下文
ms.assetid: b4eadccd-afb6-4cb5-bf52-704f64d45e40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e31c35433eb25a074578ee481beea1fa3241d828
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192913"
---
# <a name="transfer-contexts"></a>传输上下文





传输上下文是信息的集合，用于描述从微型驱动程序到应用程序的数据传输。 有关传输的信息存储在 [**MINIDRV \_ 传输 \_ 上下文**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context) 结构中。 传输上下文包括包含有关要传输的映像的信息的成员：其大小、分辨率、颜色深度 (每个像素的字节数) 、压缩类型和图像格式。 WIA 服务在调用 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法之前，从相关的 WIA 项属性获取这些值。 然后，这些值将存储在 MINIDRV \_ 传输 \_ 上下文结构中并向下传递到该驱动程序以方便访问。 此过程无需驱动程序使用 WIA 服务库例程来从应用程序项上下文读取这些值 (即 WIA 服务上下文) 。

传输上下文还包括有关传输类型的信息：是文件数据传输还是内存回调传输。 对于文件数据传输，其中一个成员包含将写入的文件的句柄。 建议微型驱动程序不触及此控点。 WIA 服务在传输发生前打开该句柄，并在传输完成后关闭该句柄。 对于内存回调数据传输 (和文件数据传输，其中应用程序要从微型驱动程序) 接收更新，成员包含微型驱动程序的回调例程的地址。

其他成员包含传输中使用的所有缓冲区的总大小等信息，以及微型驱动程序或 WIA 服务是否分配了这些信息。 有关此结构的成员的完整列表，请参阅 [**MINIDRV \_ 传输 \_ 上下文**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context) 。

微型驱动程序和 [**wiasGetImageInformation**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation) 函数一起设置许多用于描述图像本身的传输上下文项，例如，其宽度（以像素为单位）和行数。 WIA 服务设置许多与数据传输相关的传输上下文项，例如文件句柄 (适用) 时的传输类型。

 

