---
title: 示例端口监视器
description: 示例端口监视器
ms.assetid: dac754bf-f39d-439c-974b-889436211ef3
keywords:
- 端口监视 WDK 打印示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f739b15987fd73acfbf2e937cb7d232911f1ccf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366717"
---
# <a name="sample-port-monitor"></a>示例端口监视器





Windows Driver Kit (WDK) 中包含的源代码 LOCALMON (Localmon.dll) 支持本地 LPT 和 COM 端口，端口监视器。

从 Windows 2000 开始，所有 LOCALMON 将导出的函数已融入 Localspl.dll，本地打印提供程序。 在 Windows 2000 和更高版本的操作系统版本的另一个更改是监视器分为两个 Dll 该端口： 端口监视服务器 DLL，以及端口监视器用户界面 DLL。 这些 Dll 的源代码位于\\Src\\打印\\监视器\\Localmon 并\\Src\\打印\\监视器\\Localui 子目录。

 

 




