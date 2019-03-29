---
title: SCSI 微型端口调试概述
description: SCSI 微型端口调试概述
ms.assetid: 9d05d416-aae4-453a-bdb0-2ac9148ad81d
keywords:
- SCSI 微型端口调试、 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a08cb3c42c7fa770ff807e587dad123365951f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576451"
---
# <a name="overview-of-scsi-miniport-debugging"></a>SCSI 微型端口调试概述


小型计算机系统接口 (SCSI) 调试扩展可在两个扩展模块：Scsikd.dll 和 Minipkd.dll。 这些模块中的最重要扩展命令的概述，请参阅[调试 SCSI 微型端口驱动程序的扩展](extensions-for-debugging-scsi-miniport-drivers.md)。 有关完整列表，请参阅[SCSI 微型端口扩展](scsi-miniport-extensions--scsikd-dll-and-minipkd-dll-.md)。

可以在任何版本的 Windows 中使用 SCSIkd.dll 扩展命令。 Minipkd.dll 扩展命令仅可在 Windows XP 和更高版本的 Windows。 Minipkd.dll 中的命令都只适用于使用 SCSI 端口驱动程序的微型端口驱动程序。

若要测试 SCSI 微型端口驱动程序，请使用 SCSI 验证功能的驱动程序验证程序。 有关驱动程序验证程序的信息，请参阅[Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480) Windows Driver Kit (WDK) 文档中。

 

 





