---
title: 反交错 DDI
description: 反交错 DDI
ms.assetid: 06b85f76-950a-4a9b-af6b-ded823bfda6a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07a2aa7869adf9fdb6c3c9cd7aaa92eadfddaef6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348897"
---
# <a name="deinterlace-ddi"></a>反交错 DDI


## <span id="ddk_deinterlace_ddi_gg"></span><span id="DDK_DEINTERLACE_DDI_GG"></span>


显示驱动程序，以便视频混合使用呈现器 (VMR) 可以取消隔行扫描，并对视频内容执行帧速率转换，必须实现[动作补偿回调函数](https://msdn.microsoft.com/library/windows/hardware/ff568441)。

若要简化驱动程序开发，使用运动补偿代码模板，并在本部分中实现取消隔行扫描的函数。 函数是取消隔行扫描容器设备或取消隔行扫描模式设备类的成员函数。 有关详细信息，请参阅[定义取消隔行扫描设备容器类](https://msdn.microsoft.com/library/windows/hardware/ff552682)并[定义取消隔行扫描 Bob 设备类](https://msdn.microsoft.com/library/windows/hardware/ff552679)。

 

 





