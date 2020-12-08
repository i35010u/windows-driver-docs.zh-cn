---
title: SCSI 微型端口调试概述
description: SCSI 微型端口调试概述
keywords:
- SCSI 微型端口调试，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e91ef437ed39611064916eb4e18fee460cf9ad8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828859"
---
# <a name="overview-of-scsi-miniport-debugging"></a>SCSI 微型端口调试概述

## <a name="span-idoverview_of_scsispanspan-idoverview_of_scsispan-scsi-verification"></a><span id="overview_of_scsi"></span><span id="OVERVIEW_OF_SCSI"></span> SCSI 验证

小型计算机系统接口 (SCSI) 调试扩展可以在两个扩展模块中找到： Scsikd.dll 和 Minipkd.dll。 有关这些模块中最重要的扩展命令的概述，请参阅 [用于调试 SCSI 微型端口驱动程序的扩展](extensions-for-debugging-scsi-miniport-drivers.md)。 有关完整列表，请参阅 [SCSI 微型端口扩展](scsi-miniport-extensions--scsikd-dll-and-minipkd-dll-.md)。

SCSIkd.dll 扩展命令可在任何版本的 Windows 中使用。 Minipkd.dll 扩展命令只能在 Windows XP 和更高版本的 Windows 中使用。 Minipkd.dll 中的命令仅适用于使用 SCSI 端口驱动程序的微型端口驱动程序。

若要测试 SCSI 微型端口驱动程序，请使用驱动程序验证程序的 SCSI 验证功能。 有关驱动程序验证程序的信息，请参阅 Windows 驱动程序工具包中的 [驱动程序验证](../devtest/driver-verifier.md) 器 (WDK) 文档。
