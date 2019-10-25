---
title: 调试器数据模型 C++ 脚本
description: 本主题介绍如何使用调试器数据模型C++脚本来通过调试器引擎来支持自动化。
ms.date: 09/12/2019
ms.openlocfilehash: 01fc05ad1e38564ddc8bf3851e4ecb1a78995915
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837801"
---
# <a name="debugger-data-model-c-scripting"></a>调试器数据模型 C++ 脚本

本主题介绍如何使用调试器数据模型C++调试器数据模型C++脚本来通过使用脚本编写的调试器引擎来支持自动化。

## <a name="span-idscriptmanangement-script-management-in-the-debugger-data-model"></a>调试器数据模型中的 <span id="scriptmanangement"> 脚本管理 

除了作为对象创建和扩展性的中心权威的数据模型管理器角色以外，它还负责管理脚本的抽象概念。 从数据模型管理器的脚本管理器部分的角度来看，脚本是指可以动态加载、卸载并可能由提供程序调试的内容，以便扩展或向数据模型提供新的功能。 

脚本提供程序是一个组件，它将语言（例如： NatVis、JavaScript 等）桥接到数据模型。 它注册一个或多个文件扩展名（例如： "）。NatVis "，" .js "），由提供程序处理，使调试器客户端或用户接口允许通过委托将脚本文件委托给提供程序来加载该特定扩展。 

**核心脚本管理器： IDataModelScriptManager**

核心脚本管理器接口的定义如下。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptManager, IUnknown)
{
    STDMETHOD(GetDefaultNameBinder)(_COM_Outptr_ IDataModelNameBinder **ppNameBinder) PURE;
    STDMETHOD(RegisterScriptProvider)(_In_ IDataModelScriptProvider *provider) PURE;
    STDMETHOD(UnregisterScriptProvider)(_In_ IDataModelScriptProvider *provider) PURE;
    STDMETHOD(FindProviderForScriptType)(_In_ PCWSTR scriptType, _COM_Outptr_ IDataModelScriptProvider **provider) PURE;
    STDMETHOD(FindProviderForScriptExtension)(_In_ PCWSTR scriptExtension, _COM_Outptr_ IDataModelScriptProvider **provider) PURE;
    STDMETHOD(EnumerateScriptProviders)(_COM_Outptr_ IDataModelScriptProviderEnumerator **enumerator) PURE;
}
```

[GetDefaultNameBinder](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-getdefaultnamebinder)

GetDefaultNameBinder 方法返回数据模型的默认脚本名称联编程序。 名称联编程序是一个在对象的上下文中解析名称的组件。 例如，在给定表达式 "foo. bar" 的情况下，将调用名称联编程序解析对象 foo 上下文中的名称栏。 此处返回的联编程序遵循一组默认的数据模型规则。 脚本提供程序可以使用此联编程序跨提供程序提供名称解析的一致性。 


[RegisterScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-registerscriptprovider)

RegisterScriptProvider 方法通知数据模型存在一个新的脚本提供程序，该提供程序能够将新语言桥接到数据模型。 调用此方法时，脚本管理器会立即回叫给定的脚本提供程序，并查询它所管理的脚本的属性。 如果已在给定的脚本提供程序所指示的名称或文件扩展名下面注册了某个提供程序，则此方法将失败。 只有单个脚本提供程序可注册为特定名称或文件扩展名的处理程序。 


[UnregisterScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-unregisterscriptprovider)

UnregisterScriptProvider 方法撤消对 RegisterScriptProvider 方法的调用。 Inpassed 脚本提供程序提供的名称和文件扩展名将不再与其关联。 需要注意的是，即使在注销后，也可能对脚本提供程序有大量未完成的 COM 引用。 此方法仅阻止加载/创建给定脚本提供程序所管理的类型的脚本。 如果该提供程序加载的脚本仍在加载，或者已经操作了调试器（或数据模型）的对象模型，则这些操作可能仍具有返回到脚本的引用。 可能存在直接引用脚本中的构造的数据模型、方法或对象。 脚本提供程序必须准备好处理该提供程序。 


[FindProviderForScriptType](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-findproviderforscripttype)

FindProviderForScriptType 方法会在脚本管理器中搜索包含脚本类型字符串的提供程序，如此方法中所示。 如果找不到，则此方法将失败;否则，此类脚本提供程序将返回到调用方。 


[EnumerateScriptProviders](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-enumeratescriptproviders)

EnumerateScriptProviders 方法将返回一个枚举器，该枚举器将枚举通过先前对 RegisterScriptProvider 方法的调用向脚本管理器注册的每个脚本提供程序。 



**脚本提供程序枚举： IDataModelScriptProviderEnumerator**

EnumerateScriptProviders 方法将返回以下格式的枚举器：

```cpp 
DECLARE_INTERFACE_(IDataModelScriptProviderEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptProvider **provider) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptproviderenumerator-reset)

Reset 方法会将枚举器移动到在返回第一个元素之前的位置。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptproviderenumerator-getnext)

GetNext 方法将枚举器向前移动一个元素，并返回该元素处的脚本提供程序。 枚举器到达枚举的末尾时，将返回 E_BOUNDS。 收到此错误后，调用 GetNext 方法将继续无限期地返回 E_BOUNDS。 



## <a name="span-idhostinterfacesscript-debugger-data-model-c-host-interfaces-for-scripting"></a><span id="hostinterfacesscript"> 用于脚本编写C++的调试器数据模型主机接口

**宿主在脚本中的角色**

调试主机公开了一系列非常低的级别接口，用于了解其调试目标的类型系统的性质，用其调试目标的语言来计算表达式，等等 。通常情况下，它与脚本编写的更高级别构造不关心。 这种情况留给了整个调试器应用程序或提供这些功能的扩展。 但有一个例外。 任何想要参与数据模型提供的总体脚本编写体验的调试宿主都需要实现一些简单的接口，以便向脚本提供上下文。 实际上，调试宿主会控制它希望脚本环境在数据模型的命名空间中放置函数和其他脚本提供的功能的位置。 在此过程中，允许主机允许（或不）使用此类函数（例如）的表达式计算器。 此处所涉及的接口如下所示： 

接口 | 描述
|---------|------------|
IDebugHostScriptHost | 指示调试宿主要在脚本环境中参与的功能的接口。 此接口可用于创建上下文，用于通知脚本引擎放置对象的位置。
IDataModelScriptHostContext | 由脚本提供程序用作脚本内容的容器的宿主接口。 除了其对调试器应用程序的对象模型执行的操作之外，脚本表面的内容如何取决于特定的调试宿主。 此接口允许脚本提供程序获取有关内容放置位置的信息。 有关详细信息，请参阅本主题后面的[数据模型C++脚本接口](#scriptinterface)。


**调试宿主的脚本宿主： IDebugHostScriptHost**

IDebugHostScriptHost 接口是脚本提供程序为新创建的脚本从调试宿主获取上下文时使用的接口。 此上下文包含一个对象（由调试宿主提供），脚本提供程序可在其中将任何桥放到数据模型和脚本环境之间。 例如，此类桥可能是调用脚本函数的数据模型方法。 这样一来，数据模型端的调用方可以通过 IModelMethod 接口上的调用方法来调用脚本方法。 

IDebugHostScriptHost 接口的定义如下。 

```cpp
DECLARE_INTERFACE_(IDebugHostScriptHost, IUnknown)
{
    STDMETHOD(CreateContext)(_In_ IDataModelScript* script, _COM_Outptr_ IDataModelScriptHostContext** scriptContext) PURE;
}
```

[CreateContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostscripthost-createcontext)

脚本提供程序调用 CreateContext 方法来创建新的上下文，以便在其中放置脚本的内容。 此类上下文由 "数据模型C++脚本接口" 页上详细描述的 IDataModelScriptHostContext 接口表示。 


## <a name="span-idscriptinterface-debugger-data-model-c-scripting-interfaces"></a><span id="scriptinterface"> 调试程序数据C++模型脚本接口

**脚本和脚本接口**

数据模型的总体体系结构允许第三方定义数据模型的某些语言和对象模型之间的桥梁。 通常，要桥接的语言是一种脚本语言，因为数据模型的环境是非常动态的。 在语言和数据模型的对象模型之间定义并实现此桥梁的组件称为脚本提供程序。 初始化后，脚本提供程序会向数据模型管理器的脚本管理器部分注册自身，管理扩展性的任何接口将随后允许编辑、加载、卸载和可能调试脚本写入脚本提供程序管理的语言。 

请注意，适用于 Windows 的调试工具目前定义了两个脚本提供程序。

- NatVis 提供程序。 此提供程序嵌入在 DbgEng 和 NatVis XML 和数据模型之间，允许对本机/语言数据类型进行可视化。
- JavaScript 提供程序。 此提供程序包含在旧版调试器扩展中： JsProvider。 它在用 JavaScript 语言和数据模型编写的脚本之间进行桥梁，允许任意形式的调试器控制和扩展性。

可以编写新的提供程序，以便将其他语言（例如： Python 等）与数据模型进行联系。 这种方法目前封装在旧版调试器扩展中用于加载。 脚本提供程序本身应该尽量减少与旧引擎接口的依赖关系，并且应尽可能地使用数据模型 Api。 这样，就可以轻松地将提供程序迁移到其他环境。

有两类与脚本提供程序相关的接口。 接口的第一类用于常规管理脚本提供程序及其管理的脚本。 第二类接口用于支持脚本调试。 虽然对第一个集的支持是必需的，但第二个支持是可选的，并且对于每个提供程序可能没有意义。 


常规管理接口包括： 

接口 | 描述
|---------|------------|
IDataModelScriptProvider | 脚本提供程序必须实现的核心接口。 这是向数据模型管理器的脚本管理器部分注册的接口，以便播发提供程序对特定类型脚本的支持并针对特定文件扩展名进行注册
IDataModelScript | 由提供程序管理的特定脚本的抽象。 加载或编辑的每个脚本都有单独的 IDataModelScript 实例
IDataModelScriptClient | 脚本提供程序用于向用户界面传递信息的客户端接口。 脚本提供程序不实现此接口。 承载需要使用脚本提供程序的数据模型的应用程序。 脚本提供程序将调用脚本客户端的方法来报告状态、错误，等等 。
IDataModelScriptHostContext | 由脚本提供程序用作脚本内容的容器的宿主接口。 除了其对调试器应用程序的对象模型执行的操作之外，脚本表面的内容如何取决于特定的调试宿主。 此接口允许脚本提供程序获取有关内容放置位置的信息。
IDataModelScriptTemplate | 脚本提供程序可以提供一个或多个模板，用作用户编写脚本的起点。 提供内置编辑器的调试器应用程序可以 prefill 通过此接口提供的提供程序公布的模板内容的新脚本。
IDataModelScriptTemplateEnumerator | 脚本提供程序实现的一个枚举器接口，用于公布它所支持的所有各种模板。
IDataModelNameBinder | 名称联编程序-一个对象，可将上下文中的名称与值相关联。 对于给定的表达式（如 "foo"），名称联编程序能够在对象 "foo" 的上下文中绑定名称 "bar"，并生成一个值或对它的引用。 名称联编程序通常不由脚本提供程序实现;相反，可以从数据模型中获取默认联编程序，并使用脚本提供程序

调试接口包括： 

接口 | 描述
|---------|------------|
IDataModelScriptDebug | 为了使脚本可调试，脚本提供程序必须提供的核心接口。 如果脚本是可调试的，则 IDataModelScript 接口的实现类必须用于 IDataModelScriptDebug 的 QueryInterface。
IDataModelScriptDebugClient | 希望提供脚本调试功能的用户界面实现了 IDataModelScriptDebugClient 接口。 脚本提供程序利用此接口来回传递调试信息（例如：发生的事件、断点等）
IDataModelScriptDebugStack | 脚本提供程序实现此接口，以便向脚本调试器公开调用堆栈的概念。
IDataModelScriptDebugStackFrame | 脚本提供程序实现此接口，以公开调用堆栈中特定堆栈帧的概念。
IDataModelScriptDebugVariableSetEnumerator | 脚本提供程序实现此接口以公开一组变量。 此集可以表示函数的参数集、本地变量集或特定范围内的变量集。 具体含义取决于获取接口的方式。
IDataModelScriptDebugBreakpoint | 脚本提供程序实现此接口，以公开脚本中特定断点的概念和控制。
IDataModelScriptDebugBreakpointEnumerator | 脚本提供程序实现此以枚举脚本中当前存在的所有断点（无论是否已启用）。

**核心脚本提供程序： IDataModelScriptProvider**

任何希望作为脚本提供程序的扩展都必须提供 IDataModelScriptProvider 接口的实现，并通过 RegisterScriptProvider 方法将其注册到数据模型管理器的脚本管理器部分。 必须实现的核心接口定义如下。

```cpp 
DECLARE_INTERFACE_(IDataModelScriptProvider, IUnknown)
{
    STDMETHOD(GetName)(_Out_ BSTR *name) PURE;
    STDMETHOD(GetExtension)(_Out_ BSTR *extension) PURE;
    STDMETHOD(CreateScript)(_COM_Outptr_ IDataModelScript **script) PURE;
    STDMETHOD(GetDefaultTemplateContent)(_COM_Outptr_ IDataModelScriptTemplate **templateContent) PURE;
    STDMETHOD(EnumerateTemplates)(_COM_Outptr_ IDataModelScriptTemplateEnumerator **enumerator) PURE;
}
```

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getname)

GetName 方法返回提供程序管理的脚本类型（或语言）的名称，该脚本通过 SysAllocString 方法进行分配。 调用方负责通过 SysFreeString 释放返回的字符串。 此方法可能返回的字符串的示例有 "JavaScript" 或 "NatVis"。 返回的字符串可能出现在承载数据模型的调试器应用程序的用户界面中。 不能有两个脚本提供程序返回相同的名称（不区分大小写）。 

[Path.getextension 对](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getextension)

Path.getextension 对方法返回此提供程序管理的脚本的文件扩展名（不带点）作为通过 SysAllocString 方法分配的字符串。 承载数据模型（具有脚本支持）的调试器应用程序将通过此扩展将脚本文件打开委托给脚本提供程序。 调用方负责通过 SysFreeString 释放返回的字符串。 此方法可能返回的字符串示例为 "js" 或 "NatVis"。 

[CreateScript](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-createscript)

调用 CreateScript 方法来创建新脚本。 每当调用此方法时，脚本提供程序都必须返回返回的 IDataModelScript 接口所表示的新的空脚本。 请注意，无论用户界面是创建新的空白脚本以供用户编辑，还是调试器应用程序从磁盘加载脚本，都将调用此方法。 提供程序不涉及文件 i/o。 它仅通过传递给 IDataModelScript 上方法的流处理来自宿主应用程序的请求。 

[GetDefaultTemplateContent](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getdefaulttemplatecontent)

GetDefaultTemplateContent 方法返回提供程序的默认模板内容的接口。 这是脚本提供程序要在编辑窗口中为新创建的脚本预先填充的内容。 如果脚本提供程序没有模板（或者没有指定为默认内容的模板内容），则脚本提供程序可能会从此方法返回 E_NOTIMPL。 

[EnumerateTemplates](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-enumeratetemplates)

EnumerateTemplates 方法返回一个枚举器，该枚举器能够枚举脚本提供程序提供的各种模板。 模板内容是在创建新脚本时，脚本提供程序要 "预先填充" 到编辑窗口中的内容。 如果支持多个不同的模板，则可以命名这些模板（例如： "命令性脚本"、"扩展脚本"），托管数据模型的调试器应用程序可以选择如何向用户显示 "模板"。 


**核心脚本接口： IDataModelScript**

管理提供程序所实现的单个脚本的主接口是 IDataModelScript 接口。 当客户端希望创建新的空白脚本并对 IDataModelScriptProvider 调用 CreateScript 方法时，将返回实现此接口的组件。 

由提供程序创建的每个脚本都应在独立的接收器中。 除了通过数据模型与外部对象进行显式交互外，一个脚本应该不能影响另一个脚本。 例如，两个脚本都可以扩展某些类型或概念（例如：调试器对进程的概念）。 然后，这两个脚本都可以通过外部进程对象访问每个字段的字段。 

接口按如下方式定义。 

```cpp
DECLARE_INTERFACE_(IDataModelScript, IUnknown)
{
    STDMETHOD(GetName)(_Out_ BSTR *scriptName) PURE;
    STDMETHOD(Rename)(_In_ PCWSTR scriptName) PURE;
    STDMETHOD(Populate)(_In_ IStream *contentStream) PURE;
    STDMETHOD(Execute)(_In_ IDataModelScriptClient *client) PURE;
    STDMETHOD(Unlink)() PURE;
    STDMETHOD(IsInvocable)(_Out_ bool *isInvocable) PURE;
    STDMETHOD(InvokeMain)(_In_ IDataModelScriptClient *client) PURE; 
}
```

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-getname)

GetName 方法通过 SysAllocString 函数将脚本的名称作为分配的字符串返回。 如果脚本尚不具有名称，则该方法应返回 null BSTR。 在这种情况下，它不会失败。 如果脚本通过调用 Rename 方法进行显式重命名，则 GetName 方法应返回新分配的名称。 

[重命名](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-rename)

Rename 方法为脚本分配新名称。 脚本实现负责保存此名称，并在调用 GetName 方法时将其返回。 当用户界面选择将作为脚本保存到新名称时，通常会调用此。 请注意，重命名该脚本可能会影响宿主应用程序选择用于投影脚本内容的位置。 

[放置](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-populate)

填充方法由客户端调用，以更改或同步脚本的 "内容"。 这是对脚本提供程序发出的、脚本代码已更改的通知。 需要注意的是，此方法不会导致脚本的执行或对脚本操作的任何对象进行更改。 这只是一个向脚本提供程序发出的通知，指出脚本的内容已更改，以便它可以同步自己的内部状态。 

[运行](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-execute)

Execute 方法执行最后一次成功填充调用时所指示的脚本内容，并根据该内容修改调试器的对象模型。 如果语言（或脚本提供程序）定义了一个 "main function"，则在执行操作过程中，如果在用户界面中单击虚部 "执行脚本" 按钮，则会调用该作者。 执行操作可视为只执行初始化和对象模型操作（例如：执行根代码和设置扩展点）。 

[Unlink](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-unlink)

取消链接方法会撤消执行操作。 在脚本执行过程中建立的任何对象模型操作或扩展点都将撤消。 取消链接操作后，该脚本可以通过调用 Execute 重新执行，也可以被释放。 

[IsInvocable](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-isinvocable)

IsInvocable 方法将返回脚本是否为 invocable，即它是否有 "main 函数" （由其语言或提供程序定义）。 如果在用户界面中按了虚部 "执行脚本" 按钮，此类 "main 函数" 将从概念上讲是要调用的脚本作者。 

[InvokeMain](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscript-invokemain)

如果脚本的 "main 函数" 旨在通过 UI 调用执行，则它会通过 IsInvocable 方法的真正返回来指示这种情况。 然后，用户界面可以调用 InvokeMain 方法来实际 "调用" 该脚本。 请注意，这不同于*执行*，后者运行所有根代码，并将脚本桥接到基础主机的命名空间。 


\* * 脚本客户端： IDataModelScriptClient * *

一种应用程序，该应用程序承载的数据模型需要管理脚本，并具有围绕此概念的用户界面（无论是图形还是控制台）来实现 IDataModelScriptClient 接口。 此接口将在执行或调用期间传递给任何脚本提供程序，或通过脚本传递回用户界面。 

IDataModelScriptClient 接口的定义如下。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptClient, IUnknown)
{
   STDMETHOD(ReportError)(_In_ ErrorClass errClass, _In_ HRESULT hrFail, _In_opt_ PCWSTR message, _In_ ULONG line, _In_ ULONG position) PURE;
}
```

[ReportError](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptclient-reporterror)

如果在执行或调用脚本的过程中出现错误，则脚本提供程序将调用 ReportError 方法以通知用户界面错误。 


**脚本的宿主上下文： IDataModelScriptHostContext**

调试宿主对数据模型脚本内容的投影方式和位置有一定的影响。 预计每个脚本都要求主机提供要在其中将桥放到脚本的上下文（例如：可以调用的函数对象等）。通过调用 IDebugHostScriptHost 上的 CreateContext 方法并获取 IDataModelScriptHostContext 来检索此上下文。 

IDataModelScriptHostContext 接口的定义如下。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptHostContext, IUnknown)
{
   STDMETHOD(NotifyScriptChange)(_In_ IDataModelScript* script, _In_ ScriptChangeKind changeKind) PURE;
   STDMETHOD(GetNamespaceObject)(_COM_Outptr_ IModelObject** namespaceObject) PURE;
}
```

[NotifyScriptChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripthostcontext-notifyscriptchange)

需要脚本提供程序在对关联上下文调用 NotifyScriptChange 方法时，通知调试宿主发生的某些操作。 此类操作定义为 ScriptChangeKind 枚举的成员

[GetNamespaceObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripthostcontext-getnamespaceobject)

GetNamespaceObject 方法返回一个对象，在该对象中，脚本提供程序可以在数据模型和脚本之间放置任何桥梁。 例如，在此示例中，脚本提供程序可能会将数据模型方法对象（装箱到 IModelObject 中的 IModelMethod 接口）放入其实现在脚本中相应命名的函数。 


**新创建脚本的模板： IDataModelScriptTemplate**

需要提供一个或多个脚本模板的脚本提供程序（例如：为了帮助用户在调试器用户界面中编写脚本，从而帮助用户在调试器用户界面中编写脚本）。 此类模板是实现 IDataModelScriptTemplate 接口的组件，可通过脚本提供程序上的 GetDefaultTemplate 方法或 EnumerateTemplates 方法返回。 

IDataModelScriptTemplate 接口的定义如下。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptTemplate, IUnknown)
{
   STDMETHOD(GetName)(_Out_ BSTR *templateName) PURE;
   STDMETHOD(GetDescription)(_Out_ BSTR *templateDescription) PURE;
   STDMETHOD(GetContent)(_COM_Outptr_ IStream **contentStream) PURE;
}
```


[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getname)

GetName 方法返回模板的名称。 如果模板没有名称，这可能会失败，并出现 E_NOTIMPL。 单个默认模板（如果存在）不需要具有名称。 所有其他模板为。 这些名称可以作为菜单的一部分显示在用户界面中，以选择要创建的模板。 


[GetDescription](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getdescription)

GetDescription 方法将返回该模板的说明。 此类描述将在更具描述性的界面中向用户显示，以帮助用户了解模板的设计内容。 如果模板没有说明，则该模板可能会从该方法返回 E_NOTIMPL。 

[GetContent](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getcontent)

GetContent 方法返回模板的内容（或代码）。 如果用户选择从该模板创建新的脚本，则会将其预填充到 "编辑" 窗口中。 该模板负责创建（并返回）客户端可以请求的内容的标准流。 

**枚举提供程序的模板内容： IDataModelScriptTemplateEnumerator**

脚本提供程序可以提供一个或多个模板，用于在某些用户界面中将内容预先填充到新创建的脚本中。 如果提供了这些模板中的任何一个，则脚本提供程序必须对其实现枚举器，以便在调用 EnumerateTemplates 方法时返回这些模板。 

此类枚举器是 IDataModelScriptTemplateEnumerator 接口的实现，按如下所示定义。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptTemplateEnumerator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptTemplate **templateContent) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplateenumerator-reset)

Reset 方法会将枚举数重置为第一次创建时所处的位置（在生成第一个模板之前）。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscripttemplateenumerator-getnext)

GetNext 方法将枚举器移动到下一个模板并返回它。 枚举结束时，枚举器返回 E_BOUNDS。 命中 E_BOUNDS 标记后，枚举器将持续产生 E_BOUNDS 错误，直到进行重置调用。 


**解析名称的含义： IDataModelNameBinder**

数据模型为脚本提供程序提供了一种标准方式，用于在给定的上下文（例如：确定将跨各种脚本提供程序操作的 bar）中确定给定名称的含义。 此机制称为 "名称" 联编程序，由 IDataModelNameBinder 接口表示。 此类联编程序封装了有关名称解析方式的一组规则，以及如何处理在对象上多次定义了名称的冲突解决方法。 这些规则中的一部分包括诸如如何根据本地名称（在要调试的语言的类型系统中为一个名称）解析投影名称（由数据模型添加的名称）。 

为了在脚本提供程序之间提供一定程度的一致性，数据模型的脚本管理器提供了一个默认名称联编程序。 可以通过调用 IDataModelScriptManager 接口上的 GetDefaultNameBinder 方法获取此默认名称联编程序。 名称联编程序接口的定义如下。 

```cpp
DECLARE_INTERFACE_(IDataModelNameBinder, IUnknown)
{
   STDMETHOD(BindValue)(_In_ IModelObject* contextObject, _In_ PCWSTR name, _COM_Errorptr_ IModelObject** value, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(BindReference)(_In_ IModelObject* contextObject, _In_ PCWSTR name, _COM_Errorptr_ IModelObject** reference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(EnumerateValues)(_In_ IModelObject* contextObject, _COM_Outptr_ IKeyEnumerator** enumerator) PURE;
   STDMETHOD(EnumerateReferences)(_In_ IModelObject* contextObject, _COM_Outptr_ IKeyEnumerator** enumerator) PURE;
}
```

[BindValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelnamebinder-bindvalue)

BindValue 方法根据一组绑定规则，对给定的对象执行等效的 contextObject.name。 此绑定的结果是一个值。 作为值，基础脚本提供程序不能使用值来将赋值返回到名称。

[BindReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelnamebinder-bindreference)

BindReference 方法类似于 BindValue，因为它还会根据一组绑定规则对给定的对象执行等效的操作。 但是，从此方法进行绑定的结果是引用而不是值。 作为参考，脚本提供程序可以利用该引用将赋值回给名称。 

[EnumerateValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelnamebinder-enumeratevalues)

EnumerateValues 方法根据 BindValue 方法的规则枚举名称和值的集合，这些名称和值将根据对象进行绑定。 不同于 IModelObject 上的 EnumerateKeys、EnumerateValues 和类似方法，这些方法可能返回具有相同值的多个名称（对于基类、父模型和类似），此枚举器将仅返回将绑定到的特定名称集BindValue 和 BindReference。 名称永远不会重复。 请注意，通过名称联编程序枚举对象比调用 IModelObject 方法要高得多。 

[EnumerateReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelnamebinder-enumeratereferences)

EnumerateReferences 方法枚举名称和对它们的引用集，这些名称和引用将根据 BindReference 方法的规则绑定到对象。 不同于 IModelObject 上的 EnumerateKeys、EnumerateValues 和类似方法，这些方法可能返回具有相同值的多个名称（对于基类、父模型和类似），此枚举器将仅返回将绑定到的特定名称集BindValue 和 BindReference。 名称永远不会重复。 请注意，通过名称联编程序枚举对象比调用 IModelObject 方法要高得多。 


## <a name="span-iddebugscript-debugger-data-model-c-script-debugging-interfaces"></a><span id="debugscript"> 调试器数据模型C++脚本调试接口

数据模型中脚本提供程序的基础结构还提供了有关调试脚本的概念。 任何想要向调试宿主和宿主数据模型的调试器应用程序公开调试功能的脚本都可以通过使用 IDataModelScript 接口来实现 IDataModelScriptDebug 接口，来实现此目的。 此脚本在脚本中的状态向基础结构指出它是可调试的。 

尽管 IDataModelScriptDebug 接口是获取对脚本提供程序的调试功能的访问权限，但它是通过提供整体调试功能的一组其他接口加入的。 

调试接口包括： 

接口 | 描述
|---------|------------|
IDataModelScriptDebug | 为了使脚本可调试，脚本提供程序必须提供的核心接口。 如果脚本是可调试的，则 IDataModelScript 接口的实现类必须用于 IDataModelScriptDebug 的 QueryInterface。
IDataModelScriptDebugClient | 希望提供脚本调试功能的用户界面实现了 IDataModelScriptDebugClient 接口。 脚本提供程序利用此接口来回传递调试信息（例如：发生的事件、断点等）
IDataModelScriptDebugStack | 脚本提供程序实现此接口，以便向脚本调试器公开调用堆栈的概念。
IDataModelScriptDebugStackFrame | 脚本提供程序实现此接口，以公开调用堆栈中特定堆栈帧的概念。
IDataModelScriptDebugVariableSetEnumerator | 脚本提供程序实现此接口以公开一组变量。 此集可以表示函数的参数集、本地变量集或特定范围内的变量集。 具体含义取决于获取接口的方式。
IDataModelScriptDebugBreakpoint | 脚本提供程序实现此接口，以公开脚本中特定断点的概念和控制。
IDataModelScriptDebugBreakpointEnumerator | 脚本提供程序实现此以枚举脚本中当前存在的所有断点（无论是否已启用）。

常规管理接口包括： 

接口 | 描述
|---------|------------|
IDataModelScriptProvider | 脚本提供程序必须实现的核心接口。 这是向数据模型管理器的脚本管理器部分注册的接口，以便播发提供程序对特定类型脚本的支持并针对特定文件扩展名进行注册
IDataModelScript | 由提供程序管理的特定脚本的抽象。 加载或编辑的每个脚本都有单独的 IDataModelScript 实例
IDataModelScriptClient | 脚本提供程序用于向用户界面传递信息的客户端接口。 脚本提供程序不实现此接口。 承载需要使用脚本提供程序的数据模型的应用程序。 脚本提供程序将调用脚本客户端的方法来报告状态、错误，等等 。
IDataModelScriptHostContext | 由脚本提供程序用作脚本内容的容器的宿主接口。 除了其对调试器应用程序的对象模型执行的操作之外，脚本表面的内容如何取决于特定的调试宿主。 此接口允许脚本提供程序获取有关内容放置位置的信息。
IDataModelScriptTemplate | 脚本提供程序可以提供一个或多个模板，用作用户编写脚本的起点。 提供内置编辑器的调试器应用程序可以 prefill 通过此接口提供的提供程序公布的模板内容的新脚本。
IDataModelScriptTemplateEnumerator | 脚本提供程序实现的一个枚举器接口，用于公布它所支持的所有各种模板。
IDataModelNameBinder | 名称联编程序-一个对象，可将上下文中的名称与值相关联。 对于给定的表达式（如 "foo"），名称联编程序能够在对象 "foo" 的上下文中绑定名称 "bar"，并生成一个值或对它的引用。 名称联编程序通常不由脚本提供程序实现;相反，可以从数据模型中获取默认联编程序，并由脚本提供程序使用。


**使脚本可调试： IDataModelScriptDebug**

任何可调试的脚本通过在实现 IDataModelScript 的同一组件上存在 IDataModelScriptDebug 接口来指示此功能。 调试宿主或宿主数据模型的调试器应用程序对此接口的查询是指调试功能的状态。 

IDataModelScriptDebug 接口的定义如下。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebug, IUnknown)
{
   STDMETHOD_(ScriptDebugState, GetDebugState)() PURE;
   STDMETHOD(GetCurrentPosition)(_Out_ ScriptDebugPosition *currentPosition, _Out_opt_ ScriptDebugPosition *positionSpanEnd, _Out_opt_ BSTR *lineText) PURE;
   STDMETHOD(GetStack)(_COM_Outptr_ IDataModelScriptDebugStack **stack) PURE;
   STDMETHOD(SetBreakpoint)(_In_ ULONG linePosition, _In_ ULONG columnPosition, _COM_Outptr_ IDataModelScriptDebugBreakpoint **breakpoint) PURE;
   STDMETHOD(FindBreakpointById)(_In_ ULONG64 breakpointId, _COM_Outptr_ IDataModelScriptDebugBreakpoint **breakpoint) PURE;
   STDMETHOD(EnumerateBreakpoints)(_COM_Outptr_ IDataModelScriptDebugBreakpointEnumerator **breakpointEnum) PURE;
   STDMETHOD(GetEventFilter)(_In_ ScriptDebugEventFilter eventFilter, _Out_ bool *isBreakEnabled) PURE;
   STDMETHOD(SetEventFilter)(_In_ ScriptDebugEventFilter eventFilter, _In_ bool isBreakEnabled) PURE;
   STDMETHOD(StartDebugging)(_In_ IDataModelScriptDebugClient *debugClient) PURE;
   STDMETHOD(StopDebugging)(_In_ IDataModelScriptDebugClient *debugClient) PURE;
}
```

[GetDebugState](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getdebugstate)

GetDebugState 方法返回脚本的当前状态（例如：是否正在执行）。 状态由 ScriptDebugState 枚举中的值定义。

[GetCurrentPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getcurrentposition)

GetCurrentPosition "方法返回脚本内的当前位置。 只有在将脚本分解到调试器中时，才会调用此方法，在这种情况下，对 GetScriptState 的调用将返回 ScriptDebugBreak。 对此方法的任何其他调用都无效，将失败。 

[GetStack](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getstack)

GetStack 方法获取中断位置的当前调用堆栈。 只有在将脚本分解到调试器时，才能调用此方法。 

[SetBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-setbreakpoint)

SetBreakpoint 方法在脚本中设置断点。 请注意，实现可自由调整 inpassed 行和列位置，使其前进到适当的代码位置。 在返回的 IDataModelScriptDebugBreakpoint 接口上，方法调用可以检索放置断点的实际行号和列号。 

[FindBreakpointById](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-findbreakpointbyid)

通过 SetBreakpoint 方法在脚本内创建的每个断点都是由实现指定的唯一标识符（64位无符号整数）。 FindBreakpointById 方法用于从给定标识符获取断点接口。 

[EnumerateBreakpoints](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-enumeratebreakpoints)

EnumerateBreakpoints 方法返回一个枚举器，该枚举器可枚举在特定脚本中设置的每个断点。 

[GetEventFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-geteventfilter)

GetEventFilter 方法返回是否对特定事件启用 "事件中断"。 可能导致 "事件中断" 的事件由 ScriptDebugEventFilter 枚举的成员描述。 

[SetEventFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-seteventfilter)

SetEventFilter 方法为 ScriptDebugEventFilter 枚举的成员定义的特定事件更改 "事件中断" 行为。 可在 GetEventFilter 方法的文档中找到可用事件（以及此枚举的说明）的完整列表。 

[StartDebugging](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-startdebugging)

StartDebugging 方法 "打开" 特定脚本的调试器。 启动调试的操作不会主动导致执行中断或单步执行。 它只是使脚本可调试，并为客户端提供一组用于与调试接口进行通信的接口。 

["](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-stopdebugging)

"方法由要停止调试的客户端调用。 此方法调用可在 StartDebugging 成功完成之后的任何时间点（例如：在中断过程中，脚本执行时，等等 ...）。调用会立即停止所有调试活动，并在调用 StartDebugging 之前将状态重置回。 


**调试接口： IDataModelScriptDebugClient**

需要为脚本调试提供接口的调试宿主或调试器应用程序必须通过的调试接口上的 StartDebugging 方法为脚本调试器提供 IDataModelScriptDebugClient 接口的实现脚本. 

IDataModelScriptDebugClient 是通过其传递调试事件的通信通道，控制从脚本执行引擎到调试器接口。 定义方式如下： 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugClient, IUnknown)
{
   STDMETHOD(NotifyDebugEvent)(_In_ ScriptDebugEventInformation *pEventInfo, _In_ IDataModelScript *pScript, _In_opt_ IModelObject *pEventDataObject, _Inout_ ScriptExecutionKind *resumeEventKind) PURE;
}
```

[NotifyDebugEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugclient-notifydebugevent)

每当发生中断脚本调试器的事件时，调试代码本身就会通过 NotifyDebugEvent 方法调用接口。 此方法是同步的。 在接口从事件返回之前，不会继续执行脚本。 脚本调试器的定义非常简单：绝对不需要处理的嵌套事件。 调试事件由称为 ScriptDebugEventInformation 的变量记录定义。 事件信息中的哪些字段有效很大程度上由 DebugEvent 成员定义。 它定义发生的事件类型，如 ScriptDebugEvent 枚举的成员所述。

**调用堆栈： IDataModelScriptDebugStack**

当发生会中断到脚本调试器中的事件时，调试接口将需要检索中断位置的调用堆栈。 这是通过 GetStack 方法完成的。 此类堆栈通过 IDataModelScriptDebugStack 定义，如下所示。 

请注意，整个堆栈可能跨越多个脚本和/或多个脚本提供程序。 在特定脚本的调试接口上对 GetStack 方法的单个调用返回的调用堆栈只应在该脚本的边界内返回调用堆栈的段。 如果同一个提供程序的两个脚本交互，则脚本调试引擎可以将调用堆栈检索为跨越多个脚本上下文。 GetStack 方法不应返回堆栈中位于另一个脚本中的部分。 相反，如果可以检测到这种情况，则将堆栈帧作为脚本的边界框架应通过在该堆栈帧上的 IsTransitionPoint 和 GetTransition 方法的实现将其标记为转换框架。 调试器接口应将整个堆栈与存在的多个堆栈段组合在一起。 

转换是以这种方式实现的，调试接口可能会将有关本地变量、参数、断点和其他脚本特定构造的查询定向到错误的脚本上下文！ 这将导致调试器界面中出现未定义的行为。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugStack, IUnknown)
{
   STDMETHOD_(ULONG64, GetFrameCount)() PURE;
   STDMETHOD(GetStackFrame)(_In_ ULONG64 frameNumber, _COM_Outptr_ IDataModelScriptDebugStackFrame **stackFrame) PURE;
}
```

[GetFrameCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstack-getframecount)

GetFrameCount 方法返回调用堆栈的此段中堆栈帧的数目。 如果提供程序可以在不同的脚本上下文或不同的提供程序中检测帧，则它应通过将进入帧上的 IsTransitionPoint 和 GetTransition 方法实现到此堆栈段来向调用方指示这一点。 

[GetStackFrame](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstack-getstackframe)

GetStackFrame 从堆栈段获取特定堆栈帧。 调用堆栈具有从零开始的索引系统：发生 break 事件的当前堆栈帧为帧0。 当前方法的调用方为帧1（等等）。 


**中断时检查状态： IDataModelScriptDebugStackFrame**

可以通过调用 IDataModelScriptDebugStack 接口上的 GetStackFrame 方法（表示发生中断的堆栈段）来检索进入脚本调试程序时调用堆栈的特定帧。 返回以表示此帧的 IDataModelScriptDebugStackFrame 接口的定义如下。

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugStackFrame, IUnknown)
{
   STDMETHOD(GetName)(_Out_ BSTR *name) PURE;
   STDMETHOD(GetPosition)(_Out_ ScriptDebugPosition *position, _Out_opt_ ScriptDebugPosition *positionSpanEnd, _Out_opt_ BSTR *lineText) PURE;
   STDMETHOD(IsTransitionPoint)(_Out_ bool *isTransitionPoint) PURE;
   STDMETHOD(GetTransition)(_COM_Outptr_ IDataModelScript **transitionScript, _Out_ bool *isTransitionContiguous) PURE;
   STDMETHOD(Evaluate)(_In_ PCWSTR pwszExpression, _COM_Outptr_ IModelObject **ppResult) PURE;
   STDMETHOD(EnumerateLocals)(_COM_Outptr_ IDataModelScriptDebugVariableSetEnumerator **variablesEnum) PURE;
   STDMETHOD(EnumerateArguments)(_COM_Outptr_ IDataModelScriptDebugVariableSetEnumerator **variablesEnum) PURE;
}
```

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-getname)

GetName 方法返回此帧的显示名称（例如：函数名称）。 此类名称将在堆栈 backtrace 中显示，并显示给用户。 

[GetPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-getposition)

GetPosition 方法返回脚本内堆栈帧所表示的位置。 仅当脚本位于包含此帧的堆栈所表示的断点内时，才能调用此方法。 始终返回此帧中的行和列位置。 如果调试器能够返回脚本内的 "执行位置" 范围，则可以在 positionSpanEnd 参数中返回结束位置。 如果调试器无法做到这一点，则跨度结束（如果需要）中的行和列值应设置为零。 

[IsTransitionPoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-istransitionpoint)

IDataModelScriptDebugStack 接口表示调用堆栈的一段，这部分调用堆栈包含在一个脚本的上下文中。 如果调试器能够检测从一个脚本到另一个脚本（或一个脚本提供程序）的转换，则可以通过实现 IsTransitionPoint 方法并根据需要返回 true 或 false 来指示这一点。 输入应用段的脚本的调用堆栈帧应视为转换点。 不是所有其他帧。 

[GetTransition](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-gettransition)

如果给定堆栈帧是由 IsTransition 方法确定的转换点（有关转换点的定义，请参阅此处的文档），GetTransition 方法将返回有关该转换的信息。 具体而言，此方法返回上一个脚本，即调用包含此 IDataModelScriptDebugStackFrame 的堆栈段所代表的脚本。 

[诂](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-evaluate)

求值方法在调用此方法的 IDataModelScriptDebugStackFrame 接口所表示的堆栈帧的上下文中计算表达式（这是脚本提供程序的语言）。 表达式求值的结果必须以 IModelObject 的形式从脚本提供程序中封送出。 在调试程序处于中断状态时，所生成的 IModelObject 上的属性和其他构造必须能够获得。 

[EnumerateLocals](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-enumeratelocals)

EnumerateLocals 方法返回一个变量集（由 IDataModelScriptDebugVariableSetEnumerator 接口表示），该变量集位于由 IDataModelScriptDebugStackFrame 表示的堆栈帧上下文的范围内的所有局部变量中。在其上调用此方法的接口。 

[EnumerateArguments](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-enumeratearguments)

EnumerateArguments 方法返回由 IDataModelScriptDebugStackFrame 表示的堆栈帧中调用的函数的所有函数参数的变量集（由 IDataModelScriptDebugVariableSetEnumerator 接口表示）。在其上调用此方法的接口。 


**查看变量： IDataModelScriptDebugVariableSetEnumerator**

要调试的脚本中的变量集（无论是特定作用域中的变量、函数的局部变量、函数的参数等）由通过 IDataModelScriptDebugVariableSetEnumerator 接口定义的变量集表示：

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugVariableSetEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_ BSTR *variableName, _COM_Outptr_opt_ IModelObject **variableValue, _COM_Outptr_opt_result_maybenull_ IKeyStore **variableMetadata) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugvariablesetenumerator-reset)

Reset 方法将枚举器的位置重置为在创建后立即开始的位置（即，在该集的第一个元素之前）。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugvariablesetenumerator-getnext)

GetNext 方法将枚举器移动到集内的下一个变量，并返回变量的名称、值以及与之关联的任何元数据。 如果枚举器已到达集的末尾，则返回错误 E_BOUNDS。 从 GetNext 方法返回 E_BOUNDS 标记后，它将在再次调用时继续生成 E_BOUNDS，除非进行了干预重置调用。 


**断点： IDataModelScriptDebugBreakpoint**

脚本断点在给定脚本的调试接口上通过 SetBreakpoint 方法设置。 此类断点由唯一 id 和定义为以下的 IDataModelScriptDebugBreakpoint 接口的实现来表示。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugBreakpoint, IUnknown)
{
    STDMETHOD_(ULONG64, GetId)() PURE;
    STDMETHOD_(bool, IsEnabled)() PURE;
    STDMETHOD_(void, Enable)() PURE;
    STDMETHOD_(void, Disable)() PURE;
    STDMETHOD_(void, Remove)() PURE;
    STDMETHOD(GetPosition)(_Out_ ScriptDebugPosition *position, _Out_opt_ ScriptDebugPosition *positionSpanEnd, _Out_opt_ BSTR *lineText) PURE;
}
```

[GetId](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-getid)

GetId 方法返回由脚本提供程序的调试引擎分配给断点的唯一标识符。 此标识符在包含脚本的上下文中必须是唯一的。 断点标识符对于提供程序可能是唯一的;但这不是必需的。 

[IsEnabled](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-isenabled)

IsEnabled 方法返回是否启用断点。 禁用的断点仍然存在，并且仍在脚本的断点列表中，只是暂时处于 "关闭" 状态。 所有断点都应在 "已启用" 状态创建。 

[Enable](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-enable)

Enable 方法启用断点。 如果断点已禁用，则在调用此方法后 "命中断点" 将导致调试器中断。 

[禁用](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-disable)

Disable 方法将禁用该断点。 在此调用之后，调用此方法后 "命中断点" 不会中断调试器。 断点仍存在，被视为 "关闭"。 

[删除](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-remove)

Remove 方法从其包含列表中删除断点。 此方法返回后，断点不再出现在语义上。 调用后，表示断点的 IDataModelScriptDebugBreakpoint 接口被视为孤立。 除发布其他内容外，不能在此调用后对其执行任何其他操作。 

[GetPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-getposition)

GetPosition 方法返回该断点在脚本中的位置。 脚本调试器必须返回断点所在的源代码中的行和列。 如果它能够执行此操作，它还可以通过填充由 positionSpanEnd 参数定义的结束位置，来返回由断点表示的源的跨度。 如果调试器不能生成此跨度并且调用方请求，则应将跨距结束位置的行和列字段填充为零，以指示无法提供这些值。 


**断点枚举： IDataModelScriptDebugBreakpointEnumerator**

如果脚本提供程序支持调试，还必须跟踪与每个脚本相关联的所有断点，并能够将这些断点枚举到调试接口。 断点的枚举器在给定脚本的调试接口上通过 EnumerateBreakpoints 方法获取，并按如下所示定义。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugBreakpointEnumerator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptDebugBreakpoint **breakpoint) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpointenumerator-reset)

Reset 方法将枚举器的位置重置为创建枚举器后的位置（即在第一个枚举断点之前）。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpointenumerator-getnext)

GetNext 方法将枚举器向前移动到要枚举的下一个断点，并返回该断点的 IDataModelScriptDebugBreakpoint 接口。 如果枚举器已到达枚举的末尾，则返回 E_BOUNDS。 生成 E_BOUNDS 错误后，对 GetNext 方法的后续调用将继续生成 E_BOUNDS，除非对 Reset 方法进行了干预调用。 

---

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

本主题是一系列文章的一部分，其中描述了可C++从其访问的接口，如何使用C++它们来生成基于的调试器扩展，以及如何从C++数据模型扩展使用其他数据模型构造（例如： JavaScript 或 NatVis）.

[调试器数据模型C++概述](data-model-cpp-overview.md)

[调试器数据模型C++接口](data-model-cpp-interfaces.md)

[调试器数据模型C++对象](data-model-cpp-objects.md)

[调试器数据模型C++附加接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型C++概念](data-model-cpp-concepts.md)
