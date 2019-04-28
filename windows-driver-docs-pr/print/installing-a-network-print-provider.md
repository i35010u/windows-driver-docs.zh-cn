---
title: 安装网络打印提供程序
description: 安装网络打印提供程序
ms.assetid: 448101f8-cb26-4a6f-807d-f110978321da
keywords:
- 打印提供程序 WDK，安装
- 网络打印提供商 WDK，安装
- 安装 WDK 的打印提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daa9d20e07c70b47df6e9a1d6eac2940f4a0da0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339074"
---
# <a name="installing-a-network-print-provider"></a>安装网络打印提供程序





若要安装新的网络打印提供程序，必须提供将提供程序 DLL 复制到目标系统的安装程序\\System32 子目录，然后调用**AddPrintProvidor** （在 Microsoft Windows 中所述SDK 文档）。 此函数的提供程序创建注册表项，并将该提供程序添加到已安装的提供程序的后台处理程序的列表的末尾。 然后，该函数将加载提供程序 DLL，调用提供程序的[ **InitializePrintProvidor** ](https://msdn.microsoft.com/library/windows/hardware/ff551614)函数。

若要创建与网络打印提供程序支持的打印机的连接，用户调用添加打印机向导，选择"网络打印机服务器"选项。 用户指定打印队列使用\\ \\*服务器*\\*打印机*格式和提供程序的**OpenPrinter**函数必须能够识别的打印队列名称。

 

 




