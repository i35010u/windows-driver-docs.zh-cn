---
title: 反交错 DDI
description: 反交错 DDI
ms.assetid: 06b85f76-950a-4a9b-af6b-ded823bfda6a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a79b7ba17b81f4556234ab8a6e6788709af06ad5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384897"
---
# <a name="deinterlace-ddi"></a>反交错 DDI


## <span id="ddk_deinterlace_ddi_gg"></span><span id="DDK_DEINTERLACE_DDI_GG"></span>


显示驱动程序，以便视频混合使用呈现器 (VMR) 可以取消隔行扫描，并对视频内容执行帧速率转换，必须实现[动作补偿回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

若要简化驱动程序开发，使用运动补偿代码模板，并在本部分中实现取消隔行扫描的函数。 函数是取消隔行扫描容器设备或取消隔行扫描模式设备类的成员函数。 有关详细信息，请参阅[定义取消隔行扫描设备容器类](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-deinterlace-container-device-class)并[定义取消隔行扫描 Bob 设备类](https://docs.microsoft.com/windows-hardware/drivers/display/defining-the-deinterlace-bob-device-class)。

 

 





