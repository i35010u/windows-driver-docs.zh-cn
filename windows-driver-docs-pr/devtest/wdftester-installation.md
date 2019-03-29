---
title: WdfTester 安装
description: WdfTester 安装
ms.assetid: 39645ca4-3f4e-4a1f-bf62-7b44856ce58e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec2a443b5c2bc39cbd11d26157e92bad8f4008c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567214"
---
# <a name="wdftester-installation"></a>WdfTester 安装


可以在您的驱动程序运行 WdfTester 工具之前，必须首先将 WdfTester 文件复制到工作目录，并运行安装脚本。

**若要安装 WdfTester**

1.  WDK 中复制以下文件列表 (*%wdkroot%*\\工具\\*&lt;平台&gt;*) 到本地文件夹，其中包含您的驱动程序的副本二进制文件。
    Wdftester.sys Wdftester.inf Wdftester.ctl Wdftester.tmf WdftesterScript.wsf
2.  打开命令提示符窗口 (务必**以管理员身份运行**Windows Vista 上)，然后键入以下命令： cscript WdfTesterScript.wsf 安装

    此命令将 Wdftester.sys 驱动程序安装并启动服务。

3.  按 Enter。

 

 





