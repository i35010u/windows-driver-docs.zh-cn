---
title: 使用内核模式性能计数器
description: 使用内核模式性能计数器
ms.assetid: b740dd92-ad75-4dea-98d4-dce04b273d2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7f302ce1ab595bedb5622be8cb4d7e9c7a438b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363784"
---
# <a name="using-kernel-mode-performance-counters"></a>使用内核模式性能计数器


内核模式 PCW 是现有的性能计数器版本 2 平台，它允许内核模式组件，可以很容易公开性能计数器的扩展。 若要将合并此新扩展，需要进行最小的新增内容介绍版本 2 计数器的清单并需要使用内核模式性能计数器接口。

使用以下步骤来开发新的计数器：

1.  编写程序清单中描述的提供程序和它的计数器设置。

    有关元素和在清单中的属性的详细信息，请参阅[性能计数器架构](https://go.microsoft.com/fwlink/p/?linkid=147029)。 计数器清单是 XML 格式文件，用于定义性能计数器提供程序和它的计数器设置。

    可以手动创建或使用的清单生成工具，Ecmangen.exe 创建的清单。 该工具包含在 WDK 中，目前在生成环境窗口 (类型**ecmangen**在命令提示符下)。

2.  使用[CTRPP 工具](https://go.microsoft.com/fwlink/p/?linkid=144441)从清单中生成的注册代码和字符串资源。

    计数器预处理器 (CTRPP) 工具包含在 WDK 中，目前在生成环境窗口 (类型**ctrpp**在命令提示符下)。

3.  添加代码以注册和注销的计数器集。

    有关详细信息，请参阅[ **PcwRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwregister)并[ **PcwUnregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwunregister)函数。

4.  添加代码以公开实例。

5.  生成包含新代码和字符串资源的二进制文件。

内核模式 PCW 提供程序的示例，请参阅[内核计数器样本 (Kcs)](https://go.microsoft.com/fwlink/p/?LinkId=617718)中[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

 

 





