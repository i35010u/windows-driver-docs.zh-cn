---
title: 调试器数据模型 C++ 接口
description: 本主题介绍如何使用调试器数据模型 c + + 接口来扩展和自定义调试器的功能。
ms.date: 10/08/2018
ms.openlocfilehash: 831e11ba8d5bcb28bd7842a9653dfff4205aafe7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564038"
---
# <a name="debugger-data-model-c-interfaces"></a>调试器数据模型 C++ 接口 

本主题提供了和如何使用调试器数据模型 c + + 接口来扩展和自定义调试器的功能的概述。

本主题是一系列用于描述可从 c + +、 如何使用它们来构建基于 c + + 调试器扩展，以及如何使访问接口的一部分使用的数据模型的其他构造 (例如：JavaScript 或 NatVis） 从 c + + 数据模型扩展插件。

[调试程序数据模型 c + + 概述](data-model-cpp-overview.md)

[调试器数据模型 c + + 接口](data-model-cpp-interfaces.md)

[调试器数据模型 c + + 对象](data-model-cpp-objects.md)

[调试器数据模型 c + + 其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 c + + 概念](data-model-cpp-concepts.md)

[C + + 编写脚本的调试程序数据模型](data-model-cpp-scripting.md)

---

## <a name="topic-sections"></a>主题部分

本主题包含以下部分：

[调试器数据模型 c + + 主机接口](#hostinterface)

[访问数据模型](#accessdatamodel)

[调试器数据模型的系统的接口](#systeminterfaces)

---

## <a name="span-idhostinterfacespan-debugger-data-model-c-host-interfaces"></a><span id="hostinterface"></span> 调试器数据模型 c + + 主机接口

**调试器数据模型主机**

调试器数据模型设计为可以在各种不同环境中托管的组件化的系统。 通常情况下，数据模型被托管的调试器应用程序上下文中。 若要在数据模型的主机，多个接口需要实现公开调试器的核心内容： 其目标，其内存空间，其计算器，其符号并键入系统，等等...而想要托管的数据模型的任何应用程序通过实现这些接口，它们被使用核心数据模型以及任何扩展的数据模型与互操作。 

核心接口的一组是： 

接口名称 | 描述
|--------------|---------------|
IDebugHost | 调试主机核心接口。
IDebugHostStatus  | 主机的状态为允许客户端查询接口。
IDebugHostContext  | 在主机内的上下文的抽象 (例如： 特定的目标、 特定的进程、 特定的地址空间，等等...)
IDebugHostErrorSink  | 若要从主机和数据模型的某些部分接收错误的调用方实现的接口
IDebugHostEvaluator / IDebugHostEvaluator2  | 调试主机的表达式计算器。
IDebugHostExtensibility  | 用于扩展的主机的功能或它的部分 （例如，表达式计算器） 的接口。

类型系统和符号的接口是： 

InterfaceName | 描述
|--------------|---------------|
IDebugHostSymbols | 核心接口，它提供了对访问和符号的解决方法
IDebugHostSymbol / IDebugHostSymbol2  | 表示任何类型的单个符号。 特定符号是此接口的派生。
IDebugHostModule | 表示在进程内加载的模块。 这是一种符号。
IDebugHostType / IDebugHostType2  | 表示本机/语言类型。
IDebugHostConstant  | 表示符号化信息中的一个常数 (例如： c + + 中的非类型模板参数)
IDebugHostField  | 表示结构或类中的字段。
IDebugHostData | 表示在模块中的数据 （已在结构或类会 IDebugHostField 的这）
IDebugHostBaseClass | 表示一个基类。
IDebugHostPublic  | 表示在 PDB publics 表中的符号。 这并没有与之关联的类型信息。 它是一个名称和地址。
IDebugHostModuleSignature | 表示模块签名-这将由名称和/或版本匹配一组模块的定义
IDebugHostTypeSignature | 表示类型签名-这将通过模块和/或名称匹配的一组类型的定义


**核心主机接口：IDebugHost**

IDebugHost 接口是数据模型的任何主机的核心接口。 它定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHost, IUnknown)
{
    STDMETHOD(GetHostDefinedInterface)(_COM_Outptr_ IUnknown** hostUnk) PURE;
    STDMETHOD(GetCurrentContext)(_COM_Outptr_ IDebugHostContext** context) PURE;
    STDMETHOD(GetDefaultMetadata)(_COM_Outptr_ IKeyStore** defaultMetadataStore) PURE;
}
```

[GetHostDefinedInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughost-gethostdefinedinterface)

如果此类为指定的主机存在，GetHostDefinedInterface 方法将返回主机的主专用接口。 对于的 Windows 调试工具，该接口返回此处是 IDebugClient （强制转换为 IUnknown）。 

[GetCurrentContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughost-getcurrentcontext)

GetCurrentContext 方法返回表示调试器主机的当前状态的接口。 确切含义应由主机，但它通常包括以下任务： 会话、 流程和调试主机的用户界面中处于活动状态的地址空间。 返回的上下文对象是很大程度上给调用方不透明，但它是一个重要的对象对调试主机的调用之间传递。 调用方，例如，读取内存时，必须知道内存从硬盘读出哪些进程和地址空间。 这种观点被封装在从此方法返回的上下文对象的概念。 

[GetDefaultMetadata](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughost-getdefaultmetadata)

GetDefaultMetadata 方法将返回可能的默认元数据存储用于某些操作 (例如： 字符串转换) 时没有显式的元数据已被传递。 这允许调试主机具有一些数据显示的方式的某些控制。 例如，默认元数据可能包括 PreferredRadix 密钥，从而允许宿主以指示是否序号应为以十进制或十六进制显示如果未另外指定。 

请注意，默认元数据存储区上的属性值必须手动解决必须通过为其查询的默认元数据的对象。 GetKey 方法应使用 GetKeyValue 代替。 

**状态界面中：IDebugHostStatus** 

IDebugHostStatus 接口允许客户端的数据模型或调试主机就可以提出调试主机的状态的某些方面。 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostStatus, IUnknown)
{
    STDMETHOD(PollUserInterrupt)(_Out_ bool* interruptRequested) PURE;
}
```

[PollUserInterrupt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughoststatus-polluserinterrupt)

PollUserInterrupt 方法用于查询调试主机的用户是否已请求中断当前操作。 属性访问器中的数据模型可能，例如，调用任意代码 (例如： JavaScript 方法)。 该代码可能需要任意长的时间。 为了使调试主机保持响应状态，这可能需要任意数量的时间的任何此类代码应检查通过调用此方法的中断请求。 如果 interruptRequested 值返回为 true，调用方应立即中止，并返回 e ABORT 的结果。 


**Context 接口：IDebugHostContext**

上下文是一个数据模型和基础调试主机的最重要的方面。 一个对象时，是重要的是能够知道对象原来所在的位置-的进程中，地址空间它与相关联。 了解这些信息使指针值等内容的正确解释。 类型的对象 IDebugHostContext 必须传递到很多方法调试主机。 可以多种方式获取此接口：

- 通过获取调试器的当前上下文： 调用 IDebugHost GetCurrentContext 方法
- 通过获取该对象的上下文： 调用 IModelObject GetContext 方法
- 通过获取符号的上下文： 调用 IDebugHostSymbol GetContext 方法

此外，有两个值分别 IDebugHostContext 接口从返回或传递到数据模型或调试主机方法的上下文中有特殊含义： 

*nullptr*： 没有上下文的指示。 它是完全有效的某些对象有没有上下文。 数据模型的根命名空间中的调试器对象不是指特定的进程或地址空间中的任何内容。 它具有无上下文。

*USE_CURRENT_HOST_CONTEXT*: sentinel 值，该值指示一个应使用调试主机的当前 UI 上下文。 此值将永远不会返回从调试主机。 可能，但是，会传递给采用而不是显式调用 IDebugHost GetCurrentContext 方法输入的 IDebugHostContext 任何调试主机方法。 请注意，显式传递 USE_CURRENT_HOST_CONTEXT 通常比显式获取当前上下文更高的性能。 

主机上下文的上下文是很大程度上给调用方不透明的。 核心调试主机外部的调用方可以与主机上下文执行操作的唯一操作是其与另一个主机上下文进行比较。 

IDebugHostContext 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostContext, IUnknown)
{
    STDMETHOD(IsEqualTo)(_In_ IDebugHostContext *pContext, _Out_ bool *pIsEqual) PURE;
}
```

[IsEqualTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostcontext-isequalto)

IsEqualTo 方法进行比较的主机上下文的另一个主机上下文。 如果两个上下文是等价的则返回的这指示。 请注意，此比较不是接口等效性。 这将进行比较的上下文本身基础不透明的内容。 


**错误接收器中：IDebugHostErrorSink**

IDebugHostErrorSink 是按其客户端可以接收通知的错误的某些操作期间发生，并将路由这些错误的方式在需要时。 接口定义，如下所示： 

```cpp
enum ErrorClass
{
    ErrorClassWarning,
    ErrorClassError
}
```

```cpp
DECLARE_INTERFACE_(IDebugHostErrorSink, IUnknown)
{
    STDMETHOD(ReportError)(_In_ ErrorClass errClass, _In_ HRESULT hrError, _In_ PCWSTR message) PURE;
}
```

[ReportError](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosterrorsink-reporterror)

ReportError 方法是以通知它发生错误，并允许接收器将路由到任何 UI 或机制是相应的错误的错误接收器上的回调。 


**主机计算器中：IDebugHostEvaluator / IDebugHostEvaluator2**

一个功能调试主机提供对客户端的最重要部分是访问其基于语言表达式计算器。 IDebugHostEvaluator 和 IDebugHostEvaluator2 接口是从调试主机访问该功能的方式。 

接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostEvaluator2, IDebugHostEvaluator)
{
    //
    // IDebugHostEvaluator:
    //
    STDMETHOD(EvaluateExpression)(_In_ IDebugHostContext* context, _In_ PCWSTR expression, _In_opt_ IModelObject* bindingContext, _COM_Errorptr_ IModelObject** result, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    STDMETHOD(EvaluateExtendedExpression)(_In_ IDebugHostContext* context, _In_ PCWSTR expression, _In_opt_ IModelObject* bindingContext, _COM_Errorptr_ IModelObject** result, _COM_Outptr_opt_result_maybenull_ IKeyStore** metadata) PURE;
    //
    // IDebugHostEvaluator2:
    //
    STDMETHOD(AssignTo)(_In_ IModelObject* assignmentReference, _In_ IModelObject* assignmentValue, _COM_Errorptr_ IModelObject** assignmentResult, _COM_Outptr_opt_result_maybenull_ IKeyStore** assignmentMetadata) PURE;
}
```

[EvaluateExpression](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostevaluator-evaluateexpression)

EvaluateExpression 方法允许请求调试主机来评估一种语言 (例如：C + +） 表达式并返回该表达式计算的结果值装箱为 IModelObject。 该方法的此特定变体仅允许语言构造。 任何其他功能是不存在的语言的调试主机的表达式计算器中的显示 (例如：LINQ 查询方法） 已关闭以进行评估。 

[EvaluateExtendedExpression](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostevaluator-evaluateextendedexpression)

EvaluateExtendedExpression 方法具有 EvaluateExpression 方法相似，只不过它将转换上其他非语言功能特定的调试主机选择要添加到其表达式计算器。 对于为 Windows 调试工具，例如，这使匿名类型、 LINQ 查询、 模块限定符，格式说明符和其他非-C/c + + 功能。 


**IDebugHostEvaluator2**

[AssignTo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostevaluator2-assignto)

AssignTo 方法执行分配根据语义正在调试的语言。 


**主机可扩展性接口：IDebugHostExtensibility**

调试主机的某些功能 （可选） 受到的可扩展性。 这可能，例如，包括表达式计算器。 IDebugHostExtensibility 接口是这些扩展点通过其访问的方法。 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostExtensibility, IUnknown)
{
    STDMETHOD(CreateFunctionAlias)(_In_ PCWSTR aliasName, _In_ IModelObject *functionObject) PURE;
    STDMETHOD(DestroyFunctionAlias)(_In_ PCWSTR aliasName) PURE;
}
```

[CreateFunctionAlias](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostextensibility-createfunctionalias)

CreateFunctionAlias 方法创建的"函数别名"，在某些扩展中实现的方法的"快速别名"。 此别名的含义是特定的主机。 它可能会扩展主机的表达式计算器使用函数或它可能会执行完全不同的东西。 

[DestroyFunctionAlias](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostextensibility-destroyfunctionalias)

DestroyFunctionAlias 方法撤消 CreateFunctionAlias 方法调用之前。 该函数将不再提供快速的别名名称下。 



## <a name="span-idaccessdatamodel-accessing-the-data-model"></a><span id="accessdatamodel"> 访问数据模型

首先，这一数据建模的扩展性的 Api 设计为非特定语言到应用程序 （通常调试器） 作为数据模型的主机。 从理论上讲，任何应用程序可以通过提供一组主机到有关哪些目标、 进程、 线程、 数据模型的命名空间公开应用程序的调试目标的类型系统和一组投影对象的 Api 的托管数据模型等...中的调试目标。 

尽管数据模型 Api-的开头 IDataModel<em>，IDebugHost</em>，并且设计为可移植的 IModelObject-负责，它们不定义什么是"调试器扩展"是。 今天，想要扩展的 Windows 调试工具和它提供了该引擎的组件必须编写引擎扩展，以获取对数据模型的访问。 该引擎扩展只需将像是加载和启动机制，用于扩展中的一个引擎扩展。 在这种情况下，将提供的最小实现： 

- **调用 DebugExtensionInitialize**:使用创建的 IDebugClient，若要获取对数据模型的访问，并设置了对象模型操作方法。
- **DebugExtensionUninitialize**:撤消其在调用 DebugExtensionInitialize 中所执行的对象模型操作方法。
- **DebugExtensionCanUnload**:一种方法可返回是否可以卸载该扩展。 如果扩展中仍然活动的 COM 对象，它必须指示这一点。 这是 COM 的 DllCanUnloadNow 调试器的等效项。 如果此方法返回的不能卸载 S_FALSE 指示，调试器可以查询此更高版本以查看是否是安全的卸载，或者它可能会再次调用调用 DebugExtensionInitialize 重新初始化该扩展。 扩展必须准备好处理这两个路径。
- **DebugExtensionUnload**:这会执行任何最终的清理方法之前 DLL 卸载所需权限

*桥接接口：IHostDataModelAccess*

如前文所述，调用 DebugExtensionInitialize 调用时，它将创建调试客户端并获取对数据模型的访问。 此类访问提供的有关 Windows 调试工具的旧 IDebug * 个接口和数据模型之间的桥接接口。 此桥接接口是 IHostDataModelAccess，定义如下： 

```cpp
DECLARE_INTERFACE_(IHostDataModelAccess, IUnknown)
{
   STDMETHOD(GetDataModel)(_COM_Outptr_ IDataModelManager** manager, _COM_Outptr_ IDebugHost** host) PURE;
}
```

[GetDataModel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-ihostdatamodelaccess-getdatamodel)

GetDataModel 方法是在桥接接口提供了访问权的数据模型的两面上的方法：通过返回 IDataModelManager 接口表示数据模型的主要组件-数据模型管理器返回的 IDebugHost 接口来表示调试主机 （在调试器中的下边缘）



## <a name="span-idsysteminterfacesspan-debugger-data-model-system-interfaces"></a><span id="systeminterfaces"></span> 调试器数据模型的系统的接口

**数据模型主机**

调试器数据模型设计为可以在各种不同环境中托管的组件化的系统。 通常情况下，数据模型被托管的调试器应用程序上下文中。 若要在数据模型的主机，多个接口需要实现公开调试器的核心内容： 其目标，其内存空间，其计算器，其符号并键入系统，等等...而想要托管的数据模型的任何应用程序通过实现这些接口，它们被使用核心数据模型以及任何扩展的数据模型与互操作。 

类型系统和符号的接口是： 


接口名称 | 描述
|--------------|------------------|
IDebugHostSymbols  | 核心接口，它提供了对访问和符号的解决方法
IDebugHostSymbol / IDebugHostSymbol2  | 表示任何类型的单个符号。 特定符号是此接口的派生。
IDebugHostModule  | 表示在进程内加载的模块。 这是一种符号。
IDebugHostType / IDebugHostType2  | 表示本机/语言类型。
IDebugHostConstant  | 表示符号化信息中的一个常数 (例如： c + + 中的非类型模板参数)
IDebugHostField | 表示结构或类中的字段。
IDebugHostData | 表示在模块中的数据 （已在结构或类会 IDebugHostField 的这）
IDebugHostBaseClass  | 表示一个基类。
IDebugHostPublic | 表示在 PDB publics 表中的符号。 这并没有与之关联的类型信息。 它是一个名称和地址。
IDebugHostModuleSignature | 表示模块签名-这将由名称和/或版本匹配一组模块的定义
IDebugHostTypeSignature | 表示类型签名-这将通过模块和/或名称匹配的一组类型的定义

其他核心接口是： 

接口名称 | 描述
|--------------|------------------|
IDebugHost | 调试主机核心接口。
IDebugHostStatus | 主机的状态为允许客户端查询接口。
IDebugHostContext | 在主机内的上下文的抽象 (例如： 特定的目标、 特定的进程、 特定的地址空间，等等...)
IDebugHostErrorSink | 若要从主机和数据模型的某些部分接收错误的调用方实现的接口
IDebugHostEvaluator / IDebugHostEvaluator2 | 调试主机的表达式计算器。
IDebugHostExtensibility | 用于扩展的主机的功能或它的部分 （例如，表达式计算器） 的接口。


**主符号接口：IDebugHostSymbols**

IDebugHostSymbols 接口是访问中的符号调试目标的主要起始点。 此接口可从 IDebugHost 的实例中查询和定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostSymbols, IUnknown)
{
    STDMETHOD(CreateModuleSignature)(_In_z_ PCWSTR pwszModuleName, _In_opt_z_ PCWSTR pwszMinVersion, _In_opt_z_ PCWSTR pwszMaxVersion, _Out_ IDebugHostModuleSignature** ppModuleSignature) PURE;
    STDMETHOD(CreateTypeSignature)(_In_z_ PCWSTR signatureSpecification, _In_opt_ IDebugHostModule* module, _Out_ IDebugHostTypeSignature** typeSignature) PURE;
    STDMETHOD(CreateTypeSignatureForModuleRange)(_In_z_ PCWSTR signatureSpecification, _In_z_ PCWSTR moduleName, _In_opt_z_ PCWSTR minVersion, _In_opt_z_ PCWSTR maxVersion, _Out_ IDebugHostTypeSignature** typeSignature) PURE;
    STDMETHOD(EnumerateModules)(_In_ IDebugHostContext* context, _COM_Outptr_ IDebugHostSymbolEnumerator** moduleEnum) PURE;
    STDMETHOD(FindModuleByName)(_In_ IDebugHostContext* context, _In_z_ PCWSTR moduleName, _COM_Outptr_ IDebugHostModule **module) PURE;
    STDMETHOD(FindModuleByLocation)(_In_ IDebugHostContext* context, _In_ Location moduleLocation, _COM_Outptr_ IDebugHostModule **module) PURE;
    STDMETHOD(GetMostDerivedObject)(_In_opt_ IDebugHostContext *pContext, _In_ Location location, _In_ IDebugHostType* objectType, _Out_ Location* derivedLocation, _Out_ IDebugHostType** derivedType) PURE;
}
```

[CreateModuleSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-createmodulesignature)

CreateModuleSignature 方法创建可以用于匹配一组特定模块 （可选） 按名称和版本的签名。 有三个组件的模块签名： 

- 名称： 匹配的模块必须具有针对签名中的名称不区分大小写完全匹配的名称
- 最低版本： 如果指定，匹配的模块必须具有至少高达此版本的最小版本。 与每个要比之前不太重要的后续部分"A.B.C.D"格式指定版本。 只有第一个段是必需的。
- 最高版本： 如果指定，匹配的模块必须具有的最大版本即不大于此版本。 与每个要比之前不太重要的后续部分"A.B.C.D"格式指定版本。 只有第一个段是必需的。

[CreateTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-createtypesignature)

CreateTypeSignature 方法创建可以用于通过将包含模块和类型名称匹配的一组具体类型的签名。 类型名称的签名字符串的格式是特定于正在调试的语言 （和调试主机）。 C/c + + 的签名字符串等效于 NatVis 类型规范。 签名字符串，即是类型名称的通配符 (指定为 *) 允许使用模板自变量。 

[CreateTypeSignatureForModuleRange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-createtypesignatureformodulerange)

CreateTypeSignatureForModuleRange 方法创建的签名可以用于具体类型的一组匹配的模块签名和类型名称。 它类似于只不过，而不是传递特定模块的签名匹配，调用方传递自变量创建模块签名所需的 CreateTypeSignature 方法 (就像使用创建的模块签名CreateModuleSignature 方法）。 

[EnumerateModules](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-enumeratemodules)

EnumerateModules 方法创建的枚举器这样枚举速度将特定的主机上下文中可用的每个模块。 该主机上下文可能会封装进程上下文或者它可能会封装类似于 Windows 内核的内容。 


[FindModuleByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-findmodulebyname)

FindModuleByName 方法将仔细查看给定的主机上下文和找到具有指定的名称的模块并返回到该接口。 它是合法模块按名称或不带文件扩展名搜索。 

[FindModuleByLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-findmodulebylocation)

FindModuleByLocation 方法将仔细查看给定的主机上下文并确定哪些模块包含由指定的位置的地址。 然后，它会向此类模块返回一个接口。 

[GetMostDerivedObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbols-getmostderivedobject)

GetMostDerivedObject 将使用调试器的类型系统以确定其静态类型中的对象的运行时类型。 此方法将仅使用符号化信息和试探法可用在类型系统层上才能执行此分析。 此类信息可能包括 c + + RTTI （运行时类型信息） 或分析的虚函数表的对象的形状。 它不包括等 IModelObject 首选的运行时类型的概念。 如果分析找不到运行时类型，或找不到运行时类型传递给该方法的静态类型不同，可能会传递的输入的位置和类型。该方法不会出于这些原因失败。 



**核心单个符号接口：IDebugHostSymbol**

可以从数据模型主机返回每个符号将以某种方式从 IDebugHostSymbol 派生。 这是每个符号实现而不考虑符号种类的核心接口。 符号种类，根据给定的符号可能会实现一组其他按返回的属性多个唯一到特定类型的符号表示此接口的接口。 IDebugHostSymbol2 / IDebugHostSymbol 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostSymbol2, IDebugHostSymbol)
{
    // 
    // IDebugHostSymbol:
    //
    STDMETHOD(GetContext)(_COM_Outptr_ IDebugHostContext** context) PURE;
    STDMETHOD(EnumerateChildren)(_In_ SymbolKind kind, _In_opt_z_ PCWSTR name, _Out_ IDebugHostSymbolEnumerator **ppEnum) PURE;
    STDMETHOD(GetSymbolKind)(_Out_ SymbolKind *kind) PURE;
    STDMETHOD(GetName)(_Out_ BSTR* symbolName) PURE;
    STDMETHOD(GetType)(_Out_ IDebugHostType** type) PURE;
    STDMETHOD(GetContainingModule)(_Out_ IDebugHostModule **containingModule) PURE;
    STDMETHOD(CompareAgainst)(_In_ IDebugHostSymbol *pComparisonSymbol, _In_ ULONG comparisonFlags, _Out_ bool *pMatches) PURE;
    //
    // IDebugHostSymbol2
    //
    STDMETHOD(EnumerateChildrenEx)(_In_ SymbolKind kind, _In_opt_z_ PCWSTR name, _In_opt_ SymbolSearchInfo* searchInfo, _Out_ IDebugHostSymbolEnumerator **ppEnum) PURE;
}
```

它是非常重要，需要注意此接口表示许多类型的符号-分隔由 SymbolKind 枚举具有值，如下所示： 

Enumarant | 含义
|--------------|------------------|
符号  | 未指定的符号类型 
SymbolModule | 符号是一个模块，可以查询的 IDebugHostModule
SymbolType | 符号类型，并可以查询的 IDebugHostType
SymbolField | 符号字段 （结构或类中的数据成员），并可以查询的 IDebugHostField
SymbolConstant | 符号的常量值，并可以查询的 IDebugHostConstant
SymbolData | 符号是这不是结构或类的成员，并且可为 IDebugHostData 查询数据
SymbolBaseClass | 符号的基类，并可为 IDebugHostBaseClass 查询
SymbolPublic | 符号 （具有无类型信息） 的模块的 publics 表中的条目，并可为 IDebugHostPublic 查询
SymbolFunction | 符号是函数，可为 IDebugHostData 查询

[GetContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbol-getcontext)

GetContext 方法返回的符号是有效的上下文。 而这将代表等存在符号的调试目标和进程/地址空间，可能不会从其他方法检索到的上下文的具体 (例如： 从*IModelObject*)。 

[EnumerateChildren](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostsymbol-enumeratechildren)

EnumerateChildren 方法返回的将枚举给定符号的所有子级的枚举器。 对于 c + + 类型，例如，基类、 字段中，成员函数和 like 是类型符号的所有被视为的子级。 


**模块接口：IDebugHostModule**

某些地址空间内加载的模块的调试器的概念在数据模型中的两个不同的方式表示：在通过 IDebugHostModule 接口的类型系统级别。 在这里，模块是一个符号和模块的核心属性包括接口方法调用计划的数据模型级别通过 Debugger.Models.Module 数据模型。 这是可扩展的类型系统模块的 IDebugHostModule 表示形式封装。

IDebugHostModule 接口定义，如下所示 （忽略是通用的 IDebugHostSymbol 的方法）： 

```cpp
DECLARE_INTERFACE_(IDebugHostModule, IDebugHostSymbol)
{
    //
    // IDebugHostModule:
    //
    STDMETHOD(GetImageName)(_In_ bool allowPath, _Out_ BSTR* imageName) PURE;
    STDMETHOD(GetBaseLocation)(_Out_ Location* moduleBaseLocation) PURE;
    STDMETHOD(GetVersion)(_Out_opt_ ULONG64* fileVersion, _Out_opt_ ULONG64* productVersion) PURE;
    STDMETHOD(FindTypeByName)(_In_z_ PCWSTR typeName, _Out_ IDebugHostType** type) PURE;
    STDMETHOD(FindSymbolByRVA)(_In_ ULONG64 rva, _Out_ IDebugHostSymbol** symbol) PURE;
    STDMETHOD(FindSymbolByName)(_In_z_ PCWSTR symbolName, _Out_ IDebugHostSymbol** symbol) PURE;
}
```

[GetImageName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-getimagename)

GetImageName 方法返回的模块的映像名称。 根据 allowPath 参数的值，返回的映像名称可能包含或不包含图像的完整路径。

[GetBaseLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-getbaselocation)

GetBaseLocation 方法作为位置结构返回该模块的基加载地址。 模块的返回的位置结构通常将引用的虚拟地址。

[GetVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-getversion)

GetVersion 方法返回 （假设此类信息能够成功读取带标头） 的模块的版本信息。 如果给定的版本请求 （通过非 nullptr 输出指针），且无法读取，则将从方法调用返回相应的错误代码。 

[FindTypeByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-findtypebyname)

FindTypeByName 方法查找由类型名称的模块中定义的类型，并为其返回类型符号。 此方法可能会返回有效 IDebugHostType 永远不会返回通过显式递归的子级的模块。 调试主机可能会允许创建派生类型--类型绝不要出现在模块本身内使用，但派生自的类型。 例如，如果结构 MyStruct 定义中的符号的模块，但类型 MyStruct * * 是从未使用过，FindTypeByName 方法可能合法地返回类型符号 MyStruct * * 尽管永远不会显式显示的符号在该类型名称该模块。 

[FindSymbolByRVA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-findsymbolbyrva)

FindSymbolByRVA 方法将查找单个匹配符号在模块内给定相对虚拟地址。 如果没有单一符号位于提供的 RVA (例如： 有多个匹配项)，此方法将返回错误。 请注意，此方法会更喜欢通过 publics 表中的符号返回私有符号。 

[FindSymbolByName](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodule-findsymbolbyname)

FindSymbolByName 方法将查找给定名称的模块中的单个全局符号。 如果不是单个符号与给定名称匹配，此方法将返回错误。 请注意，此方法会更喜欢通过 publics 表中的符号返回私有符号。 


**对类型系统的访问：IDebugHostType2 / IDebugHostType**

给定的语言/本机类型由 IDebugHostType2 或 IDebugHostType 接口描述。 请注意，这些接口上的方法的一些只适用于特定类型的类型。 给定的类型符号可能指以下类型之一如 TypeKind 枚举中所述： 

类型的种类 |  描述
|--------------|------------------|
TypeUDT | 用户定义类型 (结构、 类、 并集，等等...)。一个模型对象，它具有一个其类型为 TypeUDT 的本机类型具有的类型始终保留在相应 IModelObject ObjectTargetObject 的规范表示形式。
TypePointer | 一个指针。 一个模型对象，它具有一个其类型为 TypePointer 的本机类型具有的 ObjectIntrinsic 其中指针的值为零扩展到 VT_UI8 并保存为此 64 位窗体中的内部数据的规范表示形式。 TypePointer 任何类型符号有指针指向的类型的基类型 （作为由 GetBaseType 方法返回）。
TypeMemberPointer | 指向类成员的指针。 一个模型对象，它具有一个其类型为 TypeMemberPointer 的本机类型具有内部的规范表示形式 （正在指针值与相同的值）。 此值的确切含义是特定于编译器/调试主机。
TypeArray | 一个数组。 一个模型对象，它具有一个其类型为 TypeArray 的本机类型具有 ObjectTargetObject 的规范表示形式。 数组的基址是对象的位置 （通过 GetLocation 方法进行检索），始终会放置在数组的类型。 TypeArray 任何类型符号具有基类型 （作为由 GetBaseType 方法返回） 的数组的数组的类型。
TypeFunction | 一个函数。
TypeTypedef | Typedef。 模型对象具有其类型应 TypeTypedef 本机类型具有相同的最终基础 typedef 的类型的规范表示形式的规范表示形式。 这将显示对对象和类型信息的最终用户完全透明的除非 IDebugHostType2 的显式 typedef 方法利用查询 typedef 信息或针对 typedef 注册一个显式数据模型。 请注意，GetTypeKind 方法永远不会返回 TypeTypedef。 每个方法将返回最终基础 typedef 的类型将返回。 可用于获取 typedef 特定信息的 IDebugHostType2 上有 typedef 特定方法。
TypeEnum | 一个枚举。 一个模型对象，它具有一个其类型为 TypeEnum 的本机类型具有的 ObjectIntrinsic 值和类型的内部函数是相同类型的枚举值的规范表示形式。 
TypeIntrinsic | 内部 （基类型）。 一个模型对象，它具有一个其类型为 TypeIntrinsic 的本机类型具有 ObjectIntrinsic 的规范表示形式。 类型信息可能会或可能不保留-尤其是当基础类型完整描述了由变量数据类型 （| VT_ *） 的内部数据存储在 IModelObject

总体 IDebugHostType2 / IDebugHostType 接口 （不包括 IDebugHostSymbol 方法） 定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostType2, IDebugHostType)
{
    //
    // IDebugHostType:
    //
    STDMETHOD(GetTypeKind)(_Out_ TypeKind *kind) PURE;
    STDMETHOD(GetSize)(_Out_ ULONG64* size) PURE;
    STDMETHOD(GetBaseType)(_Out_ IDebugHostType** baseType) PURE;
    STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
    STDMETHOD(GetIntrinsicType)(_Out_opt_ IntrinsicKind *intrinsicKind, _Out_opt_ VARTYPE *carrierType) PURE;
    STDMETHOD(GetBitField)(_Out_ ULONG* lsbOfField, _Out_ ULONG* lengthOfField) PURE;
    STDMETHOD(GetPointerKind)(_Out_ PointerKind* pointerKind) PURE;
    STDMETHOD(GetMemberType)(_Out_ IDebugHostType** memberType) PURE;
    STDMETHOD(CreatePointerTo)(_In_ PointerKind kind, _COM_Outptr_ IDebugHostType** newType) PURE;
    STDMETHOD(GetArrayDimensionality)(_Out_ ULONG64* arrayDimensionality) PURE;
    STDMETHOD(GetArrayDimensions)(_In_ ULONG64 dimensions, _Out_writes_(dimensions) ArrayDimension *pDimensions) PURE;
    STDMETHOD(CreateArrayOf)(_In_ ULONG64 dimensions, _In_reads_(dimensions) ArrayDimension *pDimensions, _COM_Outptr_ IDebugHostType** newType) PURE;
    STDMETHOD(GetFunctionCallingConvention)(_Out_ CallingConventionKind* conventionKind) PURE;
    STDMETHOD(GetFunctionReturnType)(_COM_Outptr_ IDebugHostType** returnType) PURE;
    STDMETHOD(GetFunctionParameterTypeCount)(_Out_ ULONG64* count) PURE;
    STDMETHOD(GetFunctionParameterTypeAt)(_In_ ULONG64 i, _Out_ IDebugHostType** parameterType) PURE;
    STDMETHOD(IsGeneric)(_Out_ bool* isGeneric) PURE;
    STDMETHOD(GetGenericArgumentCount)(_Out_ ULONG64* argCount) PURE;
    STDMETHOD(GetGenericArgumentAt)(_In_ ULONG64 i, _Out_ IDebugHostSymbol** argument) PURE;
    //
    // IDebugHostType2:
    //
    STDMETHOD(IsTypedef)(_Out_ bool* isTypedef) PURE;
    STDMETHOD(GetTypedefBaseType)(_Out_ IDebugHostType2** baseType) PURE;
    STDMETHOD(GetTypedefFinalBaseType)(_Out_ IDebugHostType2** finalBaseType) PURE;
    STDMETHOD(GetFunctionVarArgsKind)(_Out_ VarArgsKind* varArgsKind) PURE;
}
```

**IDebugHostType2/IDebugHostType 常规方法**

下面的 IDebugHostType 方法是通用的任何类型，而不管 GetTypeKind 方法返回哪种类型： 

```cpp
STDMETHOD(GetTypeKind)(_Out_ TypeKind *kind) PURE;
STDMETHOD(GetSize)(_Out_ ULONG64* size) PURE;
STDMETHOD(GetBaseType)(_Out_ IDebugHostType** baseType) PURE;
STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
```

[GetTypeKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-gettypekind)

GetTypeKind 方法将返回哪种符号引用的类型 （指针，数组中，内部函数，等等）。 

[GetSize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getsize)

GetSize 方法返回类型的大小 （就像一个已经做 sizeof(type) c + + 中的）。 

[GetBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getbasetype)

如果类型为另一种类型的派生 (例如： 为 MyStruct * 派生自 MyStruct)，GetBaseType 方法返回的派生的基类型。 指针，这将返回指向的类型。 对于数组，这会返回什么数组是一个数组。 如果类型不是这样的派生类型，则返回错误。 

[GetHashCode](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-gethashcode)

GetHashCode 方法返回类型的 32 位哈希代码。 除了全局匹配 (例如： 等效于类型签名 * 可匹配所有内容如果允许主机)，任何类型实例可以匹配特定类型签名必须返回相同的哈希代码。 此方法是与类型签名结合使用以匹配类型签名以类型实例。 


**IDebugHostType2/IDebugHostType 内部方法**

以下 IDebugHostType 方法是特定于内部类型 （或保存内部数据，例如将枚举类型）： 

```cpp
STDMETHOD(GetIntrinsicType)(_Out_opt_ IntrinsicKind *intrinsicKind, _Out_opt_ VARTYPE *carrierType) PURE;
```

[GetIntrinsicType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getintrinsictype)

GetIntrinsicType 方法返回类型是哪种内部函数的信息。 此方法返回两个值： 

- 内部函数的类型指示总体类型 (例如： 整数，未签名，浮点数)，但不是类型的大小 (例如：8 位、 16 位、 32 位、 64 位）
- 运营商类型指示内部函数的类型如何到变体结构包。 这是一个 | VT_ * 常量。

两个值的组合提供了有关内部函数的信息的完整集。 


**IDebugHostType2/IDebugHostType 位域方法**

以下 IDebugHostType 方法是特定于数据存储在位域的类型。 有关内部函数内的位域布局的信息存储为数据模型，而不是位置的属性中的类型符号的一部分。 

```cpp
STDMETHOD(GetBitField)(_Out_ ULONG* lsbOfField, _Out_ ULONG* lengthOfField) PURE;
```

[GetBitField](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getbitfield)

如果给定的一种数据结构成员是位域 (例如：ULONG MyBits:8) 具有以来的字段的类型信息的位域布局信息。 GetBitField 方法可以用于检索该信息。 此方法将任何类型，这不是位域上失败。 这是该方法将失败的唯一原因。 只需调用此方法并查看成功/失败就足以区分非位域中的位字段。 如果确实发生给定的类型是一组标志，由半开放集定义字段位置 *(lsbOfField + lengthOfField: lsbOfField]*


**IDebugHostType2/IDebugHostType 指针相关方法**

以下 IDebugHostType 方法是特定于指针类型。 此类属于类型 GetTypeKind 在其中返回 TypePointer 或 TypeMemberPointer: 

```cpp
STDMETHOD(GetPointerKind)(_Out_ PointerKind* pointerKind) PURE;
STDMETHOD(GetMemberType)(_Out_ IDebugHostType** memberType) PURE;
```
[GetPointerKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getpointerkind)

对于类型，它们是指针，GetPointerKind 方法返回指针的类型。 这是由 PointerKind 枚举定义的。

[GetMemberType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getmembertype)

类型的指针到成员 （即 TypeMemberPointer 类型），GetMemberType 方法返回指针到成员的指针的类。 


**IDebugHostType2/IDebugHostType 数组相关的方法**

数组是其中 GetTypeKind 返回 TypeArray 类型。 请注意，数组定义由调试主机类型系统不是与单维相同、 基于零索引、 已打包线性一维数组，它利用 C。 C 样式数组放入该定义，但数组的整体范围更广泛 IDebugHostType 中。 调试主机中的数组可以是多维和每个维度的数组中定义的名为 ArrayDimensionThis 描述符包含以下字段的描述符： 



字段 | 含义
|--------------|------------------|
LowerBound | 为有符号的 64 位值数组的基索引。 对于 C 样式数组，这将始终为零。 它不需要。 数组的单个维度可被视为任何 64 位索引处开始，即使是-1。
长度 | 数组维度作为 64 位无符号值的长度。 数组的索引 s p a n 半开放集 [LowerBound、 LowerBound + 长度）。
Stride | 定义数组维度的步幅。 对于此维度的索引中的一个 （从 N 到 N + 1) 的增加，这指示继续推进工作内存中的字节数。 对于 C 样式数组，这将是数组的每个元素的大小。 它不需要为。 元素之间的填充量可表示为每个元素的大小大于跨距的值。 对于多维数组，此值将指示如何继续推进工作整个维度。 请考虑一个 M x N 矩阵。 这可能会被描述在行主窗体中为两个维度： 

```cpp   
{ [LowerBound: 0, Length: M, Stride: N \* sizeof(element)], [LowerBound: 0, Length: N, Stride: sizeof(element)]} 
```
也可能是也是作为两个维度的列主窗体中所述： 

```cpp   
{ [LowerBound: 0, Length: M, Stride: sizeof(element)], [LowerBound: 0, Length: N, Stride: M \* sizeof(element)]} 
```
ArrayDimension 概念允许这种程度的灵活性。 

以下 IDebugHostType 方法是特定于数组类型。 

```cpp
STDMETHOD(GetArrayDimensionality)(\_Out_ ULONG64\* arrayDimensionality) PURE; 
STDMETHOD(GetArrayDimensions)(\_In_ ULONG64 dimensions, \_Out_writes_(dimensions) ArrayDimension \*pDimensions) PURE;
```

[GetArrayDimensionality](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getarraydimensionality)

GetArrayDimensionality 方法返回数组索引中的维度的数。 对于 C 样式数组，将此处将始终为 1 返回的值。 

[GetArrayDimensions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getarraydimensions)

GetArrayDimensions 方法返回的描述符，一个用于如 GetArrayDimensionality 方法所指示的数组的每个维度的一组。 每个描述符是 ArrayDimension 结构描述的起始索引、 长度和正跨距的数组的每个维度。 这样，更为强大数组构造比允许 C 类型系统中的说明。 

为 C 样式数组的值始终是此处返回单个数组维度： 

- LowerBound = 0
- 长度 = ARRAYSIZE(array)
- Stride = sizeof(elementType)


**IDebugHostType2/IDebugHostType 函数相关方法**

这表示它们是通过一种类型的 TypeFunction 的函数类型的类型支持 IDebugHostType 和 IDebugHostType2 中的以下方法。 

```cpp
//
// IDebugHostType:
//
STDMETHOD(GetFunctionCallingConvention)(_Out_ CallingConventionKind* conventionKind) PURE;
STDMETHOD(GetFunctionReturnType)(_COM_Outptr_ IDebugHostType** returnType) PURE;
STDMETHOD(GetFunctionParameterTypeCount)(_Out_ ULONG64* count) PURE;
STDMETHOD(GetFunctionParameterTypeAt)(_In_ ULONG64 i, _Out_ IDebugHostType** parameterType) PURE;
//
// IDebugHostType2:
//
STDMETHOD(GetFunctionVarArgsKind)(_Out_ VarArgsKind* varArgsKind) PURE;
```

[GetFunctionCallingConvention](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getfunctioncallingconvention)

GetFunctionCallingConvention 方法将返回该函数的调用约定。 此类返回作为 CallingConventionKind 枚举的成员。 

[GetFunctionReturnType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionreturntype)

GetFunctionReturnType 方法将返回该函数的返回类型。 

[GetFunctionParameterTypeCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionparametertypecount)

GetFunctionParameterTypeCount 方法将返回该函数采用的参数数目。 请注意 C/c + + 省略号基于变量自变量标记不会被视为此计数中。 必须通过 GetFunctionVarArgsKind 方法来检测此类存在。 这将仅包括前省略号参数。 

[GetFunctionParameterTypeAt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionparametertypeat)

GetFunctionParameterTypeAt 方法返回到函数的第 i 个自变量的类型。 

GetFunctionVarArgsKind 方法将返回给定的函数使用变量参数列表，以及如果是这样，什么样式的自变量它利用。 通过按如下所示定义 VarArgsKind 枚举的成员定义这样的： 

 列举 | 含义
|---------|---------|
VarArgsNone | 函数不采用任何变量自变量。
VarArgsCStyle | 该函数是 C 样式 varargs 函数 (returnType （arg1、 arg2，...）)。报告的函数的参数数目不包括省略号参数。 在 GetFunctionParameterTypeCount 方法返回的参数数目后发生的任何变量自变量传递。


**IDebugHostType2 GetFunctionVarArgsKind**

GetFunctionVarArgsKind 方法将返回给定的函数使用变量参数列表，以及如果是这样，什么样式的自变量它利用。 通过按如下所示定义 VarArgsKind 枚举的成员定义这样的： 


**IDebugHostType2/IDebugHostType Typedef 相关方法**

这是一个 typedef 任何类型的行为就像的类型是最终基础 typedef 的类型。 这意味着，方法如 GetTypeKind 将指示该类型是其 typedef。 同样，GetBaseType 不会返回定义引用的类型。 而是将指示行为就如同它们被称为最终定义基础 typedef 上。 例如： 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```

有关 IDebugHostType PMYSTRUCT 或 PTRMYSTRUCT 将报告以下信息： 

- GetTypeKind 方法将返回 TypePointer。 最终基础类型 MYSTRUCT * 确实是一个指针。
- GetBaseType 方法将返回 MYSTRUCT 的一种类型。 MYSTRUCT 的基础类型 * 是 MYSTRUCT。

唯一的区别是对 IDebugHostType2 typedef 特定方法的行为方式。 这些方法包括： 

```cpp
STDMETHOD(IsTypedef)(_Out_ bool* isTypedef) PURE;
STDMETHOD(GetTypedefBaseType)(_Out_ IDebugHostType2** baseType) PURE;
STDMETHOD(GetTypedefFinalBaseType)(_Out_ IDebugHostType2** finalBaseType) PURE;
```

在本示例中： 

- PMYSTRUCT 和 PTRMYSTRUCT 的 IsTypedef 方法将返回 true
- GetTypedefBaseType 方法将返回 MYSTRUCT * PMYSTRUCT 和 PTRMYSTRUCT 的 PMYSTRUCT
- GetTypedefFinalBaseType 方法将返回 MYSTRUCT * 这两种类型

[IsTypedef](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype2-istypedef)

IsTypedef 方法是能够看到是否 typedef 类型的唯一方法。 GetTypeKind 方法将行为就如同在基础类型上调用。 

[GetTypedefBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype2-gettypedefbasetype)

GetTypedefBaseType 方法将返回直接定义的 typedef。 在文档中所述的示例： 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```
此方法将返回 MYSTRUCT * PMYSTRUCT 和 PTRMYSTRUCT 的 PMYSTRUCT。


[GetTypedefFinalBaseType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttype2-gettypedeffinalbasetype)

GetTypedefFinalBaseType 方法将返回的最后一个类型的 typedef 的定义。 如果 typedef 的另一个 typedef 定义，这将继续按照定义链，直到它达到这不是一个 typedef，并将返回类型的类型。 在文档中所述的示例： 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```

此方法将返回 MYSTRUCT * PMYSTRUCT 或 PTRMYSTRUCT 上调用时。 

**IDebugHostType2/IDebugHostType 类型创建方法**

```cpp
STDMETHOD(CreatePointerTo)(_In_ PointerKind kind, _COM_Outptr_ IDebugHostType** newType) PURE;
STDMETHOD(CreateArrayOf)(_In_ ULONG64 dimensions, _In_reads_(dimensions) ArrayDimension *pDimensions, _COM_Outptr_ IDebugHostType** newType) PURE;
```

**常量的符号的值：IDebugHostConstant**

有关常量值位于 （其中一个特定值是一个符号可能会也可能不是常量值） 的符号化信息的位置，IDebugHostConstant 接口表示此类常量的这一概念。 这通常用于与给定的参数位置通常是一种类型而可能是到非类型模板参数的模板自变量 (例如： 常量)。 

IDebugHostConstant 接口定义，如下所示 （忽略由 IDebugHostSymbol 实现的泛型方法）： 

```cpp
DECLARE_INTERFACE_(IDebugHostConstant, IDebugHostSymbol)
{
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostconstant-getvalue)

GetValue 方法返回打包到一个变量的常量的值。 请务必注意 IDebugHostSymbol GetType 方法可能会返回特定类型符号常量。 在这种情况下，没有无法保证常量值的装箱类型符号的定义是封装相同由此处的 GetValue 方法返回。 


**数据成员访问：IDebugHostField**

IDebugHostField 类表示符号，后者是一个类、 结构、 联合或其他类型的构造的数据成员。 它不表示的免费数据 (例如： 全局数据)。 接口定义，如下所示 （忽略 IDebugHostSymbol 到泛型方法）： 

```cpp
DECLARE_INTERFACE_(IDebugHostField, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetOffset)(_Out_ ULONG64* offset) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostfield-getlocationkind)

GetLocationKind 方法返回何种符号位于的位置根据 LocationKind 枚举。 此类枚举可以是下列值之一： 

列举 | 含义
|---------|--------|
LocationMember | 该字段是常规数据成员的类、 结构、 联合或其他类型的构造。 它必须是相对于包含的类型构造的基址的偏移量。 这通常表示此类的基址指针。 可以通过 GetOffset 方法检索的字段偏移量。 GetLocation 和 GetValue 方法即 LocationMember 字段将会失败。
LocationStatic | 该字段是静态的并具有其自己的地址。 GetLocation 方法将返回的抽象的位置 (例如： 地址) 的静态字段。 GetOffset 和 GetValue 方法即 LocationStatic 字段将会失败。
LocationConstant | 该字段是一个常量，并且具有值。 GetValue 方法将返回常量的值。 GetOffset 和 GetLocation 方法将失败的字段可能是 LocationConstant
LocationNone | 该字段具有任何位置。 它可能已经过优化，缩小由编译器也可能是其声明，但是永远不会定义一个静态字段。 此类字段是如何为，无论有没有物理访问或值。 它是仅在符号中。 所有采集方法 （GetOffset、 GetLocation 和 GetValue） 时即 LocationNone 字段将都失败。

[GetOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostfield-getoffset)

字段的偏移量 (例如： 字段的位置类型表明 LocationMember)，GetOffset 方法将返回的偏移量，从包含类型的基址 (此指针) 到字段本身的数据。 此类的偏移量始终表示为无符号 64 位值。 如果给定的字段不具有这是从包含类型的基址的偏移量的位置，GetOffset 方法将失败。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostfield-getlocation)

有一个地址而不考虑特定类型实例的字段 (例如： 字段的位置类型表明 LocationStatic)，GetLocation 方法将返回该字段的抽象位置 （地址）。 如果给定的字段不具有静态位置，则 GetLocation 方法将失败。 

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostfield-getvalue)

有符号化信息中定义的常量值的字段 (例如： 字段的位置类型表明 LocationConstant)，GetValue 方法将返回该字段的常量值。 如果给定的字段不具有常量值，则 GetValue 方法将失败。 


**可用的数据访问：IDebugHostData**

在模块中的数据，这不是另一种类型的成员由 IDebugHostData 接口表示。 该接口定义，如下所示 （忽略 IDebugHostSymbol 到泛型方法）： 

```cpp
DECLARE_INTERFACE_(IDebugHostData, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

所有这些方法都是语义上等效于 IDebugHostField 中其匹配。 唯一的区别是 GetLocationKind 方法将永远不会返回可用数据 LocationMember。 

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostdata-getlocationkind)

GetLocationKind 方法返回何种符号位于的位置根据 LocationKind 枚举。 此枚举的说明，可以找到有关 IDebugHostField 的文档中。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostdata-getlocation)

对于具有地址的数据，GetLocation 方法将返回该字段的抽象位置 （地址）。 如果给定的数据不具有静态位置，则 GetLocation 方法将失败。 

[GetValue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostdata-getvalue)

Datawhich 的符号化信息中定义的常量值 (例如： 数据的位置类型表明 LocationConstant)，GetValue 方法将返回该字段的常量值。 如果给定的数据不具有常量值，则 GetValue 方法将失败。 


**基类：IDebugHostBaseClass**

给定类型的继承层次结构被表示为类型符号的子级。 如果给定的类型从一个或多个类型派生 (继承 wise)，将有一个或多个 SymbolBaseClass 子级的类型符号的类型。 每个这些 SymbolBaseClass 符号表示从特定类型直接继承。 基类的名称是 SymbolBaseClass 符号名称以及的基本类的类型符号。 SymbolBaseClass 符号 GetType 方法可用于获取类型符号自身的基类。 可以按探索 SymbolBaseClass 子符号以递归方式遍历的完整的继承层次结构。 每个这些基类符号通过 IDebugHostBaseClass 接口定义，如下所示 （忽略 IDebugHostSymbol 到泛型方法） 来表示： 

```cpp
DECLARE_INTERFACE_(IDebugHostBaseClass, IDebugHostSymbol)
{
    STDMETHOD(GetOffset)(_Out_ ULONG64* offset) PURE;
}
```

[GetOffset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostbaseclass-getoffset)

GetOffset 方法返回从派生类的基址的基类的偏移量。 此类偏移量可以为零，或者可能正的 64 位无符号的值。 


**公共符号：IDebugHostPublic**

公共符号表示符号文件中的公共表中的内容。 它们实际上是，导出地址。 没有类型信息与公共 symbol--仅一个地址相关联。 除非调用方显式请求一个公共符号时，调试主机可以优先选择要返回的每个查询的私有符号。 通过 IDebugHostPublic 接口定义，如下所示 （忽略是通用的 IDebugHostSymbol 方法） 来表示公共符号： 

```cpp
DECLARE_INTERFACE_(IDebugHostPublic, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
}
```

所有这些方法都是语义上等效于 IDebugHostField 中其匹配。 唯一的区别是，GetLocationKind 方法将永远不会返回 LocationMember 或 LocationConstant 此类符号。 

[GetLocationKind](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostpublic-getlocationkind)

GetLocationKind 方法返回何种符号位于的位置根据 LocationKind 枚举。 此枚举的说明，可以找到有关 IDebugHostField 的文档中。 

[GetLocation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostpublic-getlocation)

对于具有地址的数据，GetLocation 方法将返回该字段的抽象位置 （地址）。 如果给定的公钥不具有静态位置，则 GetLocation 方法将失败。 


**模块签名和版本匹配：IDebugHostModuleSignature**

模块签名表示一种方法来检查给定的模块是否符合一组有关命名和版本控制的条件。 通过在 IDebugHostSymbols CreateModuleSignature 方法创建模块签名。 它可以与匹配的模块名称和版本号的模块的可选范围。 一旦创建此类的签名，客户端收到 IDebugHostModuleSignature 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostModuleSignature, IUnknown)
{
    STDMETHOD(IsMatch)(_In_ IDebugHostModule* pModule, _Out_ bool* isMatch) PURE;
}
```

[IsMatch](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughostmodulesignature-ismatch)

IsMatch 方法将针对一个签名，模块名称和签名中指定的名称和版本范围的版本比较 （作为给定 IDebugHostModule 符号） 为特定模块进行比较。 返回表示给定的模块符号是否与签名匹配。 

**类型签名和类型匹配：IDebugHostTypeSignature**

类型签名表示一种方法来检查给定的类型实例是否满足一组有关的类型名称、 类型和该类型位于中的模块的泛型参数的条件。 通过在 IDebugHostSymbols CreateTypeSignature 方法创建类型签名。 一旦创建此类的签名，客户端收到 IDebugHostTypeSignature 接口定义，如下所示： 

```cpp
DECLARE_INTERFACE_(IDebugHostTypeSignature, IUnknown)
{
    STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
    STDMETHOD(IsMatch)(_In_ IDebugHostType* type, _Out_ bool* isMatch, _COM_Outptr_opt_ IDebugHostSymbolEnumerator** wildcardMatches) PURE;
    STDMETHOD(CompareAgainst)(_In_ IDebugHostTypeSignature* typeSignature, _Out_ SignatureComparison* result) PURE;
}
```

[GetHashCode](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttypesignature-gethashcode)

GetHashCode 方法返回类型签名的 32 位哈希代码。 调试主机保证在实现中返回的类型实例的哈希代码和返回类型签名的哈希代码之间的同步。 除了全局匹配项，如果类型实例能够支持的匹配类型签名中，都将具有相同的 32 位哈希代码。 这允许初始快速比较和匹配的类型实例和大量的数据模型管理器中注册的类型签名。 

[IsMatch](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttypesignature-ismatch)

IsMatch 方法返回的特定类型实例是否与指定类型签名中的条件匹配的指示。 如果是这样，相对值的指示这被返回及的枚举器将指示所有类型实例 （作为符号） 的匹配类型签名中的通配符的特定部分。 

[CompareAgainst](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nf-dbgmodel-idebughosttypesignature-compareagainst)

CompareAgainst 方法比较到另一个类型签名的类型签名并返回两个签名的进行比较。 返回比较结果是，如下所示定义 SignatureComparison 枚举的成员： 

列举 | 含义
|---------|-----------|
不相关 | 没有任何两个签名或要比较的类型之间的关系。
不明确 |一个签名或类型对其他比较不明确。 对于两个类型签名，这意味着有潜在的类型实例可以匹配任一签名很有效。 例如，如下所示的两个类型签名会引起歧义。  签名 1:`std::pair<*, int>`  签名 2:`std::pair<int,*>`因为类型实例`std::pair<int, int>`匹配两者中任何一个同样好 （它们都具有一个具体和一个通配符匹配）。
LessSpecific | 不太具体比另一个签名或类型。 通常情况下，这意味着更具体的签名包含一个通配符的更具体的一个其中有具体的类型。 例如，下面的第一个签名是更具体的第二个。 签名 1:`std::pair<*, int>` 签名 2:`std::pair<int, int>`因为它包含一个通配符 ( `*`)，第二个具体类型 (int)。
MoreSpecific | 一个签名或类型是比其他更具体。 通常情况下，这意味着更具体的签名具有一个具体类型的更具体的一个其中包含一个通配符。 例如，下面的第一个签名是第二个更具体。 签名 1:`std::pair<int, int>` 签名 2:`std::pair<*, int>`因为它有一个具体类型 (int) 第二个其中包含一个通配符 ( `*`)。
相同 | 两个签名或类型是相同的。







---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[调试程序数据模型 c + + 概述](data-model-cpp-overview.md)

[调试器数据模型 c + + 接口](data-model-cpp-interfaces.md)

[调试器数据模型 c + + 对象](data-model-cpp-objects.md)

[调试器数据模型 c + + 其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 c + + 概念](data-model-cpp-concepts.md)

[C + + 编写脚本的调试程序数据模型](data-model-cpp-scripting.md)
