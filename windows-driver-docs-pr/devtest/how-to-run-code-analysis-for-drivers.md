---
title: 如何为驱动程序运行代码分析
description: 驱动程序的代码分析提供了有关在源代码中可能存在的缺陷的信息。 可以手动运行代码分析，您还可以运行代码分析自动使用每个生成。
ms.assetid: BDD4EC2C-FB23-44BE-9A52-F98774AC7268
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7afc921336f407ef693fe94ebdced0a0d5cfb6c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330658"
---
# <a name="how-to-run-code-analysis-for-drivers"></a>如何为驱动程序运行代码分析

驱动程序的代码分析提供了有关在源代码中可能存在的缺陷的信息。 可以手动运行代码分析，您还可以运行代码分析自动使用每个生成。

本主题内容：

* [运行代码分析](#running-code-analysis)
* [查看代码分析结果](#viewing-the-code-analysis-results)
* [禁止显示缺陷的报告](#suppressing-the-report-of-defects)
* [对于警告 C6262 内核模式驱动程序的不断变化的堆栈使用限制](#changing-stack-usage-limits-for-warning-c6262-for-kernel-mode-drivers)
* [相关的主题](#related-topics)

## <a name="running-code-analysis"></a>运行代码分析

### <a name="to-run-code-analysis-on-driver-source-code-manually"></a>若要对驱动程序源代码中手动运行代码分析

1. 在 Visual Studio 中，选择的驱动程序项目文件或解决方案并选择的项目配置和平台来分析。
2. 从**分析**或**生成**菜单，单击**对解决方案运行代码分析**。

### <a name="to-run-code-analysis-on-driver-source-code-automatically-with-each-build"></a>若要对驱动程序源代码，使用每个生成自动运行代码分析

1. 在 Visual Studio 中，右键单击驱动程序项目或解决方案**解决方案资源管理器**然后单击**属性**。
2. 在项目属性对话框中，单击**代码分析**。
3. 在中**于 c 语言的代码分析 /C++属性**页上，选择想要分析 （例如，Windows 8 和 Win32） 的项目配置和平台。
4. 选择**于 c 语言时启用代码分析 /C++上生成**。
5. 在规则集下选择**Microsoft 驱动程序建议规则**。 这是为驱动程序设置的默认规则。
6. 在中**构建**菜单上，单击**生成解决方案**。

## <a name="viewing-the-code-analysis-results"></a>查看代码分析结果

如有可能的源代码中找到缺陷**代码分析结果**窗口出现缺陷的源文件中显示的代码分析警告号和行号。

### <a name="to-view-defects"></a>若要查看缺陷

1. 在中**代码分析结果**窗口中，单击行号和缺陷的说明会显示在**代码分析结果**窗口。

   代码窗口显示的源代码，并指明发生故障。

2. 若要了解有关特定的警告的详细信息，请单击中的警告**代码分析结果**窗口。

### <a name="to-view-the-code-analysis-log-file-associated-with-a-build"></a>若要查看与生成关联的代码分析日志文件

1. 导航到你的生成配置和平台的目录 (例如， `\\Windows7Release\\x64`)。
2. 如果你使用建议的规则，日志文件被称为`vc.\*codeanalysis.xml`。 如果要为 Windows Server 2012 中创建一个驱动程序，此文件用于创建驱动程序验证日志。

## <a name="suppressing-the-report-of-defects"></a>禁止显示缺陷的报告

在某些情况下，你可能想要禁止显示的特定警告消息; 报表例如，如果警告为主要是信息性，并且您知道错误的原因。

### <a name="to-suppress-warning-messages"></a>若要禁止显示警告消息

1. 若要删除的报告缺陷实例，选择的行号和中的警告**代码分析结果**窗口。
2. 在该警告的详细说明，单击**操作** &gt; **禁止显示消息** &gt; **源中**。

   具有 suppress 说明符的杂注警告指令将禁止显示警告仅为紧跟在后面的代码行\#杂注警告语句。

    ```command
    #pragma warning(suppress: 6014)
    ```

## <a name="changing-stack-usage-limits-for-warning-c6262-for-kernel-mode-drivers"></a>对于警告 C6262 内核模式驱动程序的不断变化的堆栈使用限制

在用户模式和内核模式代码中，堆栈空间是有限的并提交页面堆栈的失败会导致堆栈溢出异常。 高堆栈使用是特别是在内核模式下的问题，因为可用的总的堆栈空间是仅为 12 KB。 内核模式代码应主动的方式限制堆栈使用。

代码分析工具会发出警告[C6262](https://go.microsoft.com/fwlink/p/?linkid=321750)如果在函数中本地使用超过 1 KB 的堆栈空间。 如果你想要调查可能会占用大量资源的函数，可以自定义或较低的堆栈阈值限制由[C6262](https://go.microsoft.com/fwlink/p/?linkid=321750)。 如果您降低堆栈阈值限制，代码分析工具可能会找到更多的问题。 然后，可以解决这些堆栈使用情况问题。 例如，可以减小到 400 个字节的阈值以查看是否其他函数所使用的资源。

### <a name="to-customize-the-stacksize-limit-for-c6262"></a>若要自定义 C6262 stacksize 限制

1. 在记事本或其他文本编辑器中，为内核模式驱动程序 （或组件） 中打开 Visual Studio 项目文件 (.vcxproj)。
2. 添加一个新 **\<ItemDefinitionGroup\>** 编译器 **\<ClCompile\>** 。
3. 添加 **\<PREfastAdditionalOptions\>** 元素，并设置**stacksize\<字节\>** 。 默认值是**stacksize1024**。

```XML
     <ItemDefinitionGroup>
       <ClCompile>


      <!-- Change stack depth for C6262 from 1024 to 400 -->
      <PREfastAdditionalOptions>stacksize400</PREfastAdditionalOptions>

    </ClCompile>
  </ItemDefinitionGroup>
```

4. 保存项目文件。 启动 Visual Studio 中，加载已更新的驱动程序的项目，并运行代码分析。

   若要恢复为默认值为 1 KB，请撤消对项目文件中，所做的更改，或更改到的堆栈大小值**stacksize1024**。

## <a name="related-topics"></a>相关主题

[代码分析驱动程序警告](prefast-for-drivers-warnings.md)
