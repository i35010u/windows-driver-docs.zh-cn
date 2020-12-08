---
title: 命令处理
description: 命令处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31f7fa925f74ab9294d90bf16bf5973aaeab4f48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823185"
---
# <a name="command-handling"></a>命令处理





WIA 体系结构使 WIA 应用程序能够向 WIA 微型驱动程序发送特定命令。 此命令只能发送到 WIA 项树中的根项。  (请注意，微型驱动程序将报告它在其功能表中支持的所有命令。 ) 

WIA 应用程序发出的命令不会直接发送到 WIA 微型驱动程序。 相反，应用程序会将命令发送到 WIA 服务。 WIA 服务随后会将此命令转发到 WIA 微型驱动程序。 当微型驱动程序接收到命令 (作为 [**IWiaMiniDrv：:D rvdevicecommand**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdevicecommand)) 方法的参数时，微型驱动程序可能需要访问设备以满足命令。

在某些情况下，该命令可能要求微型驱动程序创建新的子驱动程序项。 例如，数字照相机设备可能支持 **TakePicture** 命令。 如果微型驱动程序收到此命令，它会指示相机拍摄一张照片。 当照相机执行拍摄照片的请求时，照相机会在其媒体上创建新图像，WIA 微型驱动程序会将新的驱动程序项添加到其项树中。

 

