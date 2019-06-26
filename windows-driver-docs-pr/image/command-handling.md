---
title: 命令处理
description: 命令处理
ms.assetid: 1b940585-8228-4857-92bf-c77c789f6ad5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a7df5390b327c1cc6451f4e728bda98237d16eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358644"
---
# <a name="command-handling"></a>命令处理





WIA 体系结构可以将特定的命令发送到 WIA 微型驱动程序将 WIA 应用程序。 此命令可以只发送到 WIA 项树中的根项。 （请注意微型驱动程序报告的所有命令它支持其功能表中。）

WIA 应用程序发出的命令不会直接学习 WIA 微型驱动程序。 相反，应用程序将命令发送到 WIA 服务。 然后，WIA 服务将此命令转发到 WIA 微型驱动程序。 微型驱动程序时收到命令 (作为参数的[ **IWiaMiniDrv::drvDeviceCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)方法)，微型驱动程序可能需要访问设备，以满足该命令。

在某些情况下，该命令可能需要微型驱动程序创建的新驱动程序子项。 例如，数码相机设备可能支持**TakePicture**命令。 如果微型驱动程序收到此命令时，它指示摄像机拍摄一张照片。 当照相机拍摄照片的请求执行一些时，照相机在其媒体上，创建一个新映像和 WIA 微型驱动程序将新的驱动程序项添加到其项树。

 

 




