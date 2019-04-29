---
title: 微型驱动程序 INI 文件中的 BidiFiles 项
description: 微型驱动程序 INI 文件中的 BidiFiles 项
ms.assetid: 953a29d2-f778-410e-bc8a-a09e294f2473
keywords:
- BidiFiles 部分
- INF 文件 WDK 打印，bidi 扩展文件信息
- bidi 扩展文件 WDK 打印机自动配置
- 框中自动配置支持 WDK 打印机，bidi 扩展名为的文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3eacbaaada4df272c7b6e079d2acb2afe3e4b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376584"
---
# <a name="bidifiles-entry-in-a-minidrivers-ini-file"></a>微型驱动程序 INI 文件中的 BidiFiles 项


打印机微型驱动程序通信，通过特定于微型驱动程序的 INI 文件到端口监视器 bidi 扩展文件的信息。 端口监视器使用此信息在端口初始化过程中。

下面的示例演示`BidiFiles`INI 文件的部分。 `BidiSPMFile`会为标准 TCP/IP 端口监视器，使用项和`BidiWSDFile`条目将用于 Web Services for Devices (WSD) 端口监视器。

```INI
# OEM Mapping & Extension GDL files 
# 
[BidiFiles]
BidiSPMFile = BidiSPM_AcmeXXX.XML
BidiWSDFile  = BidiWSD_AcmeXXX.XML
```
