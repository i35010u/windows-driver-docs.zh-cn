---
title: 编写分析扩展插件以扩展分析
description: 您可以通过编写分析扩展插件来扩展 "分析调试器" 命令的功能。
ms.assetid: 7648F789-85D5-4247-90DD-2EAA43543483
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab72c46243c129717de6413726abc4462a6bdd3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834170"
---
# <a name="writing-an-analysis-extension-plugin-to-extend-analyze"></a>正在写入分析扩展插件！分析


可以通过编写分析扩展插件来扩展[ **！分析**](-analyze.md)调试器命令的功能。 通过提供分析扩展插件，您可以以特定于您自己的组件或应用程序的方式参与对 bug 检查或异常的分析。

编写分析扩展插件时，还需要编写一个元数据文件，用于描述要为其调用插件的情况。 当[ **！分析**](-analyze.md)运行时，它会查找、加载和运行相应的分析扩展插件。

若要写入分析扩展插件并使其可用于[ **！分析**](-analyze.md)，请执行以下步骤。

-   创建一个 DLL，该 DLL 导出[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)函数。
-   创建与您的 DLL 同名的元数据文件，并创建 alz 扩展名。 例如，如果您的 DLL 名为 MyAnalyzer，则元数据文件必须命名为 MyAnalyzer. alz。 有关如何创建元数据文件的信息，请参阅[Analysis extension 的元数据文件](metadata-files-for-analysis-extensions.md)。 将元数据文件放在与 DLL 相同的目录中。
-   在调试器中，使用[**extpath**](-extpath--set-extension-path-.md)命令将目录添加到扩展文件路径。 例如，如果 DLL 和元数据文件位于名为 c：\\MyAnalyzer 的文件夹中，请输入**extpath + c：\\MyAnalyzer**。

当 "[**分析**](-analyze.md)" 命令在调试器中运行时，分析引擎会在扩展文件路径中查找扩展名为 alz 的元数据文件。 分析引擎读取元数据文件，以确定应加载哪些分析扩展插件。 例如，假设分析引擎正在运行，以响应错误检查，0xA IRQL\_不\_\_或\_相等，并且读取名为 MyAnalyzer alz 的元数据文件，该文件包含以下条目。

```text
PluginId       MyPlugin
DebuggeeClass  Kernel
BugCheckCode   0xA
BugCheckCode   0xE2
```

条目 `BugCheckCode  0x0A` 指定此插件要参与 Bug 检查0xA 分析，以便分析引擎加载 MyAnalyzer （它必须位于与 MyAnalyzer 相同的目录中，并调用其[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)函数。

**请注意**  元数据文件的最后一行必须以换行符结尾。

 

## <a name="span-idskeleton_examplespanspan-idskeleton-examplespanspan-idskeleton_examplespanskeleton-example"></a><span id="Skeleton_Example"></span><span id="skeleton-example"></span><span id="SKELETON_EXAMPLE"></span>框架示例


下面是一个框架示例，可以将其用作起始点。

1.  生成一个名为 MyAnalyzer 的 DLL，该 DLL 将导出此处显示的[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)函数。

    ```cpp
    #include <windows.h>
    #define KDEXT_64BIT
    #include <wdbgexts.h>
    #include <dbgeng.h>
    #include <extsfns.h>

    extern "C" __declspec(dllexport) HRESULT _EFN_Analyze(_In_ PDEBUG_CLIENT4 Client, 
       _In_ FA_EXTENSION_PLUGIN_PHASE CallPhase, _In_ PDEBUG_FAILURE_ANALYSIS2 pAnalysis)
    { 
       HRESULT hr = E_FAIL;

       PDEBUG_CONTROL pControl = NULL;
       hr = Client->QueryInterface(__uuidof(IDebugControl), (void**)&pControl);

       if(S_OK == hr && NULL != pControl)
       {
          IDebugFAEntryTags* pTags = NULL;
          pAnalysis->GetDebugFATagControl(&pTags);

          if(NULL != pTags)
          {
             if(FA_PLUGIN_INITILIZATION == CallPhase)
             { 
                pControl->Output(DEBUG_OUTPUT_NORMAL, "My analyzer: initialization\n");  
             }
             else if(FA_PLUGIN_STACK_ANALYSIS == CallPhase)
             {
                pControl->Output(DEBUG_OUTPUT_NORMAL, "My analyzer: stack analysis\n"); 
             }
             else if(FA_PLUGIN_PRE_BUCKETING == CallPhase)
             {
                pControl->Output(DEBUG_OUTPUT_NORMAL, "My analyzer: prebucketing\n");
             }
             else if(FA_PLUGIN_POST_BUCKETING == CallPhase)
             {
                pControl->Output(DEBUG_OUTPUT_NORMAL, "My analyzer: post bucketing\n");    
                FA_ENTRY_TYPE entryType = pTags->GetType(DEBUG_FLR_BUGCHECK_CODE);       
                pControl->Output(DEBUG_OUTPUT_NORMAL, "The data type for the DEBUG_FLR_BUGCHECK_CODE tag is 0x%x.\n\n", entryType);
             }
          }

          pControl->Release();
       }
       return hr;
    }
    ```

2.  创建一个名为 MyAnalyzer. alz 的元数据文件，该文件包含以下条目。

    ```text
    PluginId      MyPlugin
    DebuggeeClass Kernel
    BugCheckCode  0xE2
    ```

    **请注意**  元数据文件的最后一行必须以换行符结尾。

     

3.  建立主机和目标计算机之间的内核模式调试会话。

4.  在主计算机上，将 MyAnalyzer 和 MyAnalyzer 放在文件夹 c：\\MyAnalyzer 中。

5.  在主计算机上的调试器中，输入以下命令。

    **. extpath + c：\\MyAnalyzer**

    **。崩溃**

6.  [**崩溃**](-crash--force-system-crash-.md)命令手动生成 Bug 检查 0xE2\_在目标计算机上启动\_崩溃，这会导致主计算机上的调试器中断。 Bug 检查分析引擎（在主计算机上的调试器中运行）读取 MyAnalyzer，并发现 MyAnalyzer 能够参与分析 bug 检查0xE2。 因此，分析引擎加载 MyAnalyzer 并调用其[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)函数。

    验证是否在调试器中看到类似于下面的输出。

    ```dbgcmd
    *                        Bugcheck Analysis                                    *
    *                                                                             *
    *******************************************************************************

    Use !analyze -v to get detailed debugging information.

    BugCheck E2, {0, 0, 0, 0}

    My analyzer: initialization
    My analyzer: stack analysis
    My analyzer: prebucketing
    My analyzer: post bucketing
    The data type for the DEBUG_FLR_BUGCHECK_CODE tag is 0x1.
    ```

以上调试器输出显示，分析引擎调用[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)函数四次：一次针对分析的每个阶段。 分析引擎传递 **\_EFN\_分析**函数两个接口指针。 *客户端*是一个[**IDebugClient4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient4)接口， *pAnalysis*是一个[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)接口。 上述框架示例中的代码演示了如何获取另外两个接口指针。 `Client->QueryInterface` 获取[**IDebugControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)接口，`pAnalysis->GetDebugFATagControl` 获取**IDebugFAEntryTags**接口。

## <a name="span-idfailure-analysis-entries-tags-and-data-typesspanspan-idfailure_analysis_entries_tags_and_data_typesspanfailure-analysis-entries-tags-and-data-types"></a><span id="failure-analysis-entries-tags-and-data-types"></span><span id="FAILURE_ANALYSIS_ENTRIES_TAGS_AND_DATA_TYPES"></span>故障分析条目、标记和数据类型


分析引擎将创建一个[**DebugFailureAnalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)对象，以组织与特定代码失败有关的数据。 **DebugFailureAnalysis**对象具有一系列[失败分析条目](failure-analysis-entries.md)（fa 条目），其中每个条目都由一个**FA\_条目**结构表示。 分析扩展插件使用**IDebugFailureAnalysis2**接口来访问此 FA 项集合。 每个 FA 项都有一个标记，用于标识该项包含的信息的类型。 例如，FA 条目可能包含标记**DEBUG\_FLR\_错误检测\_代码**，这表明该条目包含 bug 检查代码。 标记是**DEBUG\_FLR\_PARAM\_类型**枚举中的值（在 extsfns 中定义），也称为**FA\_标记**枚举。

```cpp
typedef enum _DEBUG_FLR_PARAM_TYPE {
    ...
    DEBUG_FLR_BUGCHECK_CODE,
    ...
    DEBUG_FLR_BUILD_VERSION_STRING,
    ...
} DEBUG_FLR_PARAM_TYPE;

typedef DEBUG_FLR_PARAM_TYPE FA_TAG;
```

大多数[FA 条目](failure-analysis-entries.md)都具有关联的数据块。 **FA\_条目**结构的**DataSize**成员保存数据块的大小。 有些 FA 条目没有关联的数据块;所有信息都由标记传达。 在这些情况下， **DataSize**成员的值为0。

```cpp
typedef struct _FA_ENTRY
{
    FA_TAG Tag;
    USHORT FullSize;
    USHORT DataSize;
} FA_ENTRY, *PFA_ENTRY;
```

每个标记都有一组属性：例如，名称、说明和数据类型。 [**DebugFailureAnalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)对象与[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)对象关联，后者包含标记属性的集合。 下图说明了此关联。

![显示分析引擎、debugfailureanalysis 对象和 debugfailureanalysistags 对象的关系图](images/debugfa01.png)

[**DebugFailureAnalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)对象具有属于特定分析会话的[FA 条目](failure-analysis-entries.md)的集合。 关联的[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)对象具有标记属性的集合，这些属性仅包括该相同分析会话所使用的标记。 如前面的关系图所示，分析引擎具有一个全局标记表，其中包含有关分析会话通常可以使用的大量标记的信息。

分析会话使用的大多数标记通常是标准标记;也就是说，标记是[**FA\_标记**](https://docs.microsoft.com/previous-versions/jj991810(v=vs.85))枚举中的值。 不过，分析扩展插件可以创建自定义标记。 分析扩展插件可以将[FA 条目](failure-analysis-entries.md)添加到[**DebugFailureAnalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)对象，并为该条目指定自定义标记。 在这种情况下，自定义标记的属性将添加到关联的[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)对象中的标记属性集合。

可以通过 IDebugFAEntry 标记界面访问[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags) 。 若要获取指向 IDebugFAEntry 接口的指针，请调用[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)接口的[**GetDebugFATagControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nf-extsfns-idebugfailureanalysis2-getdebugfatagcontrol)方法。

每个标记都有一个数据类型属性，您可以通过检查该属性来确定失败分析条目中的数据的数据类型。 数据类型由**FA\_条目**中的值表示\_类型枚举。

下面的代码行获取**调试\_FLR\_生成\_版本\_字符串**标记的数据类型。 在这种情况下，数据类型为**DEBUG\_FA\_条目\_ANSI\_字符串**。 在代码中，`pAnalysis` 是指向[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)接口的指针。

```cpp
IDebugFAEntryTags* pTags = pAnalysis->GetDebugFATagControl(&pTags);

if(NULL != pTags)
{
   FA_ENTRY_TYPE entryType = pTags->GetType(DEBUG_FLR_BUILD_VERSION_STRING);
}
```

如果失败分析条目没有数据块，则关联标记的数据类型为**DEBUG\_FA\_条目\_不\_类型**。

回忆一下， [**DebugFailureAnalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)对象具有[FA 条目](failure-analysis-entries.md)的集合。 若要检查集合中的所有 FA 条目，请使用**NextEntry**方法。 下面的示例演示如何循环访问 FA 条目的整个集合。 假设*pAnalysis*是指向**IDebugFailureAnalysis2**接口的指针。 请注意，我们通过将**NULL**传递到**NextEntry**获取第一个条目。

```cpp
PFA_ENTRY entry = pAnalysis->NextEntry(NULL);

while(NULL != entry)
{
   // Do something with the entry

   entry = pAnalysis->NextEntry(entry);
}
```

标记可以有名称和说明。 在下面的代码中， *pAnalysis*是指向[**IDebugFailureAnalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)接口的指针， *pControl*是指向[**IDebugControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)接口的指针，`pTags` 是指向[IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)接口的指针。 此代码演示如何使用**GetProperties**方法获取与[FA 条目](failure-analysis-entries.md)关联的标记的名称和说明。

```cpp
#define MAX_NAME_LENGTH 64
#define MAX_DESCRIPTION_LENGTH 512

CHAR name[MAX_NAME_LENGTH] = {0};
ULONG nameSize = MAX_NAME_LENGTH;
CHAR desc[MAX_DESCRIPTION_LENGTH] = {0};
ULONG descSize = MAX_DESCRIPTION_LENGTH;
                  
PFA_ENTRY pEntry = pAnalysis->NextEntry(NULL); 
pTags->GetProperties(pEntry->Tag, name, &nameSize, desc, &descSize, NULL);
pControl->Output(DEBUG_OUTPUT_NORMAL, "The name is %s\n", name);
pControl->Output(DEBUG_OUTPUT_NORMAL, "The description is %s\n", desc);
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[编写自定义分析调试器扩展](writing-custom-analysis-debugger-extensions.md)

[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nc-extsfns-ext_analysis_plugin)

[分析扩展插件的元数据文件](metadata-files-for-analysis-extensions.md)

[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)

[IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)

 

 






