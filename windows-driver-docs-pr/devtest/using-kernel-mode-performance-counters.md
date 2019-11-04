---
title: 使用内核模式性能计数器
description: 使用内核模式性能计数器
ms.assetid: b740dd92-ad75-4dea-98d4-dce04b273d2f
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 78f65bae39d83b41c10cce0f2a2c7031b42f86b7
ms.sourcegitcommit: 7aa0dc2d0465f815438dcbb5335fd6a77a0fd630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2019
ms.locfileid: "73432668"
---
# <a name="using-kernel-mode-performance-counters"></a>使用内核模式性能计数器

内核模式 PCW 是对现有性能计数器版本2平台的扩展，使内核模式组件可以轻松地公开性能计数器。 若要合并此新扩展，需要对描述版本2计数器的清单进行最小程度的添加，并需要使用内核模式性能计数器接口。

使用以下步骤来开发新计数器：

1. 编写描述提供程序及其计数器集的[信息清单](https://docs.microsoft.com/windows/win32/wes/writing-an-instrumentation-manifest)。

    有关清单中的元素和属性的详细信息，请参阅[性能计数器架构](https://go.microsoft.com/fwlink/p/?linkid=147029)。 计数器清单是一种 XML 格式的文件，用于定义性能计数器提供程序及其计数器集。

    可以手动创建清单，也可以使用 WDK 中包含的清单生成器工具**Ecmangen**创建清单。 可以通过键入**ecmangen**在[开发人员命令提示](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs)中使用它。

2. 使用[CTRPP 工具](https://go.microsoft.com/fwlink/p/?linkid=144441)从清单生成注册代码和字符串资源。

    在 WDK 中包含计数器预处理器（CTRPP）工具，通过键入**CTRPP**可在[开发人员命令提示](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs)中找到该工具。

3. 添加用于注册和注销计数器集的代码。

    有关详细信息，请参阅[**PcwRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)和[**PcwUnregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwunregister)函数。

4. 添加用于公开实例的代码。

5. 生成包含新代码和字符串资源的二进制文件。

有关内核模式 PCW 提供程序的示例，请参阅 GitHub 上的[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[内核计数器示例（Kcs）](https://go.microsoft.com/fwlink/p/?LinkId=617718) 。
