---
title: 打印机自动配置
description: 打印机自动配置
ms.assetid: bbe5e58b-4ca2-4ec2-867e-27765d4f59ab
keywords:
- 自动配置 WDK 打印机
- 打印机自动配置 WDK 打印机
- 自动配置 WDK 打印机，有关打印机自动配置
- 打印机自动配置 WDK 打印机，有关打印机自动配置
- 打印队列 WDK，自动配置
- 队列 WDK 打印机，自动配置
- 自动打印机配置 WDK
- 打印机配置 WDK，自动配置
- 队列 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a6e6ea45766ccc8409fe10394f66a4d42e7262c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547173"
---
# <a name="printer-autoconfiguration"></a>打印机自动配置


在 Windows Vista 之前的 Windows 操作系统版本中，打印队列的已设置了最初为驱动程序的默认设置，而不是适用于设备的设置。 对于 Unidrv 和 Pscript5 驱动程序，这意味着中指定默认值*GPD*或*PPD*文件始终用于初始的打印队列安装程序。 此静态组默认值必须表示打印机可随附的最低配置。 例如，如果装订单元是可选的设备，然后此类设备不能具有装订功能默认情况下启用。 如果装订功能已启用默认情况下，未装订单元的设备的用户界面将显示作为一个选项; 装订客户选择装订选项，但未找到工作可能会存在混淆或不高兴。

对于任何附带基本模型中不存在的功能的设备，用户或管理员必须手动配置这些功能上的打印队列安装完成后。 这有时，可以是一个令人困惑且非直观的过程。 配置过程是容易出错，尤其是对于内部参数，如内存和硬盘大小，这将严重影响打印速度和质量。

自动配置可以通过自动配置的设备，可安装的功能根据的打印队列，而不是只需使用驱动程序的默认设置来解决此问题。

自动配置的主要目标是网络打印机，因为它们是最有可能拥有多个可选功能，需要使用更多的配置。 如果未使用自动配置，用户将需要手动执行此配置。

[自动配置的详细信息](autoconfiguration-details.md)

[自动配置实现选项](autoconfiguration-implementation-options.md)

 

 




