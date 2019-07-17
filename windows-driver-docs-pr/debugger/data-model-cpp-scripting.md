---
title: 调试器数据模型 C++ 脚本
description: 本主题介绍如何使用调试器数据模型C++脚本来支持自动化与调试器引擎。
ms.date: 10/08/2018
ms.openlocfilehash: 7860ee5a0f36c9f03eadc028f0c92cc10fc99e16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376089"
---
# <a name="debugger-data-model-c-scripting"></a>调试器数据模型 C++ 脚本

本主题介绍如何使用调试器数据模型C++调试器的数据模型C++脚本来支持自动化与调试器引擎使用脚本。

本主题是一系列用于描述可从访问接口的一部分C++，如何使用它们来生成C++调试器扩展，以及如何使基于使用的数据模型的其他构造 (例如：JavaScript 或 NatVis） 从C++数据模型扩展。

[调试器数据模型C++概述](data-model-cpp-overview.md)

[调试器数据模型C++接口](data-model-cpp-interfaces.md)

[调试器数据模型C++对象](data-model-cpp-objects.md)

[调试器数据模型C++的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型C++概念](data-model-cpp-concepts.md)

[调试器数据模型C++脚本](data-model-cpp-scripting.md)

---

## <a name="topic-sections"></a>主题部分

本主题包含以下部分：

[调试器数据模型中的脚本管理](#scriptmanangement)

[调试器数据模型C++用于脚本编写承载接口](#hostinterfacesscript)

[调试器数据模型C++脚本接口](#scriptinterface)

[调试器数据模型C++编写的脚本调试接口](#debugscript)

---

## <a name="span-idscriptmanangement-script-management-in-the-debugger-data-model"></a><span id="scriptmanangement"> 调试器数据模型中的脚本管理 

除了上对象的创建和可扩展性的中央机构作为数据模型管理器的角色时，它也是概念的负责管理脚本的一个抽象。 从脚本管理器部分的数据模型管理器的角度来看，脚本是后者可以动态加载、 卸载，并可能通过以扩展或提供的数据模型的新功能的提供程序进行调试的某些内容。 

脚本提供程序是一个组件用于桥接一种语言 (例如：NatVis、 JavaScript 等...)到数据模型。 它会注册一个或多个文件扩展名 (例如:"。NatVis"，".js") 的步骤将由允许调试器客户端或用户界面与该特定扩展名的脚本文件的加载，从而实现委派给提供程序的提供程序。 


**核心脚本管理器：IDataModelScriptManager**

核心脚本管理器接口定义，如下所示。 

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

[GetDefaultNameBinder](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-getdefaultnamebinder)

GetDefaultNameBinder 方法返回的数据模型的默认脚本名称联编程序。 名称联编程序是对象的一个组件可解析上下文中的名称。 例如，给定表达式"foo.bar"，名称联编程序被调用来解析对象 foo 的上下文中的名称栏。 此处返回的 binder 中遵循一组数据模型的默认规则。 脚本提供程序可以使用此联编程序提供程序之间提供名称解析的一致性。 


[RegisterScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-registerscriptprovider)

RegisterScriptProvider 方法将通知数据模型的新的脚本提供程序存在适合的桥接一种新语言到数据模型。 调用此方法时，脚本管理器将立即返回调用给定的脚本提供程序并查询它所管理的脚本的属性。 如果已存在名称或文件的扩展，用于指示给定的脚本提供程序下注册的提供程序，此方法将失败。 可以为特定的名称或文件扩展名的处理程序注册只能由单个脚本提供商。 


[UnregisterScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-unregisterscriptprovider)

UnregisterScriptProvider 方法撤消对 RegisterScriptProvider 方法的调用。 提供由 inpassed 的脚本提供程序的名称和文件扩展名将不再与之相关联。 请务必注意，可能有大量的脚本提供程序未完成的 COM 引用甚至后注销。 此方法只会加载/创建的类型的给定的脚本提供商管理的脚本。 如果由该提供程序加载的脚本仍处于加载状态或已操作的调试程序 （或数据模型） 的对象模型，这些操作可能仍具有恢复到该脚本的引用。 可能的数据模型、 方法或直接引用在脚本中的构造的对象。 脚本提供程序必须准备好解决这一问题。 


[FindProviderForScriptType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-findproviderforscripttype)

FindProviderForScriptType 方法搜索提供程序具有此方法中所示的脚本类型字符串的脚本管理器。 如果无法找到，此方法将失败;否则，此类脚本提供程序将返回给调用方。 


[EnumerateScriptProviders](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptmanager-enumeratescriptproviders)

EnumerateScriptProviders 方法将返回一个枚举器这样枚举速度将通过 RegisterScriptProvider 方法调用之前在脚本管理器已注册的每个脚本提供程序。 



**脚本提供程序枚举：IDataModelScriptProviderEnumerator**

EnumerateScriptProviders 方法将返回以下形式的枚举器：

```cpp 
DECLARE_INTERFACE_(IDataModelScriptProviderEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptProvider **provider) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptproviderenumerator-reset)

重置方法将移动到它在返回的第一个元素之前所处的位置的枚举器。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptproviderenumerator-getnext)

GetNext 方法将移动枚举数前移一个元素，并返回位于该元素的脚本提供程序。 当枚举器遇到枚举结束时，将返回 E_BOUNDS。 调用 GetNext 方法后收到此错误将继续无限期地返回 E_BOUNDS。 



## <a name="span-idhostinterfacesscript-debugger-data-model-c-host-interfaces-for-scripting"></a><span id="hostinterfacesscript"> 调试器数据模型C++用于脚本编写承载接口

**在脚本中的主机的角色**

调试主机公开一系列非常较低级别接口对于了解其调试目标的类型系统在本质上计算表达式语言中的其调试目标，等等...通常情况下，它是关心类似脚本等更高级构造。 此类是从左到整体调试器应用程序或提供这些功能的扩展。 没有，但是，一种例外。 想要参与的数据模型提供整体的脚本编写体验中的任何调试主机需要实现的几个简单接口以提供对脚本上下文。 实际上，调试主机是的它希望脚本环境，以将函数和提供的数据模型的命名空间中的功能的其他脚本的控件中。 此过程中所涉及允许主机以允许 （或不） 使用，例如，其表达式计算器中此类函数。 涉及到从以下主机的角度来看接口是： 

接口 | 描述
|---------|------------|
IDebugHostScriptHost | 一个接口，这指示调试主机能够参加脚本编写环境。 此接口允许通知的放置位置对象的脚本引擎的上下文创建。
IDataModelScriptHostContext | 主机接口，用来通过脚本提供程序作为容器的脚本的内容。 如何脚本图面以外的操作，对其执行到调试器应用程序的对象模型的内容是由特定的调试主机。 此接口允许脚本提供程序，以获取有关在何处放置其内容的信息。 请参阅[数据模型C++脚本接口](#scriptinterface)本主题中的详细信息的更高版本。


**调试主机的脚本主机：IDebugHostScriptHost**

IDebugHostScriptHost 接口是脚本提供程序用于为新创建的脚本从调试主机获取上下文的接口。 此上下文包括 （提供调试主机） 的对象的脚本提供程序可以放置任何数据模型和脚本编写环境之间的桥梁。 此类桥，可能的数据模型方法调用脚本函数。 执行此操作允许数据模型端使用量 IModelMethod 接口上调用方法调用脚本的方法的调用方。 

IDebugHostScriptHost 接口定义，如下所示。 

```cpp
DECLARE_INTERFACE_(IDebugHostScriptHost, IUnknown)
{
    STDMETHOD(CreateContext)(_In_ IDataModelScript* script, _COM_Outptr_ IDataModelScriptHostContext** scriptContext) PURE;
}
```

[CreateContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostscripthost-createcontext)

要创建新的上下文要在其中放置脚本的内容的脚本提供程序被调用 CreateContext 方法。 此类上下文表示由 IDataModelScriptHostContext 接口在数据模型上进行了详细说明C++编写脚本的接口页。 


## <a name="span-idscriptinterface-debugger-data-model-c-scripting-interfaces"></a><span id="scriptinterface"> 调试器数据模型C++脚本接口

**脚本和脚本接口**

数据模型的整体体系结构允许第三方来定义一些语言和数据模型的对象模型之间的桥梁。 通常情况下，被桥接的语言是一种脚本语言，因为是非常动态的数据模型的环境。 定义和实现一种语言和数据模型的对象模型之间的此桥的组件是名为脚本提供程序。 在初始化时，向数据模型管理器的脚本管理器部分的脚本提供程序注册自身和任何接口，该管理可扩展性接口将随后允许进行编辑，加载、 卸载和潜在的脚本调试写入到脚本提供商管理的语言。 

请注意，对于 Windows 调试工具目前定义两个脚本提供程序。

- NatVis 提供程序。 允许的本机/语言数据类型的可视化效果中 DbgEng.dll 和 NatVis XML 和数据模型之间的桥梁，嵌入此提供程序。
- JavaScript 提供程序。 此提供程序包含在传统的调试器扩展：JsProvider.dll。 它可以弥补之间 JavaScript 语言和数据模型中，对任意形式的调试器控制和可扩展性允许编写的脚本。

可以这桥接其他语言编写新的提供程序 (例如：Python，等等。...)到数据模型。 此类将当前封装在用于加载目的的传统调试器扩展。 脚本提供程序本身应尽量减少旧引擎接口对象的依赖项，并应仅使用数据模型 Api，在可能的情况。 这将允许的提供程序，使其可移植到其他环境，明显更容易。

有两个类与脚本提供程序相关的接口。 接口的第一个类是为脚本提供商和他们管理的脚本的常规管理。 第二个类的接口是用于支持的脚本调试。 第一组是必需的尽管支持对第二个是可选的可能没有意义的每个提供程序的支持。 


常规管理接口是： 

接口 | 描述
|---------|------------|
IDataModelScriptProvider | 脚本提供程序必须实现的核心接口。 这是脚本的注册到数据模型管理器以便播发的特定类型的提供程序的支持并注册针对特定文件扩展名的脚本管理器部分接口
IDataModelScript | 特定脚本正在管理提供程序的抽象。 每个脚本，它将被加载或正在编辑具有单独的 IDataModelScript 实例
IDataModelScriptClient | 一个客户端接口，将使用脚本提供程序的信息传递给一个用户界面。 脚本提供程序不实现此接口。 承载想要进行数据模型的应用程序的脚本提供程序使用 does。 脚本提供程序将调用方法的脚本客户端报告状态、 错误等...
IDataModelScriptHostContext | 主机接口，用来通过脚本提供程序作为容器的脚本的内容。 如何脚本图面以外的操作，对其执行到调试器应用程序的对象模型的内容是由特定的调试主机。 此接口允许脚本提供程序，以获取有关在何处放置其内容的信息。
IDataModelScriptTemplate | 脚本提供程序可以提供一个或多个模板以用作编写脚本的用户的起点。 提供了内置编辑器的调试器应用程序可以是预先填充其模板内容如播发由通过此接口提供程序的新脚本。
IDataModelScriptTemplateEnumerator | 它支持脚本提供程序实现以播发所有各种模板的枚举器接口。
IDataModelNameBinder | 名称联编程序-可以将在上下文中的名称与值关联的对象。 对于给定的表达式，例如"foo.bar"，名称联编程序是能够将对象"foo"的上下文中的绑定名称"bar"，并生成一个值或对它的引用。 名称绑定器通常未实现的脚本的提供程序;相反，获取从数据模型和脚本提供程序使用默认联编程序

调试接口是： 

接口 | 描述
|---------|------------|
IDataModelScriptDebug | 脚本提供程序必须提供才能使脚本可调试性核心接口。 如果该脚本可调试，IDataModelScript 接口的实现类必须为 IDataModelScriptDebug QueryInterface。
IDataModelScriptDebugClient | 其想要提供的脚本调试功能的用户界面实现 IDataModelScriptDebugClient 接口。 该脚本提供程序使用此接口可来回传递的调试信息 (例如： 事件出现、 断点，等等。...)
IDataModelScriptDebugStack | 脚本提供程序实现此接口以提供给脚本调试器调用堆栈这一概念。
IDataModelScriptDebugStackFrame | 脚本提供程序实现此接口公开特定堆栈帧调用堆栈中的概念。
IDataModelScriptDebugVariableSetEnumerator | 脚本提供程序实现此接口以公开一组变量。 此组可能为函数、 本地变量、 组或组在特定范围内的变量表示参数的集。 确切含义是取决于如何获取该接口。
IDataModelScriptDebugBreakpoint | 脚本提供程序实现此接口，以公开的概念和特定断点的脚本中的控件。
IDataModelScriptDebugBreakpointEnumerator | 脚本提供程序实现此枚举的所有断点 （无论启用） 当前存在的脚本中。

**核心脚本提供程序：IDataModelScriptProvider**

想要将脚本提供程序的任何扩展必须提供 IDataModelScriptProvider 接口的实现，并注册此类使用的数据模型管理器通过 RegisterScriptProvider 方法的脚本管理器部分。 它必须实现此核心接口定义，如下所示。

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

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getname)

GetName 方法返回的类型 （或语言） 的名称的脚本通过 SysAllocString 方法分配的字符串为管理提供程序。 调用方负责释放 SysFreeString 通过返回的字符串。 这可能会返回此方法从字符串的示例为"JavaScript"或"NatVis"。 返回的字符串是可能出现在调试器应用程序在托管数据模型的用户界面中。 没有两个脚本提供程序可能会返回相同的名称 （不区分大小写）。 

[GetExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getextension)

GetExtension 方法通过 SysAllocString 方法分配的字符串的形式返回的文件扩展名为受此提供程序 （不带点） 的脚本。 调试器应用程序宿主 （使用脚本支持） 的数据模型将委托与此扩展到脚本提供程序的脚本文件打开。 调用方负责释放 SysFreeString 通过返回的字符串。 这可能会返回此方法从字符串的示例包括"js"或"NatVis"。 

[CreateScript](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-createscript)

CreateScript 方法调用以创建新的脚本。 脚本提供程序必须返回每次调用此方法时，返回的 IDataModelScript 接口所表示的新的和空脚本。 请注意，而不考虑用户界面是否创建用于编辑用户的新空白脚本或调试器应用程序是否从磁盘加载脚本调用此方法。 提供程序不会涉及到在文件 I/O。 它只是处理来自托管应用程序通过流传递到方法 IDataModelScript 上的请求。 

[GetDefaultTemplateContent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-getdefaulttemplatecontent)

GetDefaultTemplateContent 方法返回提供程序的默认模板内容的接口。 这是希望脚本提供程序已经预填充新创建的脚本的编辑窗口的内容。 如果脚本提供程序没有模板 （或不包含任何模板内容，其指定为默认内容），脚本提供程序可能从该方法返回 E_NOTIMPL。 

[EnumerateTemplates](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptprovider-enumeratetemplates)

EnumerateTemplates 方法返回一个枚举器，这是可以枚举各种脚本提供程序提供的模板。 模板内容为脚本提供程序想要创建新的脚本时为"已预先"到编辑窗口。 如果有多个不同的模板支持，这些模板可以进行命名 (例如："命令性脚本"、"扩展脚本"） 和承载的数据模型的调试器应用程序可以选择如何向用户显示"模板"。 


**核心脚本界面：IDataModelScript**

用于管理由提供程序实现的单个脚本的主接口是 IDataModelScript 接口。 实现此接口的组件客户端希望创建一个新的空白脚本时，将返回并对 IDataModelScriptProvider 调用 CreateScript 方法。 

每个脚本，该提供程序创建脚本应在独立的接收器。 一个脚本不应能够影响除通过与通过数据模型的外部对象的显式交互的另一个脚本。 两个脚本，可以对实例，同时扩展某些类型或概念 (例如： 调试器的这一概念的进程)。 其中一个脚本可以访问彼此的字段通过外部进程对象。 

接口定义，如下所示。 

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

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-getname)

GetName 方法通过 SysAllocString 函数返回已分配的字符串形式的脚本的名称。 如果该脚本还没有一个名称，该方法应返回 null BSTR。 在此情况下，这应该不会失败。 如果该脚本通过调用 Rename 方法显式重命名，GetName 方法应返回新分配的名称。 

[重命名](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-rename)

重命名方法将新的名称分配给该脚本。 它负责要保存此名称并返回在任何 GetName 方法调用的脚本实现。 这通常称为用户界面选择另存为脚本保存到一个新名称。 请注意，重命名该脚本可能会影响在其中托管应用程序选择项目脚本的内容。 

[填充](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-populate)

填充方法称为客户端以更改或同步脚本的"内容"。 这是对脚本的代码已更改的脚本提供程序的通知。 请务必注意此方法不会导致执行脚本或对任何脚本操作的对象的更改。 这是只是到脚本的内容已更改，以便它可以同步其自己的内部状态的脚本提供程序的通知。 

[执行](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-execute)

Execute 方法规定的最后一次成功的填充调用执行脚本的内容，并修改该内容根据调试器的对象模型。 如果语言 （或脚本提供程序） 定义了"主要"-一个作者想时调用的函数后单击用户界面中的虚"执行脚本"按钮-在执行操作期间不调用此类"主函数"。 可以考虑执行操作以执行初始化和对象模型操作 (例如： 执行根代码和设置的扩展点)。 

[取消链接](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-unlink)

取消链接方法撤消执行操作。 对象模型的任何操作或脚本的执行期间建立的扩展点都将撤销。 操作完成后取消链接，该脚本可能会重新执行通过 Execute 调用，或可以释放。 

[IsInvocable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-isinvocable)

IsInvocable 方法返回指示在脚本为 invocable-即，指示它还有一个"主函数"，因为其语言或提供程序定义。 此类"主函数"从概念上讲是脚本作者希望在用户界面中调用如果虚"执行脚本"按钮按下的内容。 

[InvokeMain](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscript-invokemain)

如果脚本具有一个"主函数"其目的是从 UI 调用执行，则表示此类通过从 IsInvocable 方法返回时，则返回 true。 然后，用户界面可以调用 InvokeMain 方法来实际"调用"的脚本。 请注意，这不同于*Execute*运行所有根代码和桥脚本到基础主机的命名空间。 


\* * 脚本客户端：IDataModelScriptClient * *

应用程序承载想要管理脚本和具有用户界面的数据模型 (是否图形或控制台) 围绕这一概念实现 IDataModelScriptClient 接口。 此接口被传递给任何脚本提供程序期间执行或调用或脚本以将错误和事件信息传递到用户界面。 

IDataModelScriptClient 接口定义，如下所示。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptClient, IUnknown)
{
   STDMETHOD(ReportError)(_In_ ErrorClass errClass, _In_ HRESULT hrFail, _In_opt_ PCWSTR message, _In_ ULONG line, _In_ ULONG position) PURE;
}
```

[ReportError](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptclient-reporterror)

如果在执行或脚本调用期间发生错误，脚本提供程序调用 ReportError 方法以通知的用户界面的错误。 


**主机上下文的脚本：IDataModelScriptHostContext**

调试主机都有一些影响它方式和位置投影数据模型的脚本内容。 预计每个脚本要求宿主，为要在其中放置上下文桥接的脚本 (例如： 函数对象，可以调用，等等...)。通过调用 IDebugHostScriptHost CreateContext 方法和获取 IDataModelScriptHostContext 检索此上下文。 

IDataModelScriptHostContext 接口定义，如下所示。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptHostContext, IUnknown)
{
   STDMETHOD(NotifyScriptChange)(_In_ IDataModelScript* script, _In_ ScriptChangeKind changeKind) PURE;
   STDMETHOD(GetNamespaceObject)(_COM_Outptr_ IModelObject** namespaceObject) PURE;
}
```

[NotifyScriptChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripthostcontext-notifyscriptchange)

这是必需的脚本提供程序通知调试宿主后发生的对关联的上下文中的 NotifyScriptChange 方法的方法调用某些操作。 此类操作定义为 ScriptChangeKind 枚举的成员

[GetNamespaceObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripthostcontext-getnamespaceobject)

GetNamespaceObject 方法返回的对象的脚本提供程序可以放置任何数据模型和脚本之间的桥梁。 就在这里，例如，脚本提供程序可能放置数据模型方法对象 （装箱到 IModelObject IModelMethod 接口） 的实现将对相应地命名为脚本中的函数。 


**用于新创建的脚本模板：IDataModelScriptTemplate**

脚本需要显示的对新脚本的预先填充的内容的提供程序 (例如： 若要使用户的用户界面在调试器中编写脚本) 可以通过提供一个或多个脚本模板来实现。 此类模板是其实现 IDataModelScriptTemplate 接口和脚本提供程序上通过 GetDefaultTemplate 方法或 EnumerateTemplates 方法返回的组件。 

IDataModelScriptTemplate 接口定义，如下所示。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptTemplate, IUnknown)
{
   STDMETHOD(GetName)(_Out_ BSTR *templateName) PURE;
   STDMETHOD(GetDescription)(_Out_ BSTR *templateDescription) PURE;
   STDMETHOD(GetContent)(_COM_Outptr_ IStream **contentStream) PURE;
}
```


[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getname)

GetName 方法返回的模板的名称。 如果模板不具有一个名称，则可能会因 E_NOTIMPL。 一个默认模板 （如果存在此类） 不需要具有的名称。 所有其他模板。 这些名称可能要选择哪个模板中的菜单的一部分是创建时，用户界面中显示。 


[GetDescription](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getdescription)

GetDescription 方法返回模板的说明。 此类说明会提供给更具描述性的接口中的用户，以帮助用户了解该模板是用于执行操作。 如果它没有说明，模板可能会从此方法返回 E_NOTIMPL。 

[GetContent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplate-getcontent)

GetContent 方法返回模板的内容 （或代码）。 这是如果用户选择从该模板创建新的脚本将预先填充到编辑窗口。 该模板是负责创建 （并返回） 对客户端可以请求的内容的标准流。 

**枚举的提供程序的模板内容：IDataModelScriptTemplateEnumerator**

脚本提供程序可以提供一个或多个模板内容的预填充到某些用户界面中新创建的脚本。 如果提供了任何这些模板，脚本提供程序必须实现，这对 EnumerateTemplates 方法的调用时会返回一个枚举器。 

此类枚举器是 IDataModelScriptTemplateEnumerator 接口的实现，并按如下所示定义。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptTemplateEnumerator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptTemplate **templateContent) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplateenumerator-reset)

重置方法将枚举数重置为它所处时它首次创建-之前的第一个模板生成的位置。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscripttemplateenumerator-getnext)

GetNext 方法将枚举数移到下一个模板，并将其返回。 在枚举结束时，枚举器返回 E_BOUNDS。 一旦达到了 E_BOUNDS 标记，枚举器将继续无限期重置调用直到产生 E_BOUNDS 错误。 


**解析的名称的含义：IDataModelNameBinder**

数据模型提供脚本提供程序用来确定在给定上下文中具有给定名称的含义的标准方法 (例如： 确定哪些栏用于 foo.bar)，将运行跨多个脚本提供程序。 此机制称为名称绑定器，并由 IDataModelNameBinder 接口表示。 此类联编程序封装一组名称的解析方式以及如何处理其中一个名称在对象定义多个时间的冲突解决方法有关的规则。 这些规则的一部分包括投影的名称 （一个添加的数据模型） 如何解决与本机名 （一个正在调试的语言类型系统中） 等内容。 

为脚本提供程序在提供一定程度的一致性，数据模型的脚本管理器提供的默认名称联编程序。 可以通过调用 IDataModelScriptManager 接口上的 GetDefaultNameBinder 方法获取此默认名称联编程序。 名称绑定器接口定义，如下所示。 

```cpp
DECLARE_INTERFACE_(IDataModelNameBinder, IUnknown)
{
   STDMETHOD(BindValue)(_In_ IModelObject* contextObject, _In_ PCWSTR name, _COM_Errorptr_ IModelObject** value, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(BindReference)(_In_ IModelObject* contextObject, _In_ PCWSTR name, _COM_Errorptr_ IModelObject** reference, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
   STDMETHOD(EnumerateValues)(_In_ IModelObject* contextObject, _COM_Outptr_ IKeyEnumerator** enumerator) PURE;
   STDMETHOD(EnumerateReferences)(_In_ IModelObject* contextObject, _COM_Outptr_ IKeyEnumerator** enumerator) PURE;
}
```

[BindValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelnamebinder-bindvalue)

BindValue 方法根据绑定规则的一组给定对象上执行 contextObject.name 的等效项。 此绑定的结果是一个值。 一个值，作为基础脚本提供程序不能使用值执行回名称分配。

[BindReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelnamebinder-bindreference)

BindReference 方法的类似于 BindValue 在于，还将根据绑定规则的一组给定对象上执行 contextObject.name 的等效项。 但是，此方法从绑定的结果是而不是值的引用。 作为参考，脚本提供程序可以利用执行分配回名称的引用。 

[EnumerateValues](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelnamebinder-enumeratevalues)

EnumerateValues 方法枚举名称和值将绑定针对根据 BindValue 方法的规则的对象的集。 与不同 EnumerateKeys、 EnumerateValues 和 IModelObject 后者可能会返回多个名称使用相同的值 （适用于基类、 父模型等） 上的类似方法，此枚举器将仅返回特定的一组与将绑定的名称BindValue 和 BindReference。 不允许有重复的名称。 请注意，枚举通过比调用 IModelObject 方法的名称联编程序对象的明显更高成本。 

[EnumerateReferences](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelnamebinder-enumeratereferences)

EnumerateReferences 方法枚举一组的名称和对其的引用将绑定针对根据 BindReference 方法的规则的对象。 与不同 EnumerateKeys、 EnumerateValues 和 IModelObject 后者可能会返回多个名称使用相同的值 （适用于基类、 父模型等） 上的类似方法，此枚举器将仅返回特定的一组与将绑定的名称BindValue 和 BindReference。 不允许有重复的名称。 请注意，枚举通过比调用 IModelObject 方法的名称联编程序对象的明显更高成本。 


## <a name="span-iddebugscript-debugger-data-model-c-script-debugging-interfaces"></a><span id="debugscript"> 调试器数据模型C++编写的脚本调试接口

数据模型中的脚本提供程序的基础结构还提供了有关调试脚本的概念。 任何想要公开与调试主机承载的数据模型的调试器应用程序的调试功能的脚本可以通过让实现除了 IDataModelScript 界面 IDataModelScriptDebug 接口的可调试脚本来实现。 该脚本此接口存在对基础结构指示它是可调试。 

若要获取访问脚本提供程序的调试功能的起始点 IDataModelScriptDebug 接口时，它所加入由一组中提供整体的调试功能的其他接口。 

调试接口是： 

接口 | 描述
|---------|------------|
IDataModelScriptDebug | 脚本提供程序必须提供才能使脚本可调试性核心接口。 如果该脚本可调试，IDataModelScript 接口的实现类必须为 IDataModelScriptDebug QueryInterface。
IDataModelScriptDebugClient | 其想要提供的脚本调试功能的用户界面实现 IDataModelScriptDebugClient 接口。 该脚本提供程序使用此接口可来回传递的调试信息 (例如： 事件出现、 断点，等等。...)
IDataModelScriptDebugStack | 脚本提供程序实现此接口以提供给脚本调试器调用堆栈这一概念。
IDataModelScriptDebugStackFrame | 脚本提供程序实现此接口公开特定堆栈帧调用堆栈中的概念。
IDataModelScriptDebugVariableSetEnumerator | 脚本提供程序实现此接口以公开一组变量。 此组可能为函数、 本地变量、 组或组在特定范围内的变量表示参数的集。 确切含义是取决于如何获取该接口。
IDataModelScriptDebugBreakpoint | 脚本提供程序实现此接口，以公开的概念和特定断点的脚本中的控件。
IDataModelScriptDebugBreakpointEnumerator | 脚本提供程序实现此枚举的所有断点 （无论启用） 当前存在的脚本中。

常规管理接口是： 

接口 | 描述
|---------|------------|
IDataModelScriptProvider | 脚本提供程序必须实现的核心接口。 这是脚本的注册到数据模型管理器以便播发的特定类型的提供程序的支持并注册针对特定文件扩展名的脚本管理器部分接口
IDataModelScript | 特定脚本正在管理提供程序的抽象。 每个脚本，它将被加载或正在编辑具有单独的 IDataModelScript 实例
IDataModelScriptClient | 一个客户端接口，将使用脚本提供程序的信息传递给一个用户界面。 脚本提供程序不实现此接口。 承载想要进行数据模型的应用程序的脚本提供程序使用 does。 脚本提供程序将调用方法的脚本客户端报告状态、 错误等...
IDataModelScriptHostContext | 主机接口，用来通过脚本提供程序作为容器的脚本的内容。 如何脚本图面以外的操作，对其执行到调试器应用程序的对象模型的内容是由特定的调试主机。 此接口允许脚本提供程序，以获取有关在何处放置其内容的信息。
IDataModelScriptTemplate | 脚本提供程序可以提供一个或多个模板以用作编写脚本的用户的起点。 提供了内置编辑器的调试器应用程序可以是预先填充其模板内容如播发由通过此接口提供程序的新脚本。
IDataModelScriptTemplateEnumerator | 它支持脚本提供程序实现以播发所有各种模板的枚举器接口。
IDataModelNameBinder | 名称联编程序-可以将在上下文中的名称与值关联的对象。 对于给定的表达式，例如"foo.bar"，名称联编程序是能够将对象"foo"的上下文中的绑定名称"bar"，并生成一个值或对它的引用。 名称绑定器通常未实现的脚本的提供程序;相反，可以获取从数据模型和脚本提供程序使用默认联编程序。


**使脚本可调试：IDataModelScriptDebug**

这是可调试任何脚本指示通过实现 IDataModelScript 的同一个组件上的 IDataModelScriptDebug 接口存在此功能。 此接口由调试主机或承载数据模型的调试器应用程序的查询是什么指示调试功能存在。 

IDataModelScriptDebug 接口定义，如下所示。 

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

[GetDebugState](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getdebugstate)

GetDebugState 方法返回该脚本的当前状态 (例如： 是否执行或不)。 状态是由 ScriptDebugState 枚举中的值定义。

[GetCurrentPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getcurrentposition)

GetCurrentPosition 方法返回该脚本中的当前位置。 这只能调用如果脚本中断到调试器 GetScriptState 调用返回 ScriptDebugBreak 的位置。 任何其他调用此方法无效，将会失败。 

[GetStack](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-getstack)

GetStack 方法获取中断位置处的当前调用堆栈。 如果脚本中断到调试器，可能仅调用此方法。 

[SetBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-setbreakpoint)

SetBreakpoint 方法设置断点的脚本中。 请注意，实现随意调整 inpassed 的行和列位置向前移动到相应的代码位置。 可通过方法调用返回 IDataModelScriptDebugBreakpoint 接口上的实际行和列号放置断点的位置。 

[FindBreakpointById](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-findbreakpointbyid)

在脚本中通过 SetBreakpoint 方法创建的每个断点是由实现分配的唯一标识符 （64 位无符号整数）。 FindBreakpointById 方法用于获取到断点的一个接口，从给定的标识符。 

[EnumerateBreakpoints](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-enumeratebreakpoints)

EnumerateBreakpoints 方法返回一个枚举器可以枚举每个特定脚本中设置断点。 

[GetEventFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-geteventfilter)

GetEventFilter 方法将返回针对特定事件已启用"中断事件"。 这可能导致"中断事件"事件介绍 ScriptDebugEventFilter 枚举的成员。 

[SetEventFilter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-seteventfilter)

SetEventFilter 方法更改为特定事件的"中断事件"行为由 ScriptDebugEventFilter 枚举的成员定义。 可以为 GetEventFilter 方法的文档中找到可用的事件 （和此枚举的说明） 的完整列表。 

[StartDebugging](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-startdebugging)

StartDebugging 方法"开启"的某个特定脚本的调试器。 启动调试的 act 不主动会导致任何执行中断或单步执行。 它只是可使脚本可调试，并提供了一组客户端与调试接口进行通信的接口。 

[StopDebugging](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebug-stopdebugging)

StopDebugging 方法称为客户端想要停止调试。 此方法调用可能会在任何时候，StartDebugging 进行成功后 (例如： 期间中断，在执行脚本时，等等。...)。在调用立即停止所有调试活动和状态返回到调用 StartDebugging 之前重置。 


**调试接口：IDataModelScriptDebugClient**

其想要提供围绕脚本调试接口的调试主机或调试器应用程序必须向脚本调试器为调试接口上的 StartDebugging 方法通过提供 IDataModelScriptDebugClient 接口的实现脚本。 

IDataModelScriptDebugClient 是在其中调试事件传递和控制转到调试器界面从脚本执行引擎的通信通道。 它定义，如下所示。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugClient, IUnknown)
{
   STDMETHOD(NotifyDebugEvent)(_In_ ScriptDebugEventInformation *pEventInfo, _In_ IDataModelScript *pScript, _In_opt_ IModelObject *pEventDataObject, _Inout_ ScriptExecutionKind *resumeEventKind) PURE;
}
```

[NotifyDebugEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugclient-notifydebugevent)

每次任何事件发生时分解为多个脚本调试程序，调试代码本身可以通过 NotifyDebugEvent 方法接口的调用。 此方法是同步的。 没有执行该脚本将继续进行，直到接口返回的事件。 脚本调试程序的定义用于简单： 有嵌套绝对不需要处理的事件。 调试事件是由称为 ScriptDebugEventInformation 的变体记录定义的。 DebugEvent 成员很大程度上定义的信息是有效的事件中的哪些字段。 它定义事件发生所描述的 ScriptDebugEvent 枚举的成员的类型。

**调用堆栈：IDataModelScriptDebugStack**

事件时发生的分解为多个脚本调试器，调试接口将想要检索的中断位置的调用堆栈。 这是通过 GetStack 方法。 此类堆栈表示通过 IDataModelScriptDebugStack 定义，如下所示。 

请注意，整个堆栈可能跨多个脚本和/或多个脚本提供程序。 调用堆栈某个特定脚本调试接口返回通过 GetStack 方法一次调用应仅返回该脚本的边界内的调用堆栈段。 它是完全有可能脚本调试引擎可以检索调用堆栈，如跨多个脚本上下文，如果两个脚本的相同的提供程序进行交互。 GetStack 方法不应返回堆栈中的另一个脚本的一部分。 相反，如果可以检测到这种情况下，这是到脚本的边界帧的堆栈帧应将标记本身为通过该堆栈帧上的 IsTransitionPoint 和 GetTransition 方法的实现的过渡帧。 应，调试器界面将整合从多个堆栈段存在的在整个堆栈。 

非常有必要，在这种方式实现转换或调试接口会将有关局部变量、 参数、 断点、 查询和其他脚本特定构造到错误的脚本上下文 ！ 这将导致调试器界面中未定义的行为。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugStack, IUnknown)
{
   STDMETHOD_(ULONG64, GetFrameCount)() PURE;
   STDMETHOD(GetStackFrame)(_In_ ULONG64 frameNumber, _COM_Outptr_ IDataModelScriptDebugStackFrame **stackFrame) PURE;
}
```

[GetFrameCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstack-getframecount)

GetFrameCount 方法返回在此段中的调用堆栈的堆栈帧数。 如果在不同的脚本上下文中或不同的提供程序，提供程序可以检测到的帧，它应此信息指示给调用方通过此堆栈段上的入口帧的 IsTransitionPoint 和 GetTransition 方法的实现。 

[GetStackFrame](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstack-getstackframe)

GetStackFrame 堆栈段中获取特定堆栈帧。 调用堆栈有零个基于索引的系统： 中断事件的发生位置的当前堆栈帧是帧 0。 当前方法的调用方是第 1 帧 （依此类推）。 


**如果中断正在检查状态：IDataModelScriptDebugStackFrame**

如果脚本调试器中中断的调用堆栈的特定帧可以检索通过发生中断 IDataModelScriptDebugStack 接口表示堆栈段上的 GetStackFrame 方法调用。 返回表示此帧的 IDataModelScriptDebugStackFrame 接口定义，如下所示。

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

[GetName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-getname)

GetName 方法返回的显示名称 (例如： 函数名称) 的此帧。 此类名称将显示在调试器界面中向用户显示堆栈回溯。 

[GetPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-getposition)

GetPosition 方法返回代表堆栈帧的脚本中的位置。 如果脚本是一个分行符，由其中包含此帧的堆栈中，可能仅调用此方法。 始终返回此范围内的行和列位置。 如果调试器能够返回的脚本中的"执行位置"的范围，可以 positionSpanEnd 参数中返回的结束位置。 如果不支持此调试器，则 s p a n 端 （如果请求） 中的行和列的值应设置为零。 

[IsTransitionPoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-istransitionpoint)

IDataModelScriptDebugStack 接口表示调用堆栈-调用堆栈包含在一个脚本的上下文内的该部分的段。 如果调试器能够检测到另一个脚本 （或到另一个脚本提供程序） 中的转换，它可以通过实现 IsTransitionPoint 方法并返回 true 或 false，根据需要来进行指示。 转换点，应考虑输入脚本段其中适用的调用堆栈帧。 不是所有其他帧。 

[GetTransition](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-gettransition)

如果给定的堆栈帧转换点由 IsTransition 方法 （请参阅的文档有关的转换点定义），GetTransition 方法返回有关转换的信息。 具体而言，此方法将返回上一个脚本--这使得调用堆栈段，其中包含此 IDataModelScriptDebugStackFrame 代表的脚本的一个。 

[评估](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-evaluate)

Evaluate 方法由 IDataModelScriptDebugStackFrame 接口在其调用此方法表示堆栈帧的上下文中计算 （的脚本提供程序的语言） 表达式。 表达式计算结果必须作为 IModelObject 封送出脚本提供程序。 属性和生成 IModelObject 的其他构造所有必须能够在调试器处于中断状态时获取。 

[EnumerateLocals](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-enumeratelocals)

EnumerateLocals 方法返回的所有本地变量由 IDataModelScriptDebugStackFrame 表示堆栈帧的上下文中的作用域中的设置变量 （由 IDataModelScriptDebugVariableSetEnumerator 接口）在其调用此方法的接口。 

[EnumerateArguments](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugstackframe-enumeratearguments)

EnumerateArguments 方法返回由 IDataModelScriptDebugStackFrame 表示堆栈帧中调用的函数的所有函数参数设置变量 （由 IDataModelScriptDebugVariableSetEnumerator 接口）在其调用此方法的接口。 


**查看变量：IDataModelScriptDebugVariableSetEnumerator**

一组在正在调试的脚本中的变量 (是否中特定作用域、 一个函数的局部变量、 参数的函数等...) 由通过 IDataModelScriptDebugVariableSetEnumerator 接口定义的变量集：

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugVariableSetEnumerator, IUnknown)
{
    STDMETHOD(Reset)() PURE;
    STDMETHOD(GetNext)(_Out_ BSTR *variableName, _COM_Outptr_opt_ IModelObject **variableValue, _COM_Outptr_opt_result_maybenull_ IKeyStore **variableMetadata) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugvariablesetenumerator-reset)

重置方法将枚举器的位置重置为了创建-后立即，即在集中的第一个元素之前。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugvariablesetenumerator-getnext)

GetNext 方法将枚举数移到集中的下一个变量，并返回变量的名称、 值和与之关联的任何元数据。 如果枚举数已达到集的末尾，E_BOUNDS 会返回错误。 一旦从 GetNext 方法返回后 E_BOUNDS 标记，它将继续生成 E_BOUNDS 时再次调用，除非进行干预调用重置。 


**断点：IDataModelScriptDebugBreakpoint**

在给定的脚本的调试接口上，通过 SetBreakpoint 方法设置脚本断点。 此类断点表示的唯一 id 和 IDataModelScriptDebugBreakpoint 接口定义，如下所示的实现。 

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

[GetId](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-getid)

GetId 方法将返回分配到该断点的脚本提供程序的调试引擎的唯一标识符。 此标识符必须是包含脚本的上下文中是唯一的。 断点标识符可能是唯一的该提供程序;但是，不需要。 

[IsEnabled](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-isenabled)

IsEnabled 方法返回指示启用断点。 已禁用的断点仍然存在并且仍在脚本的断点的列表，它只是"关闭"暂时。 应在已启用状态中创建的所有断点。 

[Enable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-enable)

Enable 方法用于启用断点。 如果已禁用断点，调用此方法后的"命中断点"会中断到调试器。 

[禁用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-disable)

Disable 方法禁用断点。 此调用后，调用此方法后的"命中断点"不会中断到调试器。 所需断点，尽管仍然存在，被视为"关闭"。 

[删除](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-remove)

Remove 方法从其包含列表中删除断点。 断点在语义上不再存在此方法返回后。 孤立的调用后，属于 IDataModelScriptDebugBreakpoint 接口将表示该断点。 其他任何内容 （合法） 可以与之之外释放此调用后。 

[GetPosition](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpoint-getposition)

GetPosition 方法返回的脚本中的断点的位置。 脚本调试程序必须返回的行和列源代码中的的断点所在的位置。 如果能够执行此操作，它还可以返回由该断点表示通过填写结束位置的方式的 positionSpanEnd 参数定义的源跨度。 如果调试器能够生成此跨度，并且调用方请求它，应不能提供的值为零，表明填充范围的结束位置的行和列字段。 


**断点枚举：IDataModelScriptDebugBreakpointEnumerator**

如果脚本访问接口支持调试，它必须还跟踪的与每个脚本相关联的所有断点并可以枚举这些断点到调试接口。 断点的枚举器通过给定脚本调试接口上的 EnumerateBreakpoints 方法获取，并按如下所示定义。 

```cpp
DECLARE_INTERFACE_(IDataModelScriptDebugBreakpointEnumerator, IUnknown)
{
   STDMETHOD(Reset)() PURE;
   STDMETHOD(GetNext)(_COM_Outptr_ IDataModelScriptDebugBreakpoint **breakpoint) PURE;
}
```

[重置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpointenumerator-reset)

重置方法重置到了枚举器-即之前创建的第一个枚举断点后的枚举器的位置。 

[GetNext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idatamodelscriptdebugbreakpointenumerator-getnext)

GetNext 方法将枚举数向前移动到下一个要枚举的断点，并返回该断点的 IDataModelScriptDebugBreakpoint 接口。 如果枚举数已经到达枚举末尾，则返回 E_BOUNDS。 一旦已生成 E_BOUNDS 错误，对 GetNext 方法的后续调用将继续生成 E_BOUNDS，除非重置方法对的干预调用。 





---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[调试器数据模型C++概述](data-model-cpp-overview.md)

[调试器数据模型C++接口](data-model-cpp-interfaces.md)

[调试器数据模型C++对象](data-model-cpp-objects.md)

[调试器数据模型C++的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型C++概念](data-model-cpp-concepts.md)

[调试器数据模型C++脚本](data-model-cpp-scripting.md)
