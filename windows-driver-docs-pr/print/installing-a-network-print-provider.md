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
ms.openlocfilehash: 20aab15387010c756d3e97b97b03ccbfb8191512
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213669"
---
# <a name="installing-a-network-print-provider"></a>安装网络打印提供程序





若要安装新的网络打印提供程序，必须提供一个将提供程序 DLL 复制到目标系统的 System32 子目录中的安装程序， \\ 然后调用 Microsoft Windows SDK 文档) 中所述的 **AddPrintProvidor** (。 此函数创建提供程序的注册表项，并将该提供程序添加到已安装的提供程序的后台处理程序列表的末尾。 然后，该函数加载提供程序 DLL 并调用提供程序的 [**InitializePrintProvidor**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintprovidor) 函数。

若要创建与网络打印提供程序支持的打印机的连接，用户需要调用 "添加打印机向导" 并选择 "网络打印机服务器" 选项。 用户使用 \\ \\ *服务器* \\ *打印机*格式指定打印队列，提供程序的**OpenPrinter**函数必须识别该打印队列名称。

 

