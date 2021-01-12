---
title: 使用静态驱动程序验证程序查找 Windows 驱动程序中的缺陷
description: 静态驱动程序验证器 (SDV) 使用一组接口规则和操作系统模型来确定驱动程序是否与 Windows 操作系统正确交互。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a054167b50d2dd207abd71b252f0619758d719cd
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124163"
---
# <a name="using-static-driver-verifier-to-find-defects-in-windows-drivers"></a>使用静态驱动程序验证程序查找 Windows 驱动程序中的缺陷

静态驱动程序验证器 (SDV) 使用一组接口规则和操作系统模型来确定驱动程序是否与 Windows 操作系统正确交互。 SDV 在驱动程序代码中查找一些缺陷，这些缺陷可能指向驱动程序中的潜在 bug。

SDV 可以分析符合以下驱动程序模型之一的内核模式驱动程序： WDM、KMDF、NDIS 或 Storport。 有关详细信息，请参阅 [支持的驱动程序](supported-drivers.md) 和 [确定 Static driver Verifier 是否支持驱动程序或库](determining-if-static-driver-verifier-supports-your-driver-or-library.md)。  此外，SDV 还 (严格限制的规则集提供有限的支持，该规则集中侧重于对不遵循以上驱动程序模型的驱动程序) 取消引用的常规错误。

## <a name="preparing-your-source-code"></a>准备源代码

使用以下步骤准备要分析的代码。

1. **使用函数角色类型声明驱动程序提供的函数**

    SDV 要求通过使用函数角色类型声明来声明函数。 例如，必须使用[](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)驱动程序 \_ 初始化函数角色类型声明 DriverEntry 例程：

    ```command
    DRIVER_INITIALIZE DriverEntry;
    ```

    在声明后，按如下所示实现 (或定义) 回调例程：

    ```command
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

    每个受支持的驱动程序模型都具有一组用于驱动程序回调函数和调度例程的函数角色类型。 这些函数角色类型在 WDK 标头文件中声明。 例如，下面是驱动程序初始化角色类型的函数原型， \_ 因为它显示在 Wdm. h 中。

    ```command
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

    由于已在 WDK 标头文件中定义了函数角色类型，因此只需将回调函数声明为该类型。 在这种情况下，将 *DriverEntry* 声明为 **驱动程序 \_ 初始化** 类型。 有关驱动程序模型的函数角色类型的完整列表，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md)。

2. **运行 C/c + + 代码分析**

    为了帮助您确定是否已准备好源代码，请在 Visual Studio 中运行 [代码分析工具](/previous-versions/visualstudio/visual-studio-2013/dd264897(v=vs.120)) 。 代码分析工具将检查 SDV 要求的函数角色类型声明。 当函数定义的参数与函数角色类型中的参数不匹配时，代码分析工具可帮助确定任何可能已丢失或发出警告的函数声明。

    - 在 Visual Studio 中打开驱动程序项目。
    - 在 " **生成** " 菜单中，单击 " **对解决方案运行代码分析**"。

    结果将显示在 " **代码分析** " 窗口中。 修复任何可能丢失的函数声明。 你还可以配置代码分析工具，使其在每次生成解决方案时运行。

    下表显示了代码分析工具可能在你的驱动程序代码中找到的一些警告。 若要运行静态驱动程序验证程序，你的驱动程序需要没有这些缺陷。

    | C/c + + 代码分析警告 | 描述                                                                                                                         |
    |---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
    | C28101                          | 驱动程序模块已推断出当前函数是 &lt; 函数类型 &gt; 函数                                       |
    | C28022                          | 此函数的函数类 (es) 与用于定义它的 typedef 上的函数类 (es) 不匹配。                       |
    | C28023                          | 分配或传递的函数应该 \_ \_ 至少有一个类的函数类 \_ 注释 (es)                 |
    | C28024                          | 向其分配的函数指针是用函数类进行批注的，函数类不包含在函数类中 (es) 列表。 |
    | C28169                          | 调度函数 &lt; 函数没有 &gt; 任何 \_ 调度 \_ 类型 \_ 批注                                             |
    | C28208                          | 函数签名与函数声明不匹配                                                                     |

## <a name="running-static-driver-verifier"></a>运行静态驱动程序验证程序

1. 在 Visual Studio 中打开驱动程序项目 ( .Vcxproj) 文件。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

    这会打开静态驱动程序验证程序应用程序，你可以在其中控制、配置和计划静态驱动程序验证程序执行分析的时间。

2. 如果驱动程序包含库，请单击 " **库** " 选项卡，然后单击 " **添加库** " 以添加库。

    浏览到库源代码的目录，并选择项目文件 ( ".Vcxproj") 。 添加驱动程序包含的所有库。 在 SDV 分析驱动程序之前，必须添加这些库。 当你开始分析你的驱动程序时，SDV 还会分析尚未处理的库。 库处理完毕后，将存储在全局 SDV 缓存中。 有关详细信息，请参阅 [静态驱动程序验证程序中的库处理](library-processing-in-static-driver-verifier.md)

3. 检查静态驱动程序验证程序的配置设置。 单击 **“配置”** 选项卡。

    **项目配置** 项目配置显示您在 Visual Studio 中选择的配置和平台设置。

    **资源** 在大多数情况下，您可以使用默认设置。 如果 SDV 报告 "超时"、"放弃" 或 "Spaceout"，则可以尝试调整这些设置。 有关详细信息，请参阅 [静态驱动程序验证程序疑难解答的建议](recommendations-for-troubleshooting-static-driver-verifier.md)。

    **计划** 选择开始验证的开始时间。 默认设置是在单击 **主** 选项卡上的 "**启动**" 后立即开始分析。静态分析可能需要较长时间才能运行，具体取决于驱动程序的大小及其复杂性。 你可能希望将分析计划为在最方便的时候开始分析;例如，在一天结束时。

    >[!NOTE]
    >] 确保检查计算机的电源管理计划，以确保在分析期间计算机不会进入睡眠状态。

4. 单击 " **规则** " 选项卡，选择在启动分析时要验证的驱动程序 API 使用规则。

    静态驱动程序验证程序检测到正在分析的驱动程序类型 (WDF、WDM、NDIS 或 Storport) 并为驱动程序类型选择默认的规则集。 如果这是你第一次在你的驱动程序上运行 SDV，则应该运行默认规则集。

    有关规则的信息，请参阅 [DDI 合规性规则](/windows-hardware/drivers/ddi/index)。

5. 开始静态分析。 单击 " **主** " 选项卡，然后单击 " **启动**"。 单击 " **启动**" 时，将显示一条消息，告知你计划了静态分析并且分析可能需要较长时间才能运行。 单击 **“确定”** 继续。 分析从你计划的时间开始。

## <a name="viewing-and-analyzing-the-results"></a>查看并分析结果

在静态分析过程中，SDV 将报告分析的状态。 分析完成后，SDV 会报告结果和统计信息。 如果驱动程序无法满足 API 使用规则，则结果将报告为缺陷。

如果遇到任何问题，SDV 将在 " **警告** " 和 " **错误** " 页上显示这些问题。 " **驱动程序属性** " 页显示某些驱动程序属性的测试结果。 驱动程序属性测试用于标识驱动程序功能，以进一步限定分析。 您可以使用 **驱动程序属性** 结果来确认您的驱动程序所需的属性和支持的功能。

若要查看 [静态驱动程序验证程序报告](static-driver-verifier-report.md)中的特定缺陷，请在 **结果** 窗格中单击 "缺陷"。 这会打开 [跟踪查看器](defect-viewer.md)，其中显示规则冲突的代码路径跟踪。 有关详细信息，请参阅 [解释静态驱动程序验证程序结果](interpreting-static-driver-verifier-results.md)。

>[!NOTE]
>静态驱动程序验证程序保留分析的结果和设置。 若要清除结果，请单击 " **清除**"。

## <a name="troubleshooting-static-driver-verifier-results"></a>静态驱动程序验证程序结果疑难解答

如果 SDV 报告未找到缺陷，请检查 **主** 选项卡以确保检测到入口点。 如果驱动程序没有使用函数角色类型声明函数，则 SDV 将无法分析和查找驱动程序代码中的缺陷。 有关详细信息，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md)。

如果 SDV 报告超时或无法返回有用的结果，则可能需要更改几个 SDV 配置选项。 有关如何对 SDV 进行故障排除的详细信息，请参阅 [对静态驱动程序验证程序进行故障排除的建议](recommendations-for-troubleshooting-static-driver-verifier.md)。

## <a name="related-topics"></a>相关主题

[确定静态驱动程序验证程序是否支持你的驱动程序或库](determining-if-static-driver-verifier-supports-your-driver-or-library.md)

[使用函数角色类型声明](using-function-role-type-declarations.md)

[静态驱动程序验证程序规则](./static-driver-verifier-rules.md)

[代码分析工具](/previous-versions/visualstudio/visual-studio-2013/dd264897(v=vs.120))