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
ms.openlocfilehash: 2dffd766a2ab27bd678d675dee9a5e949ce5a91e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385976"
---
# <a name="installing-a-network-print-provider"></a>安装网络打印提供程序





若要安装新的网络打印提供程序，必须提供将提供程序 DLL 复制到目标系统的安装程序\\System32 子目录，然后调用**AddPrintProvidor** （在 Microsoft Windows 中所述SDK 文档）。 此函数的提供程序创建注册表项，并将该提供程序添加到已安装的提供程序的后台处理程序的列表的末尾。 然后，该函数将加载提供程序 DLL，调用提供程序的[ **InitializePrintProvidor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintprovidor)函数。

若要创建与网络打印提供程序支持的打印机的连接，用户调用添加打印机向导，选择"网络打印机服务器"选项。 用户指定打印队列使用\\ \\*服务器*\\*打印机*格式和提供程序的**OpenPrinter**函数必须能够识别的打印队列名称。

 

 




