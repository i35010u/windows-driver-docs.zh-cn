---
title: 使用静态驱动程序验证程序查找 Windows 驱动程序中的缺陷
description: Static Driver Verifier (SDV) 使用一组接口规则和操作系统的模型来确定该驱动程序正确交互与 Windows 操作系统。
ms.assetid: 94D4104C-66ED-4C1E-8EE1-4C669EB4EAAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecf17c5836dd28eb12f398a4fb11bbf9c342a960
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565869"
---
# <a name="using-static-driver-verifier-to-find-defects-in-windows-drivers"></a>使用静态驱动程序验证程序查找 Windows 驱动程序中的缺陷


Static Driver Verifier (SDV) 使用一组接口规则和操作系统的模型来确定该驱动程序正确交互与 Windows 操作系统。 SDV 可以指向驱动程序中的潜在错误的驱动程序代码中查找缺陷。

SDV 可以分析内核模式驱动程序符合以下驱动程序模型之一：WDM、 KMDF、 NDIS 或 Storport。 有关详细信息，请参阅[支持的驱动程序](supported-drivers.md)并[确定驱动程序或库是否支持 Static Driver Verifier](determining-if-static-driver-verifier-supports-your-driver-or-library.md)。  此外，SDV 不遵循以上的驱动程序模型的驱动程序提供有限的支持 （严格限制的规则集侧重于常规错误，如 null 取消引用）。

### <span id="preparing_your_source_code"></span><span id="PREPARING_YOUR_SOURCE_CODE"></span>

| 准备你的源代码 |
|----------------------------|
|                            |

使用以下步骤来准备用于分析你的代码。

1.  **使用函数角色类型声明驱动程序提供的函数**

    SDV 要求通过使用函数角色类型声明，声明函数。 例如， [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程必须使用驱动程序声明\_INITIALIZE 函数角色类型：

    ```
    DRIVER_INITIALIZE DriverEntry;
    ```

    在声明后你实现 （或定义） 在回调例程按如下所示：

    ```
    /
    // Driver initialization routine
    //
    NTSTATUS 
      DriverEntry( 
        _In_ struct _DRIVER_OBJECT  *DriverObject,
        _In_ PUNICODE_STRING  RegistryPath 
        )
      {
          // Function body
      }
    ```

    每个支持的驱动程序模型有一组用于驱动程序回调函数和调度例程的函数角色类型。 在 WDK 标头文件中声明这些函数角色类型。 例如，下面是该驱动程序的函数原型\_初始化角色类型，因为它将显示在 wdm.h 中。

    ```
    /
    // Define driver initialization routine type.
    //
    _Function_class_(DRIVER_INITIALIZE)
    _IRQL_requires_same_
    typedef
    NTSTATUS
    DRIVER_INITIALIZE (
        _In_ struct _DRIVER_OBJECT *DriverObject,
        _In_ PUNICODE_STRING RegistryPath
        );

    typedef DRIVER_INITIALIZE *PDRIVER_INITIALIZE;
    ```

    因为在 WDK 标头文件中已定义的函数角色类型，只需声明回调函数来为该类型。 在这种情况下，声明*DriverEntry*属于类型**驱动程序\_初始化**。 有关驱动程序模型的函数角色类型的完整列表，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。

2.  **运行的 C/c + + 代码分析**

    若要帮助您确定是否准备好的源代码，请运行[代码分析工具](https://go.microsoft.com/fwlink/p/?linkid=226836)Visual Studio 中。 代码分析工具检查函数角色类型声明，这 SDV 要求。 代码分析工具可以帮助识别可能会遗漏任何函数声明或函数定义的参数不匹配函数角色类型中时向您发出警告。

    -   在 Visual Studio 中打开驱动程序项目。
    -   从**构建**菜单上，单击**对解决方案运行代码分析**。

    结果显示在**代码分析**窗口。 解决可能疏漏的任何函数声明。 因此，它能够运行生成你的解决方案时，还可以配置代码分析工具。

    下表显示了一些代码分析工具可能会发现在驱动程序代码中的警告。 若要运行 Static Driver Verifier，您的驱动程序必须是免费的这些缺陷。

    | C/c + + 警告的代码分析 | 描述                                                                                                                         |
    |---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
    | C28101                          | 驱动程序模块已推断当前函数，是&lt;函数类型&gt;函数                                       |
    | C28022                          | 有关该函数的函数类与使用定义它的 typedef 上的函数类不匹配。                       |
    | C28023                          | 分配或传递的函数应有\_函数\_类\_至少一个类批注                |
    | C28024                          | 函数指针分配给将批注与函数类，它不包含在函数类的列表。 |
    | C28169                          | 调度函数&lt;函数&gt;没有任何\_调度\_类型\_批注                                             |
    | C28208                          | 函数签名与函数声明不匹配                                                                     |



### <span id="running_static_driver_verifier"></span><span id="RUNNING_STATIC_DRIVER_VERIFIER"></span>

| 运行的 Static Driver Verifier |
|--------------------------------|
|                                |

1.  在 Visual Studio 中打开驱动程序项目 (.vcxProj) 文件。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

    这将打开 Static Driver Verifier 应用程序，其中可以控制、 配置和计划时 Static Driver Verifier 执行分析。

2.  如果您的驱动程序包含一个库，请单击**库**选项卡，单击**添加库**添加库。

    浏览到库源代码的目录，并选择项目文件 (.vcxProj)。 添加所有驱动程序包括的库。 SDV 分析您的驱动程序之前，必须添加库。 当你启动您的驱动程序的分析时，SDV 还可以分析尚未处理的库。 处理一个库后，它存储在全局 SDV 缓存。 有关详细信息，请参阅[库处理中 Static Driver Verifier](library-processing-in-static-driver-verifier.md)

3.  检查 Static Driver Verifier 的配置设置。 单击**配置**选项卡。

    **项目配置**项目配置显示了配置和你在 Visual Studio 中选择的平台设置。

    **资源**在大多数情况下，可以使用默认设置。 如果 SDV 报告超时、 放弃、 或 Spaceout，您可以尝试调整这些设置。 有关详细信息，请参阅[建议的故障排除 Static Driver Verifier](recommendations-for-troubleshooting-static-driver-verifier.md)。

    **计划**选择开始时间开始验证。 默认设置是在单击后立即开始分析**启动**上**Main**选项卡。根据该驱动程序和其复杂性的大小，静态分析可能需要很长时间才能运行。 你可能想要计划要为您; 最方便的时候开始分析例如，在一天结束。

    **请注意**请务必检查您的计算机的电源管理计划，以确保计算机不会进入睡眠状态在分析过程。



4.  单击**规则**选项卡以选择哪些驱动程序 API 使用规则以验证何时开始分析。

    Static Driver Verifier 检测到类型的驱动程序 （WDF、 WDM、 NDIS 或 Storport） 分析和选择的驱动程序类型的默认规则集。 如果这是首次在您的驱动程序运行 SDV，应运行的默认规则集。

    有关规则的信息，请参阅[DDI 符合性规则](https://msdn.microsoft.com/library/windows/hardware/ff552840)。

5.  启动的静态分析。 单击**Main**选项卡，然后单击**启动**。 当您单击**启动**、 显示一条消息，告知你此计划静态分析和分析可能需要很长时间才能运行。 单击“确定”  继续。 在你计划的时间开始分析。

### <span id="viewing_and_analyzing_the_results"></span><span id="VIEWING_AND_ANALYZING_THE_RESULTS"></span>

| 查看和分析结果 |
|-----------------------------------|
|                                   |

随着进行静态分析，SDV 报告分析的状态。 分析完成后，SDV 报告的结果和统计信息。 如果该驱动程序无法满足 API 使用情况的规则，结果将被报告为一个缺陷。

如果遇到任何问题，SDV 显示那些 on**警告**并**错误**页。 **驱动程序属性**页显示的某些驱动程序属性的测试结果。 驱动程序属性测试用于标识要进一步限定分析的驱动程序功能。 可以使用**驱动程序属性**结果以确认预期的属性，支持您的驱动程序的功能。

若要查看在特定缺陷[静态驱动程序验证工具报告](static-driver-verifier-report.md)，单击在缺陷**结果**窗格。 这将打开[跟踪查看器](defect-viewer.md)，其中显示的代码路径的跟踪规则发生冲突。 有关详细信息，请参阅[解释静态驱动程序验证工具结果](interpreting-static-driver-verifier-results.md)。

**请注意**Static Driver Verifier 保留结果和分析设置。 若要清除结果，请单击**清理**。



### <a name="span-idtroubleshootingsdvresultsspanspan-idtroubleshootingsdvresultsspantroubleshooting-static-driver-verifier-results"></a><span id="troubleshooting_sdv_results"></span><span id="TROUBLESHOOTING_SDV_RESULTS"></span>Static Driver Verifier 结果进行故障排除

如果 SDV 报告未找到任何缺陷，请检查**Main**选项卡，确保已检测到入口点。 如果该驱动程序不通过使用函数角色类型声明函数，SDV 将无法分析和查找驱动程序代码中的缺陷。 有关详细信息，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。

如果 SDV 报告超时或失败返回有用的结果，您可能需要更改几个 SDV 配置选项。 有关如何解决 SDV 的详细信息，请参阅[建议的故障排除 Static Driver Verifier](recommendations-for-troubleshooting-static-driver-verifier.md)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[确定是否 Static Driver Verifier 支持驱动程序或库](determining-if-static-driver-verifier-supports-your-driver-or-library.md)

[使用函数角色类型声明](using-function-role-type-declarations.md)

[Static Driver Verifier 规则](https://msdn.microsoft.com/library/windows/hardware/ff552840)

[代码分析工具](https://go.microsoft.com/fwlink/p/?linkid=226836)










