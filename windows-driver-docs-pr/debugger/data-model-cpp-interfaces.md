---
title: 调试器数据模型 C++ 接口
description: 本主题介绍如何使用调试器数据模型 c + + 接口来扩展和自定义调试器的功能。
ms.date: 10/08/2018
ms.openlocfilehash: ffa122d2d8d641f80943bc0f15a8d9c247844360
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212597"
---
# <a name="debugger-data-model-c-interfaces"></a>调试器数据模型 C++ 接口 

本主题提供了有关如何使用调试器数据模型 c + + 接口来扩展和自定义调试器功能的概述。

## <a name="span-idhostinterfacespan-debugger-data-model-c-host-interfaces"></a><span id="hostinterface"></span> 调试器数据模型 c + + 主机接口

**调试器数据模型主机**

调试器数据模型设计为可在各种不同的上下文中托管的组件化系统。 通常情况下，数据模型承载于调试器应用程序的上下文中。 为了使其成为数据模型的宿主，需要实现多个接口以公开调试器的核心方面：其目标、其内存空间、计算器、符号和类型系统等。尽管这些接口是由任何希望承载数据模型的应用程序实现的，但核心数据模型和与数据模型互操作的任何扩展都将使用这些接口。 

核心接口集包括： 

接口名称 | 说明
|--------------|---------------|
IDebugHost | 调试宿主的核心接口。
IDebugHostStatus  | 允许客户端查询主机状态的接口。
IDebugHostContext  | 主机内上下文的抽象 (例如：特定目标、特定进程、特定地址空间等。) 
IDebugHostErrorSink  | 由调用方实现的接口，用于接收来自主机和数据模型的某些部分的错误
IDebugHostEvaluator / IDebugHostEvaluator2  | 调试宿主的表达式计算器。
IDebugHostExtensibility  | 用于扩展主机或其部分功能 (例如表达式计算器) 的接口。

类型系统接口和符号接口为： 

InterfaceName | 说明
|--------------|---------------|
IDebugHostSymbols | 提供对符号的访问和解析的核心接口
IDebugHostSymbol / IDebugHostSymbol2  | 表示任意类型的单个符号。 特定符号是此接口的派生。
IDebugHostModule | 表示在进程中加载的模块。 这是一种符号。
IDebugHostType / IDebugHostType2  | 表示本机/语言类型。
IDebugHostConstant  | 表示符号信息中的常量 (例如： c + + 中的非类型模板参数) 
IDebugHostField  | 表示结构或类中的字段。
IDebugHostData | 表示模块中的数据 (在结构或类中是 IDebugHostField) 
IDebugHostBaseClass | 表示基类。
IDebugHostPublic  | 表示 PDB 的 publics 表中的符号。 这不具有与其关联的类型信息。 它是一个名称和地址。
IDebugHostModuleSignature | 表示一个模块签名，该定义将按名称和/或版本匹配一组模块
IDebugHostTypeSignature | 表示一个类型签名-一种定义，该定义将按模块和/或名称匹配一组类型


**核心主机接口： IDebugHost**

IDebugHost 接口是任何数据模型主机的核心接口。 它的定义如下： 

```cpp
DECLARE_INTERFACE_(IDebugHost, IUnknown)
{
    STDMETHOD(GetHostDefinedInterface)(_COM_Outptr_ IUnknown** hostUnk) PURE;
    STDMETHOD(GetCurrentContext)(_COM_Outptr_ IDebugHostContext** context) PURE;
    STDMETHOD(GetDefaultMetadata)(_COM_Outptr_ IKeyStore** defaultMetadataStore) PURE;
}
```

[GetHostDefinedInterface](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughost-gethostdefinedinterface)

如果给定主机存在，GetHostDefinedInterface 方法将返回宿主的主专用接口。 对于适用于 Windows 的调试工具，此处返回的接口是 IDebugClient (强制转换为 IUnknown) 。 

[GetCurrentContext](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughost-getcurrentcontext)

GetCurrentContext 方法返回一个接口，该接口表示调试器主机的当前状态。 这种情况的确切含义是留给主机，但它通常包括在调试宿主的用户界面中处于活动状态的会话、进程和地址空间等内容。 返回的上下文对象在很大程度上对调用方是不透明的，但它是在对调试宿主的调用之间传递的重要对象。 例如，当调用方为读取内存时，必须知道要从中读取内存的进程和地址空间。 此概念封装在从此方法返回的上下文对象的概念中。 

[GetDefaultMetadata](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughost-getdefaultmetadata)

GetDefaultMetadata 方法返回一个默认的元数据存储区，该存储可用于某些操作 (例如：未传递显式元数据时) 字符串转换。 这样，调试宿主便可以控制某些数据的显示方式。 例如，默认的元数据可能包含一个 PreferredRadix 键，这允许宿主指示序号应以十进制还是十六进制显示（如果没有另外指定）。 

请注意，必须手动解析默认元数据存储区上的属性值，并且必须传递要查询其默认元数据的对象。 应使用 GetKey 方法代替 GetKeyValue。 

**状态接口： IDebugHostStatus** 

IDebugHostStatus 接口允许数据模型或调试宿主的客户端查询调试宿主状态的某些方面。 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IDebugHostStatus, IUnknown)
{
    STDMETHOD(PollUserInterrupt)(_Out_ bool* interruptRequested) PURE;
}
```

[PollUserInterrupt](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughoststatus-polluserinterrupt)

PollUserInterrupt 方法用于查询调试宿主的用户是否请求了当前操作的中断。 例如，数据模型中的属性访问器可能会调用任意代码 (例如： JavaScript 方法) 。 该代码可能需要任意一段时间。 为了保持调试宿主的响应能力，任何可能需要花费任意时间的此类代码都应该通过调用此方法来检查中断请求。 如果 interruptRequested 值返回为 true，则调用方应立即中止并返回 E_ABORT 的结果。 


**上下文接口： IDebugHostContext**

上下文是数据模型和基础调试宿主最重要的方面之一。 当你保存某个对象时，必须能够知道对象的来源是什么，它是哪个进程，它与哪个地址空间相关联。 如果知道此信息，则可以正确解释指针值之类的内容。 必须将类型为 IDebugHostContext 的对象传递给调试主机上的多个方法。 可以通过多种方式获取此接口：

- 通过获取调试器的当前上下文：调用 IDebugHost 的 GetCurrentContext 方法
- 通过获取对象的上下文：调用 IModelObject 的 GetContext 方法
- 通过获取符号的上下文：调用 IDebugHostSymbol 的 GetContext 方法

此外，还存在两个值，这两个值在 IDebugHostContext 接口的上下文中具有特殊意义，此接口既可以从返回，也可以传递给数据模型或调试主机方法： 

*nullptr*：指示没有上下文。 对于某些对象，如果没有上下文，则完全有效。 数据模型的根命名空间中的调试器对象不是指特定进程或地址空间内的任何内容。 它没有上下文。

*USE_CURRENT_HOST_CONTEXT*：指示应使用调试宿主的当前 UI 上下文的 sentinel 值。 此值永远不会从调试主机返回。 但是，它可能会传递到任何调试主机方法，该方法采用输入 IDebugHostContext，而不是显式调用 IDebugHost 的 GetCurrentContext 方法。 请注意，显式传递 USE_CURRENT_HOST_CONTEXT 通常比显式获取当前上下文的性能更高。 

宿主上下文的上下文在很大程度上对调用方是不透明的。 核心调试主机外部的调用方可以对宿主上下文执行的唯一操作是将其与另一个主机上下文进行比较。 

IDebugHostContext 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IDebugHostContext, IUnknown)
{
    STDMETHOD(IsEqualTo)(_In_ IDebugHostContext *pContext, _Out_ bool *pIsEqual) PURE;
}
```

[IsEqualTo](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostcontext-isequalto)

IsEqualTo 方法将宿主上下文与其他宿主上下文进行比较。 如果两个上下文相等，则返回此的指示。 请注意，此比较不是接口等效性。 这比较了上下文本身的根本不透明内容。 


**错误接收器： IDebugHostErrorSink**

IDebugHostErrorSink 是一种方法，通过该方法，客户端可以接收特定操作期间发生的错误的通知，并在需要时路由这些错误。 接口定义如下： 

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

[ReportError](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosterrorsink-reporterror)

ReportError 方法是错误接收器上的回调，用于通知其已发生错误，并允许接收器将错误路由到任何合适的 UI 或机制。 


**主机计算器： IDebugHostEvaluator/IDebugHostEvaluator2**

调试宿主向客户端提供的最重要功能之一是可以访问其基于语言的表达式计算器。 IDebugHostEvaluator 和 IDebugHostEvaluator2 接口是从调试宿主访问该功能的方法。 

接口定义如下： 

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

[EvaluateExpression](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostevaluator-evaluateexpression)

EvaluateExpression 方法允许请求调试宿主计算语言 (例如： c + +) 表达式，并将该表达式求值的结果值作为 IModelObject 返回。 此方法的这一特定变体仅允许语言构造。 在调试宿主的表达式计算器内显示的任何其他功能，这些功能在语言 (例如： LINQ query 方法) 对于计算是关闭的。 

[EvaluateExtendedExpression](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostevaluator-evaluateextendedexpression)

EvaluateExtendedExpression 方法类似于 EvaluateExpression 方法，不同之处在于，它会返回特定调试宿主选择要添加到其表达式计算器的其他非语言功能。 例如，对于用于 Windows 的调试工具，这将启用匿名类型、LINQ 查询、模块限定符、格式说明符和其他非 C/c + + 功能。 


**IDebugHostEvaluator2**

[AssignTo](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostevaluator2-assignto)

AssignTo 方法根据正在调试的语言的语义执行赋值。 


**主机扩展性接口： IDebugHostExtensibility**

调试主机的某些功能可选择性地服从可扩展性。 例如，这可能包括表达式计算器。 IDebugHostExtensibility 接口是访问这些扩展点的方法。 接口定义如下： 

```cpp
DECLARE_INTERFACE_(IDebugHostExtensibility, IUnknown)
{
    STDMETHOD(CreateFunctionAlias)(_In_ PCWSTR aliasName, _In_ IModelObject *functionObject) PURE;
    STDMETHOD(DestroyFunctionAlias)(_In_ PCWSTR aliasName) PURE;
}
```

[CreateFunctionAlias](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostextensibility-createfunctionalias)

CreateFunctionAlias 方法为某些扩展中实现的方法创建 "函数别名"、"快速别名"。 此别名的含义是主机特定的。 它可以通过函数扩展主机的表达式计算器，或执行完全不同的操作。 

[DestroyFunctionAlias](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostextensibility-destroyfunctionalias)

DestroyFunctionAlias 方法撤消之前对 CreateFunctionAlias 方法的调用。 该函数将在 "快速别名" 下不再可用。 



## <a name="span-idaccessdatamodel-accessing-the-data-model"></a><span id="accessdatamodel"> 访问数据模型

首先，数据模型扩展性 Api 被设计为对应用程序而言是非特定的 (通常是用作数据模型主机的调试器) 。 从理论上讲，任何应用程序都可以通过提供一组主机 Api 来承载数据模型，该程序集将应用程序的调试目标的类型系统公开 () ，并将一组投影对象公开到数据模型的命名空间中，以了解目标、进程、线程等。位于这些调试目标 () 。 

数据模型 Api （即开始 IDataModel<em>、IDebugHost</em>和 Offshoots of IModelObject 的 api）的设计是可移植的，它们不会定义 "调试器扩展" 的含义。 目前，希望扩展 Windows 的调试工具和它所提供的引擎的组件必须编写引擎扩展，才能访问数据模型。 该引擎扩展只需作为中的引擎扩展，就是扩展的加载和启动机制。 因此，最小实现将提供： 

- **DebugExtensionInitialize**：一种方法，该方法利用创建的 IDebugClient 获取对数据模型的访问权限并设置对象模型操作。
- **DebugExtensionUninitialize**：一种方法，该方法撤消在 DebugExtensionInitialize 中执行的对象模型操作。
- **DebugExtensionCanUnload**：返回是否可以卸载扩展的方法。 如果扩展中仍存在活动的 COM 对象，则它必须指示这一点。 这是调试器等效于 COM 的 DllCanUnloadNow。 如果此方法返回无法卸载的 S_FALSE 指示，则调试器可以稍后对此进行查询，以查看卸载是否安全，或者是否可以通过再次调用 DebugExtensionInitialize 来重新初始化扩展。 扩展必须准备好处理这两个路径。
- **DebugExtensionUnload**：一种方法，该方法在 DLL 卸载之前执行所需的任何最终清理操作

*桥接口： IHostDataModelAccess*

如前所述，在调用 DebugExtensionInitialize 时，它将创建调试客户端并获取对数据模型的访问权限。 此类访问由用于 Windows 调试工具和数据模型的旧式 IDebug * 接口之间的桥接口提供。 此桥接接口为 "IHostDataModelAccess"，定义如下： 

```cpp
DECLARE_INTERFACE_(IHostDataModelAccess, IUnknown)
{
   STDMETHOD(GetDataModel)(_COM_Outptr_ IDataModelManager** manager, _COM_Outptr_ IDebugHost** host) PURE;
}
```

[GetDataModel](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-ihostdatamodelaccess-getdatamodel)

GetDataModel 方法是桥接口上的方法，该方法提供对数据模型两侧的访问：调试宿主 (调试器的下边缘) 由返回的 IDebugHost 接口表示数据模型的主组件，数据模型管理器由返回的 IDataModelManager 接口表示



## <a name="span-idsysteminterfacesspan-debugger-data-model-system-interfaces"></a><span id="systeminterfaces"></span> 调试器数据模型系统接口

**数据模型主机**

调试器数据模型设计为可在各种不同的上下文中托管的组件化系统。 通常情况下，数据模型承载于调试器应用程序的上下文中。 为了使其成为数据模型的宿主，需要实现多个接口以公开调试器的核心方面：其目标、其内存空间、计算器、符号和类型系统等。尽管这些接口是由任何希望承载数据模型的应用程序实现的，但核心数据模型和与数据模型互操作的任何扩展都将使用这些接口。 

类型系统接口和符号接口为： 


接口名称 | 说明
|--------------|------------------|
IDebugHostSymbols  | 提供对符号的访问和解析的核心接口
IDebugHostSymbol / IDebugHostSymbol2  | 表示任意类型的单个符号。 特定符号是此接口的派生。
IDebugHostModule  | 表示在进程中加载的模块。 这是一种符号。
IDebugHostType / IDebugHostType2  | 表示本机/语言类型。
IDebugHostConstant  | 表示符号信息中的常量 (例如： c + + 中的非类型模板参数) 
IDebugHostField | 表示结构或类中的字段。
IDebugHostData | 表示模块中的数据 (在结构或类中是 IDebugHostField) 
IDebugHostBaseClass  | 表示基类。
IDebugHostPublic | 表示 PDB 的 publics 表中的符号。 这不具有与其关联的类型信息。 它是一个名称和地址。
IDebugHostModuleSignature | 表示一个模块签名，该定义将按名称和/或版本匹配一组模块
IDebugHostTypeSignature | 表示一个类型签名-一种定义，该定义将按模块和/或名称匹配一组类型

其他核心接口包括： 

接口名称 | 说明
|--------------|------------------|
IDebugHost | 调试宿主的核心接口。
IDebugHostStatus | 允许客户端查询主机状态的接口。
IDebugHostContext | 主机内上下文的抽象 (例如：特定目标、特定进程、特定地址空间等。) 
IDebugHostErrorSink | 由调用方实现的接口，用于接收来自主机和数据模型的某些部分的错误
IDebugHostEvaluator / IDebugHostEvaluator2 | 调试宿主的表达式计算器。
IDebugHostExtensibility | 用于扩展主机或其部分功能 (例如表达式计算器) 的接口。


**主符号接口： IDebugHostSymbols**

IDebugHostSymbols 接口是在调试目标中访问符号的主要起点。 此接口可以从 IDebugHost 的实例查询，并定义如下： 

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

[CreateModuleSignature](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-createmodulesignature)

CreateModuleSignature 方法将创建一个签名，该签名可用于按名称和（可选）按版本匹配一组特定模块。 模块签名有三个组件： 

- 名称：匹配的模块的名称必须与签名中的名称完全不区分大小写匹配
- 最低版本：如果已指定，匹配模块的最低版本必须至少为此版本。 版本是以 "A. B. D" 格式指定的，每个后续部分的重要性比以前的更重要。 只有第一个段是必需的。
- 最高版本：如果指定了匹配的模块，则该模块的最大版本必须高于此版本。 版本是以 "A. B. D" 格式指定的，每个后续部分的重要性比以前的更重要。 只有第一个段是必需的。

[CreateTypeSignature](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-createtypesignature)

CreateTypeSignature 方法创建一个签名，该签名可用于通过包含模块和类型名称来匹配一组具体类型。 类型名称签名字符串的格式特定于正在 (和调试宿主) 调试的语言。 对于 C/c + +，签名字符串等效于 NatVis 类型规范。 也就是说，签名字符串是类型名称，其中 (将通配符指定为 * ) 以便用于模板参数。 

[CreateTypeSignatureForModuleRange](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-createtypesignatureformodulerange)

CreateTypeSignatureForModuleRange 方法创建一个签名，该签名可用于按模块签名和类型名称匹配一组具体类型。 这类似于 CreateTypeSignature 方法只不过，而不是传递特定模块以使其与签名匹配，调用方传递创建模块签名所需的参数， (就像使用 CreateModuleSignature 方法) 创建模块签名一样。 

[EnumerateModules](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-enumeratemodules)

EnumerateModules 方法创建一个枚举器，用于枚举特定主机上下文中提供的每个模块。 该主机上下文可能会封装一个进程上下文，或者它可能封装类似于 Windows 内核的内容。 


[FindModuleByName](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-findmodulebyname)

FindModuleByName 方法将遍历给定的宿主上下文，并找到具有指定名称的模块，并向其返回接口。 使用或不使用文件扩展名按名称搜索模块是合法的。 

[FindModuleByLocation](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-findmodulebylocation)

FindModuleByLocation 方法将遍历给定的主机上下文，并确定哪个模块包含指定位置给定的地址。 然后，它将返回此类模块的接口。 

[GetMostDerivedObject](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbols-getmostderivedobject)

GetMostDerivedObject 将使用调试器的类型系统从其静态类型确定对象的运行时类型。 此方法将仅使用类型系统层上提供的符号信息和试探法来执行此分析。 此类信息可能包括 c + + RTTI (运行时类型信息) 或分析对象的虚函数表的形状。 它不包括 IModelObject 上首选的运行时类型的概念。 如果分析找不到运行时类型或找不到与传入方法的静态类型不同的运行时类型，则可能会传递输入位置和类型。由于这些原因，方法不会失败。 



**核心单独的符号接口： IDebugHostSymbol**

可以从数据模型主机返回的每个符号将以某种方式从 IDebugHostSymbol 派生。 这是每个符号实现的核心接口，与符号类型无关。 根据符号的类型，给定的符号可以实现一组其他接口，这些接口可返回属性，这些属性对于此接口所表示的特定类型的符号更为独特。 IDebugHostSymbol2/IDebugHostSymbol 接口定义如下： 

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

需要注意的是，此接口表示许多类型的符号，其中包含的值如下所示： 

Enumarant | 含义
|--------------|------------------|
符号  | 未指定的符号类型 
SymbolModule | 此符号是一个模块，可以查询 IDebugHostModule
SymbolType | 符号为类型，可查询 IDebugHostType
SymbolField | 符号是结构或类) 中的数据成员 (的字段，可以查询 IDebugHostField
SymbolConstant | 此符号是一个常数值，可对 IDebugHostConstant 进行查询
SymbolData | 符号是不是结构或类的成员并且可查询 IDebugHostData 的数据
SymbolBaseClass | 符号是一个基类，可用于 IDebugHostBaseClass
SymbolPublic | 符号是模块的 publics 表中的项， (不) 类型信息，并且可查询 IDebugHostPublic
SymbolFunction | 符号是一个函数，可用于 IDebugHostData

[GetContext](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbol-getcontext)

GetContext 方法返回符号有效的上下文。 尽管这会显示符号所在的调试目标和进程/地址空间等内容，但它可能不会与从其他方法检索的上下文具体 (例如：从 *IModelObject*) 。 

[EnumerateChildren](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostsymbol-enumeratechildren)

EnumerateChildren 方法返回一个枚举器，该枚举器枚举给定符号的所有子级。 例如，对于 c + + 类型，基类、字段、成员函数和 like 都属于类型符号的所有子元素。 


**模块接口： IDebugHostModule**

调试器在某个地址空间内加载的模块的概念以两种不同的方式在数据模型中以两种不同的方式表示：通过 IDebugHostModule 接口在类型系统级别。 此处，模块是模块的符号和核心属性，它是通过调试程序在数据模型级别投影的接口方法调用。 这是模块的类型系统 IDebugHostModule 表示形式的可扩展封装。

IDebugHostModule 接口定义如下 (忽略 IDebugHostSymbol 的泛型方法) ： 

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

[GetImageName](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-getimagename)

GetImageName 方法返回模块的映像名称。 根据 allowPath 参数的值，返回的映像名称可能包含图像的完整路径，也可能不包含。

[GetBaseLocation](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-getbaselocation)

GetBaseLocation 方法将模块的基加载地址作为位置结构返回。 模块的返回位置结构通常会引用虚拟地址。

[GetVersion](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-getversion)

GetVersion 方法返回有关模块的版本信息， (假设此类信息可以从标头中读取) 。 如果 (通过非 nullptr 输出指针请求给定版本) 并且无法读取该版本，则方法调用将返回相应的错误代码。 

[FindTypeByName](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-findtypebyname)

FindTypeByName 方法查找在模块内按类型名称定义的类型，并返回该类型的类型符号。 此方法可能会返回有效的 IDebugHostType，这永远不会通过模块子级的显式递归返回。 调试宿主可能允许创建派生类型--在模块本身中未使用过类型，但派生自类型。 例如，如果结构 Mystruct>) 是在模块的符号中定义的，但从未使用过类型 Mystruct>) * *，则 FindTypeByName 方法可能会合法返回 Mystruct>) * * 的类型符号，因为该类型名称永远不会显式显示在模块的符号中。 

[FindSymbolByRVA](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-findsymbolbyrva)

FindSymbolByRVA 方法将在模块内的给定相对虚拟地址处找到单个匹配的符号。 如果提供的 RVA (上没有单个符号（例如：有多个匹配项) ，则此方法将返回错误。 请注意，此方法将优先于 publics 表中的符号返回私有符号。 

[FindSymbolByName](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodule-findsymbolbyname)

FindSymbolByName 方法将在模块中找到具有给定名称的单一全局符号。 如果不存在与给定名称匹配的单个符号，则此方法将返回错误。 请注意，此方法将优先于 publics 表中的符号返回私有符号。 


**访问类型系统： IDebugHostType2/IDebugHostType**

给定语言/本机类型由 IDebugHostType2 或 IDebugHostType 接口描述。 请注意，这些接口上的某些方法仅适用于特定类型的类型。 给定的类型符号可以引用以下类型之一，如 TypeKind 枚举所述： 

类型种类 |  说明
|--------------|------------------|
TypeUDT |  (结构、类、联合等的用户定义类型 .。。) 。具有类型为 TypeUDT 的本机类型的模型对象具有规范的规范表示形式，其中类型始终保留在相应的 IModelObject 中。
TypePointer | 一个指针。 如果模型对象的类型为 TypePointer 的本机类型为类型为 "" 的类型为 "ObjectIntrinsic" 的规范表示形式，则将指针的值扩展 VT_UI8 为零，并将其保留为此64位格式的内部数据。 TypePointer 的任何类型符号都有一个基类型 (，由指针指向的类型的 GetBaseType 方法) 返回。
TypeMemberPointer | 指向类成员的指针。 具有类型为 TypeMemberPointer 的本机类型的模型对象具有规范表示形式，该表示形式 (值与指针值) 相同。 此值的确切含义是特定于编译器/调试主机的。
TypeArray | 一个数组。 具有类型为 TypeArray 的本机类型的模型对象具有 ObjectTargetObject 的规范表示形式。 数组的基址是 (通过 GetLocation 方法检索的对象的位置) 并且始终保留数组的类型。 TypeArray 的任何类型符号都具有由 GetBaseType) 方法返回的基类型 (，数组是该类型的数组。
TypeFunction | 一个函数。
TypeTypedef | Typedef。 如果模型对象的类型为 TypeTypedef 的本机类型为，则其类型应与 typedef 的最终类型的规范表示形式相同。 这对于对象的最终用户和类型信息是完全透明的，除非使用 IDebugHostType2 的显式 typedef 方法来查询 typedef 信息，或者有一个针对 typedef 注册的显式数据模型。 请注意，GetTypeKind 方法绝不会返回 TypeTypedef。 每个方法都将返回 typedef 要返回的最终类型。 IDebugHostType2 上有特定于 typedef 的方法，可用于获取特定于 typedef 的信息。
TypeEnum | 枚举。 如果模型对象的类型为 TypeEnum 的本机类型为类型为的类型，则它的规范表示形式为 ObjectIntrinsic，其中内部函数的值和类型与枚举值相同。 
TypeIntrinsic | ) 的内部 (基类型。 具有类型为 TypeIntrinsic 的本机类型的模型对象具有 ObjectIntrinsic 的规范表示形式。 类型信息可能会保留，也可能不会保留（特别是在 IModelObject 中存储的内部数据的变量数据 (类型 VT_ * ) 时，尤其是在基础类型完全由

总体 IDebugHostType2/IDebugHostType 接口定义如下 (排除 IDebugHostSymbol 方法) ： 

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

以下 IDebugHostType 方法对于任何类型都是通用的，无论从 GetTypeKind 方法返回哪种类型： 

```cpp
STDMETHOD(GetTypeKind)(_Out_ TypeKind *kind) PURE;
STDMETHOD(GetSize)(_Out_ ULONG64* size) PURE;
STDMETHOD(GetBaseType)(_Out_ IDebugHostType** baseType) PURE;
STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
```

[GetTypeKind](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-gettypekind)

GetTypeKind 方法返回类型 (指针、数组、内部等）。符号 ) 引用。 

[GetSize](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getsize)

GetSize 方法返回类型 (的大小，就像在 c + +) 中 (类型) 已完成。 

[GetBaseType](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getbasetype)

如果类型是另一个类型的导数 (例如： as Mystruct>) * 派生自 Mystruct>) ") ，则 GetBaseType 方法返回派生的基类型。 对于指针，这会返回指向的类型。 对于数组，这将返回数组是的数组。 如果类型不是派生类型，则返回错误。 

[GetHashCode](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-gethashcode)

GetHashCode 方法返回类型的32位哈希代码。 除全局匹配外 (（例如：类型签名等效于 *，如果主机) 允许，它匹配所有内容，则任何可匹配特定类型签名的类型实例都必须返回相同的哈希代码。 此方法与类型签名结合使用，以便将类型签名与类型实例相匹配。 


**IDebugHostType2/IDebugHostType 内部方法**

以下 IDebugHostType 方法特定于包含内部数据的内部类型 (或类型，如枚举) ： 

```cpp
STDMETHOD(GetIntrinsicType)(_Out_opt_ IntrinsicKind *intrinsicKind, _Out_opt_ VARTYPE *carrierType) PURE;
```

[GetIntrinsicType](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getintrinsictype)

GetIntrinsicType 方法返回类型为的内部类型的相关信息。 此方法返回了两个值： 

- 内部类型指示总体类型 (例如：整数、无符号、浮点) 但不 (类型的大小，例如：8位，16位，32位，64位) 
- 电信公司类型指示内部类型打包为变体结构的方式。 这是 VT_ * 常量。

这两个值的组合提供了有关内部函数的完整信息集。 


**IDebugHostType2/IDebugHostType 位域方法**

以下 IDebugHostType 方法特定于在位域中存储数据的类型。 内部函数中的域位置的相关信息存储在数据模型中的类型符号中，而不是位置的属性。 

```cpp
STDMETHOD(GetBitField)(_Out_ ULONG* lsbOfField, _Out_ ULONG* lengthOfField) PURE;
```

[GetBitField](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getbitfield)

如果数据结构的给定成员是域域 (例如： ULONG MyBits： 8) ，则字段的类型信息将与其域位置有关的信息。 GetBitField 方法可用于检索该信息。 此方法将对不是域域的任何类型失败。 这是该方法失败的唯一原因。 只需调用此方法并查看成功/失败就足以区分位域和非位字段。 如果某个给定类型确实为域域，则字段位置由半开放式集定义 * (lsbOfField + lengthOfField： lsbOfField]*


**IDebugHostType2/IDebugHostType 指针相关方法**

以下 IDebugHostType 方法特定于指针类型。 例如，GetTypeKind 返回 TypePointer 或 TypeMemberPointer 的类型： 

```cpp
STDMETHOD(GetPointerKind)(_Out_ PointerKind* pointerKind) PURE;
STDMETHOD(GetMemberType)(_Out_ IDebugHostType** memberType) PURE;
```
[GetPointerKind](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getpointerkind)

对于作为指针的类型，GetPointerKind 方法将返回指针的类型。 这由 PointerKind 枚举定义。

[GetMemberType](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getmembertype)

对于是指针到成员 (如类型 TypeMemberPointer) 所指示的类型，GetMemberType 方法返回类，该指针是指向成员的指针。 


**IDebugHostType2/IDebugHostType 数组相关方法**

数组是 GetTypeKind 返回 TypeArray 的类型。 请注意，由调试主机的类型系统定义的数组不同于基于零的多维线性数组（C 利用这一维数组）。 C 样式数组适合定义，但在 IDebugHostType 中，数组的总体范围更广。 调试主机中的数组可以是多维的，数组中的每个维度都由一个称为 ArrayDimensionThis 描述符的描述符来定义： 



字段 | 含义
|--------------|------------------|
LowerBound | 作为签名的64位值的数组的基本索引。 对于 C 样式数组，此值将始终为零。 不需要。 可以将数组的单个维度视为从任何64位索引（甚至是负值）开始。
Length | 作为无符号64位值的数组维度的长度。 数组的索引跨越半开放式集 [LowerBound，LowerBound + Length) 。
跨距 | 定义数组维度的跨距。 对于此维度的索引中的一个 (从 N 到 N + 1) 增加，这表示在内存中向前移动的字节数。 对于 C 样式数组，这是数组的每个元素的大小。 不需要。 元素之间的填充可表示为大于每个单个元素的大小的跨距。 对于多维数组，此值指示如何向前移动整个维度。 请考虑一个 M x N 矩阵。 这可能会在行主窗体中描述为两个维度： 

```cpp   
{ [LowerBound: 0, Length: M, Stride: N \* sizeof(element)], [LowerBound: 0, Length: N, Stride: sizeof(element)]} 
```
也可以将其作为两个维度的列主要形式来描述： 

```cpp   
{ [LowerBound: 0, Length: M, Stride: sizeof(element)], [LowerBound: 0, Length: N, Stride: M \* sizeof(element)]} 
```
ArrayDimension 概念允许这种灵活性。 

以下 IDebugHostType 方法特定于数组类型。 

```cpp
STDMETHOD(GetArrayDimensionality)(\_Out_ ULONG64\* arrayDimensionality) PURE; 
STDMETHOD(GetArrayDimensions)(\_In_ ULONG64 dimensions, \_Out_writes_(dimensions) ArrayDimension \*pDimensions) PURE;
```

[GetArrayDimensionality](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getarraydimensionality)

GetArrayDimensionality 方法返回在其中索引数组的维数。 对于 C 样式数组，此处返回的值将始终为1。 

[GetArrayDimensions](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getarraydimensions)

GetArrayDimensions 方法为数组的每个维度返回一组描述符，由 GetArrayDimensionality 方法指示。 每个描述符都是一个 ArrayDimension 结构，描述每个数组维度的起始索引、长度和正向跨距。 这允许说明比 C 类型系统中所允许的功能大得多的数组构造。 

对于 C 样式数组，在此处返回单个数组维度，其值始终为： 

- LowerBound = 0
- Length = 数组大小 (数组) 
- 步幅 = sizeof (elementType) 


**IDebugHostType2/IDebugHostType 函数相关方法**

如果类型指示它们是函数类型，则通过一种 TypeFunction 支持 IDebugHostType 和 IDebugHostType2 中的以下方法。 

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

[GetFunctionCallingConvention](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getfunctioncallingconvention)

GetFunctionCallingConvention 方法返回函数的调用约定。 此类作为 CallingConventionKind 枚举的成员返回。 

[GetFunctionReturnType](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionreturntype)

GetFunctionReturnType 方法返回函数的返回类型。 

[GetFunctionParameterTypeCount](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionparametertypecount)

GetFunctionParameterTypeCount 方法返回函数所采用的参数的数目。 请注意，在此计数中不考虑基于 C/c + + 省略号的变量参数标记。 此类的存在必须通过 GetFunctionVarArgsKind 方法来检测。 这只会在省略号之前包含参数。 

[GetFunctionParameterTypeAt](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype-getfunctionparametertypeat)

GetFunctionParameterTypeAt 方法返回函数的第 i 个参数的类型。 

GetFunctionVarArgsKind 方法返回给定函数是否使用变量自变量列表，如果是，则返回它所利用的变量参数样式。 这是由定义的 VarArgsKind 枚举的成员定义的，如下所示： 

 Enumerant | 含义
|---------|---------|
VarArgsNone | 函数不采用任何可变参数。
VarArgsCStyle | 函数是 (returnType (arg1、arg2、... ) # A3 的 C 样式 varargs 函数。函数报告的参数数目不包括省略号参数。 所有变量参数传递发生在 GetFunctionParameterTypeCount 方法返回的参数数目之后。


**IDebugHostType2 GetFunctionVarArgsKind**

GetFunctionVarArgsKind 方法返回给定函数是否使用变量自变量列表，如果是，则返回它所利用的变量参数样式。 这是由定义的 VarArgsKind 枚举的成员定义的，如下所示： 


**IDebugHostType2/IDebugHostType Typedef 相关方法**

任何类型的 typedef 都将表现为类型为 typedef 基础的最终类型。 这意味着 GetTypeKind 等方法不会指示该类型为 typedef。 同样，GetBaseType 也不会返回定义所引用的类型。 它们将改为指示行为，就好像它们是在 typedef 的最终定义上调用的一样。 示例： 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```

"PMYSTRUCT" 或 "PTRMYSTRUCT" 的 IDebugHostType 将报告以下信息： 

- GetTypeKind 方法将返回 TypePointer。 最终的基础类型 MYSTRUCT>) * 确实是一个指针。
- "GetBaseType 方法将返回 MYSTRUCT>) 的类型。 MYSTRUCT>) * 的基础类型为 MYSTRUCT>) 。

此处的唯一区别是 IDebugHostType2 上的 typedef 特定方法的行为方式。 这些方法包括： 

```cpp
STDMETHOD(IsTypedef)(_Out_ bool* isTypedef) PURE;
STDMETHOD(GetTypedefBaseType)(_Out_ IDebugHostType2** baseType) PURE;
STDMETHOD(GetTypedefFinalBaseType)(_Out_ IDebugHostType2** finalBaseType) PURE;
```

在此示例中： 

- 对于 PMYSTRUCT 和 PTRMYSTRUCT，IsTypedef 方法将返回 true
- GetTypedefBaseType 方法将返回 MYSTRUCT>) * for PMYSTRUCT 和 PMYSTRUCT for PTRMYSTRUCT
- 对于这两种类型，GetTypedefFinalBaseType 方法将返回 MYSTRUCT>) *

[IsTypedef](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype2-istypedef)

IsTypedef 方法是唯一能够查看类型是否为 typedef 的方法。 GetTypeKind 方法的行为类似于在基础类型上调用。 

[GetTypedefBaseType](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype2-gettypedefbasetype)

GetTypedefBaseType 方法将返回 typedef 立即定义的内容。 在文档中所述的示例中： 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```
此方法将为 PTRMYSTRUCT 返回 PMYSTRUCT 和 PMYSTRUCT 的 MYSTRUCT>) *。


[GetTypedefFinalBaseType](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttype2-gettypedeffinalbasetype)

GetTypedefFinalBaseType 方法将返回 typedef 是其定义的最终类型。 如果 typedef 是另一个 typedef 的定义，则这将继续遵循定义链，直到它达到不是 typedef 的类型并且将返回该类型。 在文档中所述的示例中： 

```cpp
typedef MYSTRUCT *PMYSTRUCT;
typedef PMYSTRUCT PTRMYSTRUCT;
```

当在 PMYSTRUCT 或 PTRMYSTRUCT 上调用时，此方法将返回 MYSTRUCT>) *。 

**IDebugHostType2/IDebugHostType 类型创建方法**

```cpp
STDMETHOD(CreatePointerTo)(_In_ PointerKind kind, _COM_Outptr_ IDebugHostType** newType) PURE;
STDMETHOD(CreateArrayOf)(_In_ ULONG64 dimensions, _In_reads_(dimensions) ArrayDimension *pDimensions, _COM_Outptr_ IDebugHostType** newType) PURE;
```

**常量符号值： IDebugHostConstant**

对于在符号信息 (中存在常数值的位置其中特定值是符号，该符号可以是也可以不是常数值) ，IDebugHostConstant 接口表示此类常量的概念。 这通常在类似模板参数的位置使用，其中给定自变量通常是类型，但可以是非类型模板参数 (例如：常量) 。 

IDebugHostConstant 接口定义如下 (忽略 IDebugHostSymbol 实现的泛型方法) ： 

```cpp
DECLARE_INTERFACE_(IDebugHostConstant, IDebugHostSymbol)
{
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

[GetValue](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostconstant-getvalue)

GetValue 方法返回打包为变量的常量的值。 请注意，IDebugHostSymbol 上的 GetType 方法可能返回常量的特定类型符号，这一点很重要。 在这种情况下，无法保证类型符号定义的常量值的封装与在此处 GetValue 方法返回的包装相同。 


**数据成员访问： IDebugHostField**

IDebugHostField 类表示一个符号，该符号是类、结构、联合或其他类型构造的数据成员。 它不表示可用数据 (例如：全局数据) 。 接口定义如下 (忽略 IDebugHostSymbol 的泛型方法) ： 

```cpp
DECLARE_INTERFACE_(IDebugHostField, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetOffset)(_Out_ ULONG64* offset) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

[GetLocationKind](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostfield-getlocationkind)

GetLocationKind 方法根据 LocationKind 枚举返回符号所处的位置类型。 此类枚举可以是下列值之一： 

Enumerant | 含义
|---------|--------|
LocationMember | 该字段是类、结构、联合或其他类型构造的常规数据成员。 它有一个相对于包含类型构造的基址的偏移量。 此类基址通常由 this 指针表示。 可以通过 GetOffset 方法检索字段的偏移量。 对于 LocationMember 的字段，GetLocation 和 GetValue 方法将失败。
LocationStatic | 此字段是静态的，并且具有其自己的地址。 GetLocation 方法将返回抽象位置 (例如：静态字段的地址) 。 对于 LocationStatic 的字段，GetOffset 和 GetValue 方法将失败。
LocationConstant | 此字段为常量，并且具有值。 GetValue 方法将返回常量的值。 对于 LocationConstant 的字段，GetOffset 和 GetLocation 方法将失败
LocationNone | 该字段没有位置。 它可能已被编译器优化，或者可能是声明但从未定义的静态字段。 无论这种字段如何，都不会出现物理状态或值。 它仅用于符号。 对于 LocationNone 的字段，所有 (GetOffset、GetLocation 和 GetValue) 的购置方法都将失败。

[GetOffset](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostfield-getoffset)

对于具有偏移量的字段 (例如：其位置种类指示 LocationMember) 的字段，GetOffset 方法将返回包含类型的基址的偏移量， (将 this 指针) 到字段自身的数据。 此类偏移量始终表示为未签名的64位值。 如果给定字段的位置不是与包含类型基址的偏移量，则 GetOffset 方法将失败。 

[GetLocation](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostfield-getlocation)

对于具有地址而不考虑特定类型实例的字段 (例如：其位置种类指示 LocationStatic) 的字段，GetLocation 方法将返回字段的抽象位置 (地址) 。 如果给定字段没有静态位置，则 GetLocation 方法将失败。 

[GetValue](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostfield-getvalue)

对于在符号信息中定义了常数值的字段 (例如：其位置种类指示 LocationConstant) 的字段，GetValue 方法将返回该字段的常数值。 如果给定字段没有常数值，则 GetValue 方法将失败。 


**免费数据访问： IDebugHostData**

不是其他类型的成员的模块中的数据由 IDebugHostData 接口表示。 此接口定义如下 (忽略 IDebugHostSymbol 的泛型方法) ： 

```cpp
DECLARE_INTERFACE_(IDebugHostData, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
    STDMETHOD(GetValue)(_Out_ VARIANT* value) PURE;
}
```

所有这些方法在语义上都等效于它们在 IDebugHostField 中的对应项。 唯一的区别在于，GetLocationKind 方法绝不会为 free 数据返回 LocationMember。 

[GetLocationKind](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostdata-getlocationkind)

GetLocationKind 方法根据 LocationKind 枚举返回符号所处的位置类型。 可在 IDebugHostField 的文档中找到此枚举的说明。 

[GetLocation](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostdata-getlocation)

对于包含地址的数据，GetLocation 方法将返回字段 (地址) 的抽象位置。 如果给定的数据没有静态位置，则 GetLocation 方法将失败。 

[GetValue](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostdata-getvalue)

对于 datawhich，在符号信息 (例如：其位置种类指示) LocationConstant 的数据）中定义了一个常数值，GetValue 方法将返回该字段的常数值。 如果给定的数据没有常数值，则 GetValue 方法将失败。 


**基类： IDebugHostBaseClass**

给定类型的继承层次结构通过类型符号的子级表示。 如果某个给定类型从一个或多个类型派生 (继承) ，则该类型的类型符号将有一个或多个 SymbolBaseClass 子级。 其中每个 SymbolBaseClass 符号表示从特定类型的立即继承。 基类的名称既是 SymbolBaseClass 符号的名称，也是基类的类型符号的名称。 SymbolBaseClass 符号上的 GetType 方法可用于获取基类本身的类型符号。 可以通过递归浏览 SymbolBaseClass 子符号遍历完全继承层次结构。 其中的每个基类符号都由 IDebugHostBaseClass 接口表示，此接口定义为以下内容 (忽略 IDebugHostSymbol 的泛型方法) ： 

```cpp
DECLARE_INTERFACE_(IDebugHostBaseClass, IDebugHostSymbol)
{
    STDMETHOD(GetOffset)(_Out_ ULONG64* offset) PURE;
}
```

[GetOffset](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostbaseclass-getoffset)

GetOffset 方法从派生类的基址返回基类的偏移量。 此类偏移量可以是零，也可以是正无符号64位值。 


**公共符号： IDebugHostPublic**

公共符号表示符号文件中公共表中的项。 它们实际上是导出地址。 没有与公共符号关联的类型信息-仅限一个地址。 除非调用方显式请求公共符号，否则调试宿主优先于返回每个查询的私有符号。 公共符号由定义如下的 IDebugHostPublic 接口表示， (忽略 IDebugHostSymbol 的泛型方法) ： 

```cpp
DECLARE_INTERFACE_(IDebugHostPublic, IDebugHostSymbol)
{
    STDMETHOD(GetLocationKind)(_Out_ LocationKind *locationKind) PURE;
    STDMETHOD(GetLocation)(_Out_ Location* location) PURE;
}
```

所有这些方法在语义上都等效于它们在 IDebugHostField 中的对应项。 唯一的区别是，GetLocationKind 方法绝不会为此类符号返回 LocationMember 或 LocationConstant。 

[GetLocationKind](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostpublic-getlocationkind)

GetLocationKind 方法根据 LocationKind 枚举返回符号所处的位置类型。 可在 IDebugHostField 的文档中找到此枚举的说明。 

[GetLocation](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostpublic-getlocation)

对于包含地址的数据，GetLocation 方法将返回字段 (地址) 的抽象位置。 如果给定的公共没有静态位置，则 GetLocation 方法将失败。 


**模块签名和版本匹配： IDebugHostModuleSignature**

模块签名表示一种检查给定模块是否符合一组有关命名和版本控制的条件的方法。 模块签名是通过 IDebugHostSymbols 上的 CreateModuleSignature 方法创建的。 它可以与模块名称和模块的可选版本号范围匹配。 创建此类签名后，客户端将收到如下所示的 IDebugHostModuleSignature 接口： 

```cpp
DECLARE_INTERFACE_(IDebugHostModuleSignature, IUnknown)
{
    STDMETHOD(IsMatch)(_In_ IDebugHostModule* pModule, _Out_ bool* isMatch) PURE;
}
```

[IsMatch](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughostmodulesignature-ismatch)

IsMatch 方法将 IDebugHostModule 符号) 指定的特定模块 (与签名进行比较，并将模块名称和版本与签名中指定的名称和版本范围进行比较。 返回给定模块符号是否与签名匹配。 

**类型签名和类型匹配： IDebugHostTypeSignature**

类型签名表示一种检查给定类型实例是否满足类型名称、类型的泛型参数和该类型所在的模块的一组条件的方法。 类型签名是通过 IDebugHostSymbols 上的 CreateTypeSignature 方法创建的。 创建此类签名后，客户端将收到如下所示的 IDebugHostTypeSignature 接口： 

```cpp
DECLARE_INTERFACE_(IDebugHostTypeSignature, IUnknown)
{
    STDMETHOD(GetHashCode)(_Out_ ULONG* hashCode) PURE;
    STDMETHOD(IsMatch)(_In_ IDebugHostType* type, _Out_ bool* isMatch, _COM_Outptr_opt_ IDebugHostSymbolEnumerator** wildcardMatches) PURE;
    STDMETHOD(CompareAgainst)(_In_ IDebugHostTypeSignature* typeSignature, _Out_ SignatureComparison* result) PURE;
}
```

[GetHashCode](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttypesignature-gethashcode)

GetHashCode 方法返回类型签名的32位哈希代码。 调试主机保证在为类型实例返回的哈希代码与为类型签名返回的哈希代码之间实现同步。 除全局匹配外，如果类型实例能够匹配类型签名，则这两个都将具有相同的32位哈希代码。 这允许在类型实例与使用数据模型管理器注册的类型为很多的类型之间进行初始快速比较和匹配。 

[IsMatch](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttypesignature-ismatch)

IsMatch 方法返回一个指示特定类型实例是否与类型签名中指定的条件匹配的指示。 如果是这样，则返回此的指示和一个枚举器，该枚举器将指示类型实例的所有特定部分 (为符号) 与类型签名中的通配符匹配。 

[CompareAgainst](/windows-hardware/drivers/ddi/dbgmodel/nf-dbgmodel-idebughosttypesignature-compareagainst)

CompareAgainst 方法将类型签名与其他类型签名进行比较，并返回两个签名的比较方式。 返回的比较结果是 SignatureComparison 枚举的成员，定义如下： 

Enumerant | 含义
|---------|-----------|
Unrelated | 两个签名或所比较的类型之间没有关系。
不明确 |一个签名或类型将不明确与另一个进行比较。 对于两种类型的签名，这意味着有可能的类型实例可以同样匹配其中一个签名。 例如，下面所示的两种类型签名是不明确的。  签名1： `std::pair<*, int>`  签名2： `std::pair<int,*>` 因为类型实例 `std::pair<int, int>` 与一个 (都匹配，所以两者都有一个具体的和一个通配符匹配) 。
LessSpecific | 一个或多个签名或类型不是另一个。 通常，这意味着不太具体的签名包含一个通配符，其中更具体的签名有一个具体类型。 例如，下面的第一个签名不只是第二个签名。 签名1： `std::pair<*, int>` 签名2： `std::pair<int, int>` 因为它具有一个通配符 (`*`) 其中第二个 (int) 的具体类型。
MoreSpecific | 一个签名或类型比另一个不同。 通常，这意味着更具体的签名有一个具体类型，其中不太具体的签名包含通配符。 例如，下面的第一个签名比第二个更为具体。 签名1：  `std::pair<int, int>` 签名2： `std::pair<*, int>` 因为它具有 (int) 的具体类型，其中第二种类型 () 的通配符 `*` 。
相当 | 这两个签名或类型完全相同。

---

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

本主题是一系列文章的一部分，其中描述了可从 c + + 访问的接口，如何使用它们来生成基于 c + + 的调试器扩展，以及如何利用其他数据模型构造 (例如： JavaScript 或 NatVis) 从 c + + 数据模型扩展。

[调试器数据模型 C++ 概述](data-model-cpp-overview.md)

[调试器数据模型 C++ 接口](data-model-cpp-interfaces.md)

[调试器数据模型 C++ 对象](data-model-cpp-objects.md)

[调试器数据模型 C++ 的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 C++ 的概念](data-model-cpp-concepts.md)

[调试器数据模型 C++ 脚本](data-model-cpp-scripting.md)