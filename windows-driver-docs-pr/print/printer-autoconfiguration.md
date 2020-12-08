---
title: 打印机自动配置
description: 打印机自动配置
keywords:
- 自动配置 WDK 打印机
- 打印机自动配置 WDK 打印机
- 自动配置 WDK 打印机，关于打印机自动配置
- 打印机自动配置 WDK 打印机，关于打印机自动配置
- 打印队列 WDK，自动配置
- 队列 WDK 打印机，自动配置
- 自动打印机配置 WDK
- 打印机配置 WDK，自动配置
- 队列 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 202d7c98cf4b3ab81cf667fbb5d48e0282616cda
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807389"
---
# <a name="printer-autoconfiguration"></a>打印机自动配置


在 Windows Vista 之前的 Windows 操作系统版本中，打印队列的设置最初设置为驱动程序的默认设置，而不是设置为适用于设备的设置。 对于 Unidrv 和 Pscript5 驱动程序，这意味着在 *GPD* 或 *PPD* 文件中指定的默认值始终用于初始打印队列设置。 这一静态的默认设置必须表示打印机可以附带的最小配置。 例如，如果装订设备对于设备是可选的，则默认情况下，此类设备不能具有启用装订功能。 如果在默认情况下启用了装订功能，则没有装订单元的设备的用户界面将显示装订作为选项;选择了装订选项但发现它不起作用的客户可能会混乱或不满意。

对于包含基本模型中不存在的功能的任何设备，用户或管理员必须在安装后在打印队列上手动配置这些功能。 有时，这可能是一个令人费解且不直观的过程。 配置过程容易出现错误，尤其是对于内存和硬盘大小等内部参数而言，这可能会显著影响打印速度和质量。

自动配置可以根据设备的可安装功能自动配置打印队列，而不是仅仅使用驱动程序的默认设置来解决此问题。

自动配置的主要目标是网络打印机，因为它们最可能具有多个可选功能并且需要更多配置。 如果未使用自动配置，则用户需要手动执行此配置。

[自动配置详细信息](autoconfiguration-details.md)

[自动配置实现选项](autoconfiguration-implementation-options.md)

 

 




