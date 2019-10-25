---
title: IoMmu 模型
description: 在 IoMmu 模型中，每个进程都有一个虚拟地址空间，该空间在 CPU 和图形处理单元（GPU）之间共享，由 OS 内存管理器进行管理。
ms.assetid: D8D5A2A8-F43A-4EC5-9355-C144EC15E754
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb63e371ec1554dab3aca75bb19d696e125c717b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840340"
---
# <a name="iommu-model"></a>IoMmu 模型


在*IoMmu*模型中，每个进程都有一个虚拟地址空间，该空间在 CPU 和图形处理单元（GPU）之间共享，由 OS 内存管理器进行管理。

为访问内存，GPU 将向兼容的*IoMmu*发送数据请求。 请求包括共享虚拟地址和*进程地址空间标识符*（PASID）。 *IoMmu*单位使用共享页面表执行地址转换。 如下所示：

![iommu 进程地址空间转换](images/iommu-model.1.png)

内核模式驱动程序通过设置[**DXGK\_VIDMMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)：：**IoMmuSupported** Cap 来表示对*IoMmu*模型的支持。 设置此标志后，视频内存管理器将使用 GPU 自动向*IoMmu*注册任何进程，并获取该进程地址空间的*PASID* 。 在设备创建期间， *PASID*将传递给驱动程序。

主分配在显示前由 "视频内存管理器" 映射到 "光圈" 段，以确保显示控制器具有对这些分配的物理访问权限。

在*IoMmu*模型中，驱动程序将继续使用视频内存管理器的[*分配*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)服务为 GPU 分配视频内存。 这允许用户模式驱动程序遵循派驻模型，支持 Microsoft DirectX 资源共享模型，确保主表面对内核可见，并在显示之前映射到孔径。

用户模式驱动程序以用户模式完全管理第一层翻译（将*资源地址平铺*为*共享 CPU/GPU 地址*）。

 

 





