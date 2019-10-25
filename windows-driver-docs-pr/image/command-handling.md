---
title: 命令处理
description: 命令处理
ms.assetid: 1b940585-8228-4857-92bf-c77c789f6ad5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d32b3cef55e0cbb53d715e2f0b8291987f1df60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840871"
---
# <a name="command-handling"></a>命令处理





WIA 体系结构使 WIA 应用程序能够向 WIA 微型驱动程序发送特定命令。 此命令只能发送到 WIA 项树中的根项。 （请注意，微型驱动程序将报告它在其功能表中支持的所有命令。）

WIA 应用程序发出的命令不会直接发送到 WIA 微型驱动程序。 相反，应用程序会将命令发送到 WIA 服务。 WIA 服务随后会将此命令转发到 WIA 微型驱动程序。 当微型驱动程序收到命令时（作为[**IWiaMiniDrv：:D rvdevicecommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)方法的参数），微型驱动程序可能需要访问设备以满足命令。

在某些情况下，该命令可能要求微型驱动程序创建新的子驱动程序项。 例如，数字照相机设备可能支持**TakePicture**命令。 如果微型驱动程序收到此命令，它会指示相机拍摄一张照片。 当照相机执行拍摄照片的请求时，照相机会在其媒体上创建新图像，WIA 微型驱动程序会将新的驱动程序项添加到其项树中。

 

 




