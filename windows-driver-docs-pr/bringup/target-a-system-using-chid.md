---
title: 目标系统使用 CHID 目标
description: 目标系统使用 CHID 目标
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 05f94ca402648d357df71dafcd799f463d67f7cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337382"
---
# <a name="target-a-system-using-chid-targeting"></a>目标系统使用 CHID 目标

计算机硬件 Id (CHID) s 创建的 Windows 开发人员 Kit(WDK) 工具 (ComputerHardwareIDs.exe) 或提供的审核工具运行到 Oem 通过 OEM/ODM [Microsoft OEM 下载站点](https://www.microsoftoem.com)（需登录）。

CHIDs 是计算机硬件 Id，Windows 将使用面向用途特异性排序的不同级别中这些 Id。 正确的驱动程序传递到系统，然后正常的即插即用排名高于中所述[如何 Windows Ranks Drivers](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)，和供应商可以生成一个解决此问题的策略，以适合其产品系列。

需要确保所有相应的 SMBIOS 字段填充了数据，将 OEM/考虑了 ODM 基于中提供的信息[SMBIOS](smbios.md)指导和以下[DMTF SMBIOS 规范](http://www.dmtf.org/standards/smbios)以确保 CHIDs为单个和唯一。

现在，Microsoft 会要求固件更新包，包括计算机硬件 ID (CHID) 目标设定为列出的唯一 ID 除了**系统**EFI 系统资源表 (ESRT) 中。 [下载驱动程序发布工作流适用于 Windows 10](http://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)文档包含 CHIDs 分发目标，以及安装目标中使用的详细的说明。

## <a name="related-resources"></a>相关资源

[合作伙伴中心](https://docs.microsoft.com/windows-hardware/drivers/dashboard)

[指定计算机的硬件 Id](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer)

[下载适用于 Windows 10 发布工作流的驱动程序](http://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)
