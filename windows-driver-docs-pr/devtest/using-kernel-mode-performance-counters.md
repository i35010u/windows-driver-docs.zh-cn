---
title: 使用内核模式性能计数器
description: 使用内核模式性能计数器
ms.assetid: b740dd92-ad75-4dea-98d4-dce04b273d2f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae840dc8c6d5703f4a2a5fe0d36c493499e95a3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839994"
---
# <a name="using-kernel-mode-performance-counters"></a>使用内核模式性能计数器


内核模式 PCW 是对现有性能计数器版本2平台的扩展，使内核模式组件可以轻松地公开性能计数器。 若要合并此新扩展，需要对描述版本2计数器的清单进行最小程度的添加，并需要使用内核模式性能计数器接口。

使用以下步骤来开发新计数器：

1.  编写描述提供程序及其计数器集的清单。

    有关清单中的元素和属性的详细信息，请参阅[性能计数器架构](https://go.microsoft.com/fwlink/p/?linkid=147029)。 计数器清单是一种 XML 格式的文件，用于定义性能计数器提供程序及其计数器集。

    可以手动创建或使用清单生成器工具 Ecmangen 创建清单。 该工具包含在 WDK 中，在生成环境窗口中提供（在命令提示符下键入**ecmangen** ）。

2.  使用[CTRPP 工具](https://go.microsoft.com/fwlink/p/?linkid=144441)从清单生成注册代码和字符串资源。

    "计数器预处理器（CTRPP）" 工具包含在 WDK 中，在 "生成环境" 窗口（在命令提示符下键入**CTRPP** ）中提供。

3.  添加用于注册和注销计数器集的代码。

    有关详细信息，请参阅[**PcwRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)和[**PcwUnregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwunregister)函数。

4.  添加用于公开实例的代码。

5.  生成包含新代码和字符串资源的二进制文件。

有关内核模式 PCW 提供程序的示例，请参阅 GitHub 上的[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[内核计数器示例（Kcs）](https://go.microsoft.com/fwlink/p/?LinkId=617718) 。

 

 





