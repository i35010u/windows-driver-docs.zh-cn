---
title: 装载卷
description: 装载卷
ms.assetid: 0531b023-f35c-4fe9-9c0d-5acafc42f9b4
keywords:
- 筛选器驱动程序 WDK 文件系统、 卷装入过程
- 文件系统筛选器驱动程序 WDK，卷装载进程
- 卷 WDK 文件系统装载
- 装载卷 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68b5ea6428b95c2d4302f381ac3b281d3be3ad10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545477"
---
# <a name="mounting-a-volume"></a>装载卷


## <span id="ddk_mounting_a_volume_if"></span><span id="DDK_MOUNTING_A_VOLUME_IF"></span>


卷的安装过程通常会触发一个请求将打开一个逻辑卷 （即，分区或动态卷） 上的文件，如下所示：

1.  用户应用程序调用**CreateFile**打开文件。 或内核模式驱动程序调用[ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)或[ **IoCreateFileSpecifyDeviceObjectHint**](https://msdn.microsoft.com/library/windows/hardware/ff548289)。

2.  I/O 管理器确定哪些逻辑卷是请求的目标，并检查以查看它是否将安装其设备对象。 如果 VPB\_设置安装标志，则由文件系统已装入卷。

3.  如果不已装入卷文件系统自系统启动以来 (即，VPB\_未设置安装标志)，I/O 管理器发送卷装载 ([**IRP\_MJ\_文件\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff548670)，IRP\_MN\_装载\_卷) 可能会声明该卷的每个文件系统的请求。

    不是所有内置的文件系统甚至还在系统启动之后一定加载 −。 (请参阅[发生在系统启动期间文件系统](what-happens-to-file-systems-during-system-boot.md)。)对于尚未加载内置文件系统，I/O 管理器将卷装入请求发送到文件系统识别 (FsRec)，它检查代表这些文件系统卷引导扇区。

    如果 FsRec 确定该卷由尚未加载的文件系统格式化，I/O 管理器发送以此进行响应负载文件系统 ([**IRP\_MJ\_文件\_系统\_控件** ](https://msdn.microsoft.com/library/windows/hardware/ff548670)，IRP\_MN\_负载\_文件\_系统) 到 FsRec，加载文件系统的请求。 然后，I/O 管理器将原始卷装入请求发送到文件系统。

4.  接收装入卷请求每个文件系统将检查以确定该卷的格式和其他信息是否指示卷由该特定的文件系统格式化的卷的引导扇区。 如果格式与匹配，文件系统装载卷。

以下各节讨论文件系统将卷装载后意识到它的方式：

[如何装载卷](how-the-volume-is-mounted.md)

[卷装入示例](volume-mount-example.md)

 

 




