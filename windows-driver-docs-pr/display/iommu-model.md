---
title: IoMmu 模型
description: IoMmu 模型中的每个进程具有单个虚拟地址空间的 CPU 和图形处理单元 (GPU) 之间共享，并由 OS 内存管理器管理。
ms.assetid: D8D5A2A8-F43A-4EC5-9355-C144EC15E754
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b49bd8fa1a2d4de28651cdda2eb9650a7c9a9001
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372923"
---
# <a name="iommu-model"></a>IoMmu 模型


在中*IoMmu*模型，每个进程具有单个虚拟地址空间的 CPU 和图形处理单元 (GPU) 之间共享，并由 OS 内存管理器管理。

若要访问内存，GPU 向发送的数据请求一个兼容*IoMmu*。 请求包含共享的虚拟地址和一个*进程地址空间标识符*(PASID)。 *IoMmu*单元执行使用共享的页表的地址转换。 这如下所示：

![iommu 进程地址空间转换](images/iommu-model.1.png)

内核模式驱动程序表明自己获得支持*IoMmu*模型通过设置[ **DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)::**IoMmuSupported**大写。 当设置此标志时，视频内存管理器将自动注册任何进程使用的 GPU *IoMmu* ，并获取*PASID*为该进程地址空间。 *PASID*设备创建期间传递给驱动程序。

主分配按映射的视频内存管理器 aperture 客户群正在之前显示，请确保显示控制器具有物理访问这些分配。

在中*IoMmu*模型，该驱动程序将继续为 GPU 使用视频内存管理器的分配的视频内存[*分配*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)服务。 这允许用户模式驱动程序遵循驻留模型，支持 Microsoft DirectX 资源共享模型，请确保主图面是可见内核，并在显示之前映射到 aperture。

转换的第一个级别 (*磁贴资源地址*到*共享 CPU/GPU 地址*) 由用户模式驱动程序完全管理在用户模式下。

 

 





