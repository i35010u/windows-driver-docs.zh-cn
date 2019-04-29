---
title: WIA 核心组件
description: WIA 核心组件
ms.assetid: 59c02fa2-9116-4b57-a8fa-b977a4d6c714
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: d4a708ad41ee58cd3143400e25df507a1f2789bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370045"
---
# <a name="wia-core-components"></a>WIA 核心组件

WIA 组件在下图中显示。

![说明 wia 核心组件的关系图](images/stiwhist.png)

WIA 服务 (*wiaservc.dll*) 由名为的泛型主机承载*svchost.exe*。 *Wiaservc.dll*与一个或多个用户模式下仍映像 （和驱动程序标记为 USD1、 USD2，USD3 图中的），其中每个与特定类型的内核模式驱动程序进行通信。 Windows 提供了三种类型的总线抽象：USB、 SCSI，并序列 ( *usbscan.sys*， *scsiscan.sys*，并*serscan.sys*)。

在客户端应用程序可以是任一 TWAIN 兼容应用程序 (请参阅[TWAIN 兼容应用程序的支持](support-for-twain-compatible-applications.md)) 或 WIA 应用程序。 TWAIN 应用程序将数据源管理器，进而调用到调*wiadss.dll*，转换组件的实例与之通信*sti.dll*。 *Sti.dll*是与 WIA 服务进行通信的存根。 与此相反，WIA 应用程序直接进行调用时*sti.dll*。
