---
title: 如何运行驱动程序的代码分析
description: 驱动程序代码分析提供有关源代码中可能缺陷的信息。 您可以手动运行代码分析，还可以在每次生成时自动运行代码分析。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2925743737073f65eca199286de5e1e4e5fc8a5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809659"
---
# <a name="how-to-run-code-analysis-for-drivers"></a>如何运行驱动程序的代码分析

驱动程序代码分析提供有关源代码中可能缺陷的信息。 您可以手动运行代码分析，还可以在每次生成时自动运行代码分析。

本主题内容：

* [运行代码分析](#running-code-analysis)
* [查看代码分析结果](#viewing-the-code-analysis-results)
* [禁止显示缺陷报告](#suppressing-the-report-of-defects)
* [更改内核模式驱动程序的警告 C6262 的堆栈使用限制](#changing-stack-usage-limits-for-warning-c6262-for-kernel-mode-drivers)
* [相关主题](#related-topics)

## <a name="running-code-analysis"></a>运行代码分析

### <a name="to-run-code-analysis-on-driver-source-code-manually"></a>手动对驱动程序源代码运行代码分析

1. 在 Visual Studio 中，选择 "驱动程序" 项目文件或解决方案，然后选择要分析的项目配置和平台。
2. 从“分析”  或“生成”  菜单中，单击“对解决方案运行代码分析”  。

### <a name="to-run-code-analysis-on-driver-source-code-automatically-with-each-build"></a>在每次生成时自动运行针对驱动程序源代码的代码分析

1. 在 Visual Studio 中，右键单击驱动程序项目或 **解决方案资源管理器** 中的解决方案，然后单击 " **属性**"。
2. 在项目的 "属性" 对话框中，单击 " **代码分析**"。
3. 在 " **C/c + + 代码分析" 属性** 页上，选择要分析的项目配置和平台 (例如，Windows 8 和 Win32) 。
4. 选择 **"生成时启用 c/c + + 代码分析"**。
5. 在 "规则集" 下，选择 " **Microsoft 驱动程序建议规则**"。 这是驱动程序的默认规则集。
6. 在 " **生成** " 菜单中，单击 " **生成解决方案**"。

## <a name="viewing-the-code-analysis-results"></a>查看代码分析结果

如果在源代码中找到可能的缺陷，则 **代码分析结果** 窗口将显示代码分析警告编号以及发生缺陷的源文件中的行号。

### <a name="to-view-defects"></a>查看缺陷

1. 在 " **代码分析结果** " 窗口中，单击 " **代码分析结果** " 窗口中显示的行号和缺陷说明。

   "代码" 窗口显示源代码并指示缺陷发生的位置。

2. 若要了解有关特定警告的详细信息，请在 " **代码分析结果** " 窗口中单击该警告。

### <a name="to-view-the-code-analysis-log-file-associated-with-a-build"></a>查看与生成关联的代码分析日志文件

1. 导航到生成配置和平台 (的目录，例如 `\\Windows7Release\\x64`) 。
2. 如果使用推荐的规则，则会调用日志文件 `vc.\*codeanalysis.xml` 。 如果要为 Windows Server 2012 创建驱动程序，则此文件用于创建驱动程序验证日志。

## <a name="suppressing-the-report-of-defects"></a>禁止显示缺陷报告

在某些情况下，您可能需要禁止显示特定警告消息的报告;例如，如果警告主要是信息性的，并且你知道该错误的原因。

### <a name="to-suppress-warning-messages"></a>禁止显示警告消息

1. 若要删除已报告缺陷的实例，请在 " **代码分析结果** " 窗口中选择行号和警告。
2. 在警告的展开说明中，单击 " **操作**" " &gt; **禁止** &gt; **在源中** 显示消息"。

   带有禁止显示说明符的杂注警告指令禁止仅对紧跟在 pragma warning 语句后面的代码行出现警告 \# 。

    ```command
    #pragma warning(suppress: 6014)
    ```

## <a name="changing-stack-usage-limits-for-warning-c6262-for-kernel-mode-drivers"></a>更改内核模式驱动程序的警告 C6262 的堆栈使用限制

在用户模式和内核模式代码中，堆栈空间有限，如果无法提交堆栈页，将导致堆栈溢出异常。 由于可用的总堆栈空间仅为 12 KB，因此堆栈更高的使用在内核模式下尤其重要。 内核模式代码应严格限制堆栈使用。

如果在函数中本地使用的堆栈空间超过 1 KB，代码分析工具将发出警告 [C6262](/cpp/code-quality/c6262) 。 如果要调查可能会消耗大量资源的函数，可以自定义或降低 [C6262](/cpp/code-quality/c6262)使用的堆栈阈值限制。 如果降低堆栈阈值限制，代码分析工具可能会发现更多问题。 然后，可以选择解决这些堆栈使用问题。 例如，可以将阈值减小到400字节，以查看其他函数是否正在使用资源。

### <a name="to-customize-the-stacksize-limit-for-c6262"></a>自定义 C6262 的 stacksize 限制

1. 在记事本或其他文本编辑器中打开内核模式驱动程序的 Visual Studio 项目文件 ()  (或组件) 。
2. **\<ItemDefinitionGroup\>** 为编译器添加新的 **\<ClCompile\>** 。
3. 添加 **\<PREfastAdditionalOptions\>** 元素并设置 **stacksize \<bytes\>**。 默认值为 **stacksize1024**。

```XML
     <ItemDefinitionGroup>
       <ClCompile>


      <!-- Change stack depth for C6262 from 1024 to 400 -->
      <PREfastAdditionalOptions>stacksize400</PREfastAdditionalOptions>

    </ClCompile>
  </ItemDefinitionGroup>
```

4. 保存项目文件。 启动 Visual Studio，加载更新的驱动程序项目，并运行代码分析。

   若要恢复为默认值 1 KB，请撤消对项目文件所做的更改，或将 "堆栈大小" 值更改为 " **stacksize1024**"。

## <a name="related-topics"></a>相关主题

[驱动程序的代码分析警告](prefast-for-drivers-warnings.md)
