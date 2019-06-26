---
title: 分析扩展插件写入扩展分析
description: 可以通过编写一个分析的扩展插件来扩展分析调试器命令的功能。
ms.assetid: 7648F789-85D5-4247-90DD-2EAA43543483
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1e01ff9baa0f95fbb4091ced35ced4a59a9cae2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369413"
---
# <a name="writing-an-analysis-extension-plugin-to-extend-analyze"></a>分析扩展插件写入扩展 ！ 分析


可以扩展的功能[ **！ 分析**](-analyze.md)调试器命令通过编写一个分析的扩展插件。 通过提供分析扩展插件，您可以参与的 bug 检查或特定于组件或应用程序的方式中的异常的分析。

在编写分析扩展插件时，还可以编写描述要插件调用了的情况的元数据文件。 当[ **！ 分析**](-analyze.md)运行时，它查找、 加载和运行相应分析扩展插件。

编写一个分析的扩展插件，并使其可供[ **！ 分析**](-analyze.md)，请执行以下步骤。

-   创建导出的 DLL [  **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nc-extsfns-ext_analysis_plugin)函数。
-   创建具有与您的 DLL 和.alz 的扩展相同的名称的元数据文件。 例如，如果您的 DLL 名为 MyAnalyzer.dll，元数据文件必须命名为 MyAnalyzer.alz。 有关如何创建元数据文件的信息，请参阅[分析扩展的元数据文件](metadata-files-for-analysis-extensions.md)。 将元数据文件放在与 DLL 相同的目录中。
-   在调试器中，使用[ **.extpath** ](-extpath--set-extension-path-.md)命令，将你的目录添加到扩展的文件路径。 例如，如果 DLL 和元数据文件位于文件夹中名为 c:\\MyAnalyzer，输入命令 **.extpath + c:\\MyAnalyzer**。

当[ **！ 分析**](-analyze.md)命令在调试器中运行，则在.alz 扩展名的元数据文件的扩展文件路径中查找的分析引擎。 分析引擎读取元数据文件，以确定应加载哪个 analysis 扩展插件。 例如，假设分析引擎是否正在响应 Bug 检查 0xA IRQL\_不\_较少\_或\_相等，并且它读取名为 MyAnalyzer.alz 包含以下各项的元数据文件。

```text
PluginId       MyPlugin
DebuggeeClass  Kernel
BugCheckCode   0xA
BugCheckCode   0xE2
```

该条目`BugCheckCode  0x0A`指定此插件想要参与的 Bug 检查 0xA，分析，以便分析引擎加载 MyAnalyzer.dll （它必须是与 MyAnalyzer.alz 相同的目录中） 并调用其[  **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nc-extsfns-ext_analysis_plugin)函数。

**请注意**  元数据文件的最后一行必须结束换行字符。

 

## <a name="span-idskeletonexamplespanspan-idskeleton-examplespanspan-idskeletonexamplespanskeleton-example"></a><span id="Skeleton_Example"></span><span id="skeleton-example"></span><span id="SKELETON_EXAMPLE"></span>主干示例


下面是一个框架的示例，可以使用作为起始点。

1.  生成名为 MyAnalyzer.dll，可以将导出的 DLL [  **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nc-extsfns-ext_analysis_plugin)函数如下所示。

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

2.  创建一个名为 MyAnalyzer.alz 具有以下项的元数据文件。

    ```text
    PluginId      MyPlugin
    DebuggeeClass Kernel
    BugCheckCode  0xE2
    ```

    **请注意**  元数据文件的最后一行必须结束换行字符。

     

3.  建立主机和目标计算机之间的内核模式调试会话。

4.  在主机上放置 MyAnalyzer.dll 和 MyAnalyzer.alz 文件夹 c： 驱动器中\\MyAnalyzer。

5.  主机计算机上，在调试器中，输入以下命令。

    **.extpath + c:\\MyAnalyzer**

    **.crash**

6.  [ **.Crash** ](-crash--force-system-crash-.md)命令手动生成 Bug 检查 0xE2\_启动\_崩溃的目标计算机上，这将导致中断到调试器主机计算机上。 （在调试器中运行在主机上） 的 bug 检查分析引擎读取 MyAnalyzer.alz 并发现可以参与分析 bug 检查 0xE2 MyAnalyzer.dll。 这样的分析引擎加载 MyAnalyzer.dll 并调用其[  **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nc-extsfns-ext_analysis_plugin)函数。

    验证你看到类似于调试器中的以下输出。

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

上面的调试器输出显示了分析引擎，调用[  **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nc-extsfns-ext_analysis_plugin)函数四次： 一次用于分析的每个阶段。 分析引擎会将传递 **\_EFN\_分析**函数两个接口指针。 *客户端*是[ **IDebugClient4** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugclient4)接口，并且*pAnalysis*是[ **IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)接口。 在上面的主干示例代码演示如何获取更多的两个接口指针。 `Client->QueryInterface` 获取[ **IDebugControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugcontrol)接口，并且`pAnalysis->GetDebugFATagControl`获取**IDebugFAEntryTags**接口。

## <a name="span-idfailure-analysis-entries-tags-and-data-typesspanspan-idfailureanalysisentriestagsanddatatypesspanfailure-analysis-entries-tags-and-data-types"></a><span id="failure-analysis-entries-tags-and-data-types"></span><span id="FAILURE_ANALYSIS_ENTRIES_TAGS_AND_DATA_TYPES"></span>失败分析条目、 标记和数据类型


分析引擎就会创建[ **DebugFailureAnalysis** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)对象来组织的数据与特定代码失败。 一个**DebugFailureAnalysis**对象具有一系列[失败分析条目](failure-analysis-entries.md)（FA 的项），其中每个由表示**FA\_条目**结构. 分析扩展插件使用**IDebugFailureAnalysis2**接口，用于获取对此集合的 FA 条目的访问。 FA 的每个条目都有标识的项包含的信息的类型标记。 例如，FA 条目可能标记**调试\_FLR\_检测错误\_代码**，它将告诉我们的项包含错误检查代码。 标记是中的值**调试\_FLR\_PARAM\_类型**枚举 （extsfns.h 中定义），这也称为**FA\_标记**枚举。

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

大多数[FA 条目](failure-analysis-entries.md)有关联的数据块。 **DataSize**的成员**FA\_条目**结构保存的数据块大小。 某些 FA 条目没有关联的数据块;由标记传达的信息。 在这些情况下， **DataSize**成员的值为 0。

```cpp
typedef struct _FA_ENTRY
{
    FA_TAG Tag;
    USHORT FullSize;
    USHORT DataSize;
} FA_ENTRY, *PFA_ENTRY;
```

每个标记有一组属性： 例如，名称、 说明和数据类型。 一个[ **DebugFailureAnalysis** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)对象与之关联[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfaentrytags)对象，其中包含标记属性的集合。 下图说明了这种关联。

![显示的分析引擎、 debugfailureanalysis 对象和 debugfailureanalysistags 对象的关系图](images/debugfa01.png)

一个[ **DebugFailureAnalysis** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)对象具有一系列[FA 条目](failure-analysis-entries.md)，属于特定的分析会话。 关联[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfaentrytags)对象具有包括该相同的分析会话使用的标记的标记属性集合。 如上面的关系图所示，分析引擎具有全局标记表，保存有关大型组的标记，通常可通过分析会话使用的有限的信息。

通常由分析会话使用的标记的大多数都是标准标记;也就是说，标记是中的值[ **FA\_标记**](https://docs.microsoft.com/previous-versions/jj991810(v=vs.85))枚举。 但是，分析扩展插件可以创建自定义标记。 分析扩展插件可以添加[FA 条目](failure-analysis-entries.md)到[ **DebugFailureAnalysis** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)对象，并指定该条目的自定义标记。 在这种情况下，自定义标记的属性添加到关联的标记属性的集合[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfaentrytags)对象。

您可以访问[DebugFailureAnalysisTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfaentrytags)通过 IDebugFAEntry 标记接口。 若要获得到 IDebugFAEntry 接口的指针，调用[ **GetDebugFATagControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nf-extsfns-idebugfailureanalysis2-getdebugfatagcontrol)方法[ **IDebugFailureAnalysis2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)接口。

每个标记包含的数据类型可以检查以确定无法分析项中的数据的数据类型的属性。 中的值来表示数据类型**FA\_条目\_类型**枚举。

以下代码行获取的数据类型**调试\_FLR\_构建\_版本\_字符串**标记。 在这种情况下，数据类型是**调试\_FA\_条目\_ANSI\_字符串**。 在代码中，`pAnalysis`指向的指针[ **IDebugFailureAnalysis2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)接口。

```cpp
IDebugFAEntryTags* pTags = pAnalysis->GetDebugFATagControl(&pTags);

if(NULL != pTags)
{
   FA_ENTRY_TYPE entryType = pTags->GetType(DEBUG_FLR_BUILD_VERSION_STRING);
}
```

如果无法分析项没有数据块，相关联的标记的数据类型是**调试\_FA\_条目\_没有\_类型**。

请记住， [ **DebugFailureAnalysis** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)对象具有一系列[FA 条目](failure-analysis-entries.md)。 若要检查是否在集合中的所有 FA 条目，请使用**NextEntry**方法。 下面的示例演示如何循环访问的 FA 项的整个集合。 假定*pAnalysis*指向的指针**IDebugFailureAnalysis2**接口。 请注意，我们会通过将传递第一个条目**NULL**到**NextEntry**。

```cpp
PFA_ENTRY entry = pAnalysis->NextEntry(NULL);

while(NULL != entry)
{
   // Do something with the entry

   entry = pAnalysis->NextEntry(entry);
}
```

标记可以具有一个名称和说明。 在下面的代码中， *pAnalysis*指向的指针[ **IDebugFailureAnalysis** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)接口*pControl*是指向[**IDebugControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugcontrol)接口，并且`pTags`是一个指向[IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfaentrytags)接口。 该代码演示如何使用**GetProperties**方法以获取名称和描述与关联的标记[FA 条目](failure-analysis-entries.md)。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[编写自定义分析调试器扩展](writing-custom-analysis-debugger-extensions.md)

[ **\_EFN\_分析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nc-extsfns-ext_analysis_plugin)

[分析扩展插件的元数据文件](metadata-files-for-analysis-extensions.md)

[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)

[IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfaentrytags)

 

 






