---
title: WdfTester 安装
description: WdfTester 安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54cbd5a3262ecf6759a5665bc783855573c63e15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823305"
---
# <a name="wdftester-installation"></a>WdfTester 安装


必须先将 WdfTester 文件复制到工作目录，并运行安装脚本，然后才能在驱动程序上运行 WdfTester 工具。

**安装 WdfTester**

1.  将以下文件列表从 WDK (*% WDKRoot%* \\ tools \\ *&lt; &gt; 平台*) 复制到包含驱动程序二进制文件副本的本地文件夹。
    Wdftester.sys Wdftester Wdftester Wdftester. tmf WdftesterScript. .wsf
2.  打开 "命令提示符" 窗口 (确保在 Windows Vista 上以 **管理员身份运行**) ，然后键入以下命令： cscript WdfTesterScript. .wsf install

    此命令安装 Wdftester.sys 驱动程序并启动服务。

3.  按 Enter。

 

 





