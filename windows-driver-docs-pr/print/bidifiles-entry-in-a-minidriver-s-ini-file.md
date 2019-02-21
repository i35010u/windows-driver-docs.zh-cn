---
title: BidiFiles 微型驱动程序的 INI 文件中的条目
description: BidiFiles 微型驱动程序的 INI 文件中的条目
ms.assetid: 953a29d2-f778-410e-bc8a-a09e294f2473
keywords:
- BidiFiles 部分
- INF 文件 WDK 打印，bidi 扩展文件信息
- bidi 扩展文件 WDK 打印机自动配置
- 框中自动配置支持 WDK 打印机，bidi 扩展名为的文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3eacbaaada4df272c7b6e079d2acb2afe3e4b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541848"
---
# <a name="bidifiles-entry-in-a-minidrivers-ini-file"></a>BidiFiles 微型驱动程序的 INI 文件中的条目


打印机微型驱动程序通信，通过特定于微型驱动程序的 INI 文件到端口监视器 bidi 扩展文件的信息。 端口监视器使用此信息在端口初始化过程中。

下面的示例演示`BidiFiles`INI 文件的部分。 `BidiSPMFile`会为标准 TCP/IP 端口监视器，使用项和`BidiWSDFile`条目将用于 Web Services for Devices (WSD) 端口监视器。

```INI
# OEM Mapping & Extension GDL files 
# 
[BidiFiles]
BidiSPMFile = BidiSPM_AcmeXXX.XML
BidiWSDFile  = BidiWSD_AcmeXXX.XML
```
