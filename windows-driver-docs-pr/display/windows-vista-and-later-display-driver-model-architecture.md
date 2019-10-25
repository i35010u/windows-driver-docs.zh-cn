---
title: Windows 显示驱动程序模型 (WDDM) 体系结构
description: Windows 显示驱动程序模型 (WDDM) 体系结构
ms.assetid: 1ae66fd3-8497-4098-9899-c2363671c2b0
keywords:
- 显示驱动程序模型 WDK Windows Vista，体系结构
- Windows Vista 显示器驱动程序模型 WDK、体系结构
- 体系结构 WDK 显示
- 用户模式显示驱动程序 WDK Windows Vista，体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0156b3cd3424298ffbb1b536484288736f23b27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825183"
---
# <a name="windows-display-driver-model-wddm-architecture"></a>Windows 显示驱动程序模型 (WDDM) 体系结构


## <span id="ddk_longhorn_display_driver_model_architecture_gg"></span><span id="DDK_LONGHORN_DISPLAY_DRIVER_MODEL_ARCHITECTURE_GG"></span>


Windows 显示驱动程序模型（WDDM）（从 Windows Vista 开始提供）的显示驱动程序模型体系结构由用户模式和内核模式部分组成。 下图显示支持 WDDM 所需的体系结构。

![阐释 wddm 体系结构的关系图](images/dx10arch.png)

图形硬件供应商必须提供用户模式显示驱动程序和显示微型端口驱动程序。 用户模式显示驱动程序是由 Microsoft Direct3D 运行时加载的动态链接库（DLL）。 显示*微型端口驱动程序*与 Microsoft DirectX 图形内核子系统通信。 有关用户模式显示驱动程序和显示微型端口驱动程序的详细信息，请参阅[Windows 显示驱动程序模型（WDDM）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_display/)。

 

 





