---
title: AGP 的视频端口驱动程序支持
description: AGP 的视频端口驱动程序支持
ms.assetid: 445dbe4a-7f7b-4dcc-9891-17fd8fb03a6c
keywords:
- 微型端口驱动程序 WDK Windows 2000 AGP
- AGP WDK 微型端口
- 内存 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 103af71e2aeea5f75b3535384ea3d7496fc3d533
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556214"
---
# <a name="video-port-driver-support-for-agp"></a>AGP 的视频端口驱动程序支持


## <span id="ddk_video_port_driver_support_for_agp_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_AGP_GG"></span>


视频端口驱动程序实现了以下函数来支持加速图形端口 (AGP)。

[**AgpReservePhysical**](https://msdn.microsoft.com/library/windows/hardware/ff538223)

[**AgpCommitPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff538215)

[**AgpReserveVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff538224)

[**AgpCommitVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff538216)

[**AgpFreeVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff538219)

[**AgpReleaseVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff538221)

[**AgpFreePhysical**](https://msdn.microsoft.com/library/windows/hardware/ff538217)

[**AgpReleasePhysical**](https://msdn.microsoft.com/library/windows/hardware/ff538220)

[**AgpSetRate**](https://msdn.microsoft.com/library/windows/hardware/ff538226)

上面的列表中的微型端口驱动程序调用的函数之前，它必须通过调用获取函数指针[ **VideoPortQueryServices**](https://msdn.microsoft.com/library/windows/hardware/ff570337)。 有关获取 AGP 函数的指针的详细信息，请参阅[AGP 函数实现的视频端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff538227)。

微型端口驱动程序将执行以下步骤来保留和提交的显示适配器可以通过其访问系统内存的 AGP 小孔一部分：

1.  调用[ **AgpReservePhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff538223)保留一组连续的 AGP 小孔中的物理地址。

2.  调用[ **AgpCommitPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff538215)要映射的部分 （或所有） 返回的地址范围*AgpReservePhysical*到系统内存中的页面。 在系统内存中的页是锁定状态，但不是一定是连续的。 微型端口驱动程序可以调用*AgpCommitPhysical*多次，以执行多个小型承诺而不是一个大的一个。 但是，该驱动程序必须尝试提交的已提交的范围。

然后，应用程序能够查看并使用在系统内存中的已提交的页面，微型端口驱动程序执行以下步骤：

1.  调用[ **AgpReserveVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff538224)保留一系列应用程序的地址空间中的虚拟地址。 微型端口驱动程序必须通过*AgpReserveVirtual*以前返回的句柄*AgpReservePhysical*，以便保留的虚拟地址范围可以是与物理地址相关联通过创建范围*AgpReservePhysical*。

2.  调用[ **AgpCommitVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff538216)映射返回的虚拟地址范围的一部分*AgpReserveVirtual*到系统内存中的页面。 页的*AgpCommitVirtual*映射必须之前已映射通过调用*AgpCommitPhysical*。 此外，该映射由*AgpCommitPhysical*仍必须是当前; 也就是说，这些页面必须具有尚未释放通过调用[ **AgpFreePhysical**](https://msdn.microsoft.com/library/windows/hardware/ff538217)。

**请注意**  只要使用 AGP 函数提交或保留地址范围 （物理或虚拟），该范围的大小必须为 64 千字节的倍数。

 

微型端口驱动程序负责，以便释放所有内存，它已保留并提交通过调用以下函数：

-   [**AgpFreeVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff538219)取消映射通过调用之前已映射到系统内存的虚拟地址[ **AgpCommitVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff538216)。

-   [**AgpReleaseVirtual** ](https://msdn.microsoft.com/library/windows/hardware/ff538221)释放通过以前调用而保留的虚拟地址[ **AgpReserveVirtual**](https://msdn.microsoft.com/library/windows/hardware/ff538224)。

-   [**AgpFreePhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff538217)取消通过调用之前已映射到系统内存的物理地址映射[ **AgpCommitPhysical**](https://msdn.microsoft.com/library/windows/hardware/ff538215)。

-   [**AgpReleasePhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff538220)释放通过以前调用而保留的物理地址[ **AgpReservePhysical**](https://msdn.microsoft.com/library/windows/hardware/ff538223)。

 

 





