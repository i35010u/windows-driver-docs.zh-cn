---
title: 构建用于 Windows 的多个版本的 WDF 驱动程序
description: 介绍如何构建用于 Windows 的多个版本的 WDF 驱动程序。
ms.date: 04/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 85816ea4d802853f730b5279e83724d4f4890b3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525499"
---
# <a name="building-a-wdf-driver-for-multiple-versions-of-windows"></a>构建用于 Windows 的多个版本的 WDF 驱动程序

WDF 始终允许您一次生成一个驱动程序，并使用生成的二进制文件在多个版本的 Windows，但之前 Windows 10 版本 1803 (Redstone 4)，这被限制为"基于较旧，更高版本上运行。" WDF 启动 Windows 10 版本 1803年中，添加"生成更高版本，运行更早版本，"有条件执行的其他优势。 总结：
* **现有**:与较早版本的 framework 包括提供的主版本的框架的较新版本的 Windows 版本上运行生成的二进制文件匹配。 例如，使用 KMDF 1.9 (Windows 7) 构建的驱动程序在 Windows 8 系统 (KMDF 1.11) 上运行。 在示例中，该驱动程序被限制为 KMDF 1.9 的意大功能。
* **添加项**：从版本 1.25 KMDF 和 UMDF 上 Windows 10 版本 1803年的版本 2.25，可以构建与较新的 framework 版本的驱动程序和生成的驱动程序二进制文件在早期版本的 Windows （在最小的 Windows 10 版本 1803年) 上运行。 此外，驱动程序可以有条件地使用选项仅适用于更高版本的 framework 版本的功能。

这意味着，不仅不您的驱动程序运行在未来版本的 Windows，因为它始终都有，但它还返回到 Windows 10 版本 1803年运行有关以前版本。

有两个步骤执行此操作： 在 Visual Studio 中，指定生成设置和执行 API 调用或访问的结构或可能或可能不会显示的字段之前运行时检查。

**注意**：此功能是可选的它生成的驱动程序，同时保持可加载没有最新的 WDF 功能的 Windows 的早期版本上使用的最新的 WDF 功能，才应启用驱动程序。

如果未设置**次要版本 （目标版本）** 或**次要版本 （最低要求）**，版本控制保持不变像以前一样。

## <a name="specifying-minimum-required"></a>指定所需的最小值

在 Visual Studio 中的新配置设置如下：
* **KMDF 版本次要 （最低要求）**
* **UMDF 版本次要 （最低要求）**

根据此更改后，更新了两个现有设置的名称：
* **KMDF 版本次要** -> **KMDF 版本次要 （目标版本）**
* **UMDF 版本次要** -> **UMDF 版本次要 （目标版本）**

如果未设置**所需的最小**，Visual Studio 生成**目标版本**和，并不提供低级支持。 这与旧的行为一致**次要版本**属性。

如果设置**所需的最小**，必须满足以下要求：
* 25 < = 所需的最小值 < = 目标版本
* 在中**配置属性-> 驱动程序设置-> 常规**，请设置`_NT_TARGET_VERSION`到`0x0A000005`(RS4) 或更高版本。

## <a name="checking-if-functionality-is-present"></a>正在检查功能是否存在

在每次使用 API、 结构或成员，可能会或可能不会显示之前, 必须调用 WdfFuncEnum.h 中定义的以下宏之一：

```cpp
BOOLEAN
WDF_IS_FUNCTION_AVAILABLE (
    FunctionName
    );

BOOLEAN
WDF_IS_STRUCTURE_AVAILABLE (
    StructName
    );

BOOLEAN
WDF_IS_FIELD_AVAILABLE (
    StructName,
    FieldName
    );
```

请考虑下面的示例。  WDF v29 发布时，它将添加一个新的 API:**WdfSomeNewFeature**。 如果您设置**目标版本**为 29 和**最低要求**为 25，25 到 29 从任何 framework 版本上加载该生成的驱动程序 （和更高版本，只要主版本不会更改），调用版本 25Api 一样，并使任何 v29 API 每次调用之前的以下检查：

```cpp
if (WDF_IS_FUNCTION_AVAILABLE(WdfSomeNewFeature)) {
    WdfSomeNewFeature();
}
```

如果不执行条件检查，您可能会看到以下信息：
-   如果 API 返回 NTSTATUS，调用会返回失败代码。
-   如果 API 返回 NTSTATUS 之外的任何内容：
    - KMDF:机 bug 检查。
    - UMDF:WudfHost 进程崩溃并出现 DriverStop 错误。
-   如果启用了驱动程序验证程序，该驱动程序崩溃以及。 这有助于确定在测试环境中的问题。
-   无提示的内存损坏 （时访问的结构或字段）。

驱动程序故障包含故障的驱动程序名称、 框架名称和失败的 API 索引。 可以通过查找 WDFFUNCENUM WdfFuncEnum.h 中的值来检索 API 的名称。

WDF 的 Visual Studio 属性的详细信息，请参阅[驱动程序项目的驱动程序模型设置属性](../develop/driver-model-settings-properties-for-driver-projects.md)。
