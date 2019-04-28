---
title: ProcAmp 控制 DDI
description: ProcAmp 控制 DDI
ms.assetid: 102e21eb-bad4-4ab5-8630-9ac37c33f20a
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e77350d3e2f9f0d61a4caf5311ee5233dce2c8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352183"
---
# <a name="procamp-control-ddi"></a>ProcAmp 控制 DDI


## <span id="ddk_procamp_control_ddi_gg"></span><span id="DDK_PROCAMP_CONTROL_DDI_GG"></span>


显示驱动程序，使视频混合使用呈现器 (VMR) 可以访问 ProcAmp 控件功能，必须实现[动作补偿回调函数](https://msdn.microsoft.com/library/windows/hardware/ff568441)。

若要简化驱动程序开发，使用运动补偿代码模板，并在本部分中实现的 ProcAmp 控制功能。 函数是取消隔行扫描容器设备或 ProcAmp 控制设备类的成员函数。 有关详细信息，请参阅[定义取消隔行扫描设备容器类](https://msdn.microsoft.com/library/windows/hardware/ff552682)并[定义 ProcAmp 控制设备类](https://msdn.microsoft.com/library/windows/hardware/ff552686)。

 

 





