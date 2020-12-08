---
title: IoMmu 模型
description: 在 IoMmu 模型中，每个进程都有一个虚拟地址空间，该空间在 CPU 和图形处理单元 (GPU) 之间共享，并且由 OS 内存管理器进行管理。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b646eeba76817bf0a4be50017a00175272759ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832731"
---
# <a name="iommu-model"></a>IoMmu 模型


在 *IoMmu* 模型中，每个进程都有一个虚拟地址空间，该空间在 CPU 和图形处理单元 (GPU) 之间共享，并且由 OS 内存管理器进行管理。

为访问内存，GPU 将向兼容的 *IoMmu* 发送数据请求。 请求包括共享虚拟地址和 *进程地址空间标识符* (PASID) 。 *IoMmu* 单位使用共享页面表执行地址转换。 具体语句如下所示：

![iommu 进程地址空间转换](images/iommu-model.1.png)

内核模式驱动程序通过设置 [**DXGK \_ VIDMMCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidmmcaps)：：**IoMmuSupported** cap 来表示对 *IoMmu* 模型的支持。 设置此标志后，视频内存管理器将使用 GPU 自动向 *IoMmu* 注册任何进程，并获取该进程地址空间的 *PASID* 。 在设备创建期间， *PASID* 将传递给驱动程序。

主分配在显示前由 "视频内存管理器" 映射到 "光圈" 段，以确保显示控制器具有对这些分配的物理访问权限。

在 *IoMmu* 模型中，驱动程序将继续使用视频内存管理器的 [*分配*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb) 服务为 GPU 分配视频内存。 这允许用户模式驱动程序遵循派驻模型，支持 Microsoft DirectX 资源共享模型，确保主表面对内核可见，并在显示之前映射到孔径。

第一级转换 (将 *资源地址平铺* 到 *共享 CPU/GPU 地址*) 由用户模式驱动程序在用户模式下完全管理。

 

