---
title: 使用子目标确定系统目标
description: 使用子目标确定系统目标
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5fdea7d1642d50c8ee798a345fa6a45b2603a024
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191003"
---
# <a name="target-a-system-using-chid-targeting"></a>使用子目标确定系统目标

 (子) 的计算机硬件 Id 由 OEM/ODM （运行 Windows 开发人员工具包 (WDK) 工具）创建， ( # A0) 或通过 [MICROSOFT oem 下载网站](https://www.microsoftoem.com) 的审核工具， (需要登录) 。

CHIDs 是计算机硬件 Id，Windows 利用这些 Id，以不同的目的实现目标。 将正确的驱动程序传送到系统后，正常的 PNP 排名会按 [Windows 排名驱动程序的方式](../install/how-setup-ranks-drivers--windows-vista-and-later-.md)进行介绍，并且供应商可以构建围绕此功能的策略，以便对其产品系列有意义。

OEM/ODM 需要确保根据 [smbios](smbios.md) 指南中提供的信息填充所有合适的 smbios 字段，并遵循 [DMTF smbios 规范](https://www.dmtf.org/standards/smbios) ，确保 CHIDs 是单独的且唯一的。

Microsoft 现在要求固件更新包包含计算机硬件 ID (子) 目标，以及 EFI 系统资源表 (ESRT) 中列出 **的唯一** ID。 [适用于 Windows 10 的下载驱动程序发布工作流](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)文档包含在分发目标和安装目标中使用的 CHIDs 的详细说明。

## <a name="related-resources"></a>相关资源

[合作伙伴中心](../dashboard/index.yml)

[指定计算机的硬件 ID](../install/specifying-hardware-ids-for-a-computer.md)

[下载适用于 Windows 10 的驱动程序发布工作流](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)