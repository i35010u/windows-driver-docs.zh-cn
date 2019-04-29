---
title: 传输上下文
description: 传输上下文
ms.assetid: b4eadccd-afb6-4cb5-bf52-704f64d45e40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 207ce1219c51160fa48b0e22a51dae5f39bdd1ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366993"
---
# <a name="transfer-contexts"></a>传输上下文





传输上下文是信息的一系列介绍了从微型驱动程序的应用程序的数据传输。 有关传输的信息存储在[ **MINIDRV\_传输\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff545250)结构。 传输上下文包括包含有关传输的映像的信息的成员： 其大小、 分辨率、 颜色深度 （每个像素的字节数）、 压缩和图像格式的类型。 WIA 服务从相关 WIA 项属性获取这些值，调用之前[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)方法。 值然后存储在 MINIDRV\_传输\_上下文结构并提交到方便访问的驱动程序。 此过程不需要的驱动程序以使用 WIA 的服务库例程来从应用程序项目上下文 （即，WIA 服务上下文） 中读取这些值。

传输上下文还包括有关的传输类型信息： 它是文件数据传输还是内存回调传输。 对于文件数据传输，一个成员包含要写入文件的句柄。 建议微型驱动程序不接触此句柄。 WIA 服务传输出现和传输完成后关闭之前打开句柄。 对于内存回调数据传输 （以及应用程序将从微型驱动程序接收更新的文件数据传输），成员将包含的微型驱动程序的回调例程的地址。

其他成员包含信息，例如所有在传输中使用的缓冲区的总大小以及是否微型驱动程序或 WIA 服务分配它们。 请参阅[ **MINIDRV\_传输\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff545250)有关此结构的成员的完整列表。

微型驱动程序，一起[ **wiasGetImageInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549249)函数中，将许多传输设置上下文项，用于描述中的图像本身，例如其宽度像素，并且行数。 WIA 服务集都很关心数据传输，如文件传输上下文项的许多处理 （如果适用）、 传输的类型。

 

 




