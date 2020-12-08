---
title: 使用内核模式性能计数器
description: 使用内核模式性能计数器
ms.date: 08/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 70bb418030255915fdc3995d0c77ab8bec9c78f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822549"
---
# <a name="using-kernel-mode-performance-counters"></a>使用内核模式性能计数器

内核模式组件使用 Windows (PCW) Api 的性能计数器提供性能计数器。

使用以下步骤来开发新的计数器数据提供程序：

1. 编写描述提供程序及其 countersets 的[计数器清单](/windows/win32/perfctrs/performance-counters-schema)。 计数器清单是一种 XML 格式的文件，用于定义性能计数器提供程序及其 countersets。
   - 将 `applicationIdentity` 属性设置为将作为内核模式组件安装的二进制文件的名称，并且将包含性能数据使用者所需的字符串资源。
   - 将 `providerType` 属性设置为 `kernelMode`。
   - `struct` `counterSet/structs` 使用 C/c + + 结构的名称（在将计数器值从组件传递到 PCW api 时将使用），在 ") " 中定义至少一个元素 (。
   - 在每个中 `counter` ， `struct` 定义 `field` PCW 应从中读取计数器值的和。
2. 作为组件的生成过程的一部分，请使用 [CTRPP 工具](/windows/win32/perfctrs/ctrpp) 编译计数器清单。  (计数器预处理器 (CTRPP) 工具包含在 WDK 中，并通过键入在 [开发人员命令提示](/dotnet/framework/tools/developer-command-prompt-for-vs) 中提供 `ctrpp` 。 ) CTRPP 工具会生成 `.rc` 文件和 `.h` 文件。
   - CTRPP 生成的 `.rc` 文件必须由资源编译器 ( # A0) 工具编译，并且生成的 `.res` 文件必须链接到属性中名为的二进制文件 `applicationIdentity` 。 可以直接编译 CTRPP 生成的 `.rc` 文件，也可以 `#include` 将 CTRPP 生成的 `.rc` 文件导入到 `.rc` 正在编译到二进制文件中的现有文件。
   - CTRPP 生成的 `.h` 文件包含用于包装基础 PCW api 的 helper 函数。 例如，CTRPP 生成的 `.h` 文件将包含代表您调用的 **Register**_Xxx_ 函数 `PcwRegister` 。 在大多数情况下，你将调用 CTRPP 生成的帮助程序函数，而不是直接调用任何 PCW Api，但你可以参考 PCW Api 的文档来了解相应的 CTRPP 生成的函数执行的操作。 Helper 函数管理将组件的计数器数据布局转换为 `PCW_DATA` PCW api 所需的布局。
3. 在组件初始化时，调用 CTRPP 生成的用于调用 [**PcwRegister**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)的 **Register**_Xxx_ 函数。 组件关闭时，调用 CTRPP 生成的 **注销**_Xxx_ 函数，该函数将调用 [**PcwUnregister**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwunregister)。
4. 添加代码以提供计数器数据。 这是通过以下方式实现的：实现 [*PCW_CALLBACK*](/windows-hardware/drivers/ddi/wdm/nc-wdm-pcw_callback) 回调函数或维护具有每个实例的计数器值的数据结构，并在创建并销毁实例后调用 CTRPP 生成的 **CreateInstance**_xxx_ 和 **CloseInstance**_Xxx_ 函数。
5. 在组件安装中，请使用 `lodctr /m:<CounterManifest> <InstallPath>` 安装提供程序。 卸载组件时，将 `unlodctr` (与 `/m` 或 `/g` 参数) 以卸载提供程序。 安装提供程序会将提供程序的 countersets 添加到可用 countersets 系统范围的存储库中，以便性能数据使用者（例如 perfmon、typeperf 或 WMI）可以使用 countersets。 具体而言，安装提供程序将记录包含提供程序字符串表的二进制 (DLL、SYS 或 EXE 文件) 的完整路径。 二进制文件的完整路径是通过将清单的 `applicationIdentity` 属性与 `<CounterManifest>` `<InstallPath>` 命令行中使用的和值相结合来确定的，如下所示 `lodctr` ：
   - 如果该 `applicationIdentity` 属性是完整路径，则将使用该路径。
   - 否则，如果 `<InstallationPath>` 参数是完整路径，则将使用该路径。
   - 否则，如果 `<CounterManifest>` 参数是完整路径，则中的目录 `<CounterManifest>` 将与特性中的文件名组合 `applicationIdentity` 。
   - 否则，当前工作目录将与特性中的文件名结合使用 `applicationIdentity` 。

有关内核模式 PCW 提供程序的示例，请参阅 GitHub 上的[Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)存储库中的[内核计数器示例 (Kcs) ](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/perfcounters/kcs) 。

## <a name="related-topics"></a>相关主题

[关于内核模式性能计数器](about-kernel-mode-performance-counters.md)

[性能计数器架构](/windows/win32/perfctrs/performance-counters-schema)

[CTRPP 工具](/windows/win32/perfctrs/ctrpp)

[**PcwRegister**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)

[*PCW_CALLBACK*](/windows-hardware/drivers/ddi/wdm/nc-wdm-pcw_callback)
