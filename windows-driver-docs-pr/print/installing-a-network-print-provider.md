---
title: 安装网络打印提供程序
description: 安装网络打印提供程序
ms.assetid: 448101f8-cb26-4a6f-807d-f110978321da
keywords:
- 打印提供程序 WDK，安装
- 网络打印提供程序 WDK，安装
- 安装打印提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa1291646a5c139ef4b0f5e1a31fc234b44c0504
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832103"
---
# <a name="installing-a-network-print-provider"></a>安装网络打印提供程序





若要安装新的网络打印提供程序，您必须提供一个安装程序，该安装程序将提供程序 DLL 复制到目标系统的 \\System32 子目录中，然后调用**AddPrintProvidor** （如 Microsoft Windows SDK 文档中所述）。 此函数创建提供程序的注册表项，并将该提供程序添加到已安装的提供程序的后台处理程序列表的末尾。 然后，该函数加载提供程序 DLL 并调用提供程序的[**InitializePrintProvidor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor)函数。

若要创建与网络打印提供程序支持的打印机的连接，用户需要调用 "添加打印机向导" 并选择 "网络打印机服务器" 选项。 用户使用 \\\\*Server*\\*打印机*格式指定打印队列，提供程序的**OpenPrinter**函数必须识别该打印队列名称。

 

 




