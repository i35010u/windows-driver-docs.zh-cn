---
title: Windows 显示驱动程序模型 (WDDM) 体系结构
description: Windows 显示驱动程序模型 (WDDM) 体系结构
ms.assetid: 1ae66fd3-8497-4098-9899-c2363671c2b0
keywords:
- 显示驱动程序模型 WDK Windows Vista 中，体系结构
- Windows Vista 显示器驱动程序模型 WDK，体系结构
- WDK 显示的体系结构
- 用户模式显示驱动程序 WDK Windows Vista 中，体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f0d6774937d17cbf1939807252a6086cc392c19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391135"
---
# <a name="windows-display-driver-model-wddm-architecture"></a>Windows 显示驱动程序模型 (WDDM) 体系结构


## <span id="ddk_longhorn_display_driver_model_architecture_gg"></span><span id="DDK_LONGHORN_DISPLAY_DRIVER_MODEL_ARCHITECTURE_GG"></span>


显示驱动程序模型体系结构的 Windows 显示驱动程序模型 (WDDM)，从 Windows Vista 开始提供由用户模式和内核模式部分组成。 下图显示了支持 WDDM 所需的体系结构。

![说明 wddm 体系结构的关系图](images/dx10arch.png)

图形硬件供应商必须提供用户模式显示驱动程序和显示微型端口驱动程序。 用户模式显示驱动程序是 Microsoft Direct3D 运行时加载的动态链接库 (DLL)。 显示*微型端口驱动程序*与 Microsoft DirectX 图形内核子系统进行通信。 有关用户模式显示驱动程序和显示微型端口驱动程序的详细信息，请参阅[Windows 显示驱动程序模型 (WDDM) 引用](https://msdn.microsoft.com/library/windows/hardware/ff570595)。

 

 





