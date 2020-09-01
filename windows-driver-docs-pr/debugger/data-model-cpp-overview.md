---
title: 调试器数据模型 c + + 接口概述
description: 本主题概述了用于扩展和自定义调试器功能的调试器数据模型 c + + 接口。
ms.date: 09/12/2019
ms.openlocfilehash: 264e57845d1c18bece9e34bc658738cb7f23ef53
ms.sourcegitcommit: cd84cc10570384b0e7a91cb6f91fe67009c1a90e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89238143"
---
# <a name="debugger-data-model-c-overview"></a>调试器数据模型 C++ 概述

本主题概述了如何使用调试器数据模型 c + + 接口来扩展和自定义调试器的功能。

本主题是一系列文章的一部分，其中描述了可从 c + + 访问的接口，如何使用它们来生成基于 c + + 的调试器扩展，以及如何利用其他数据模型构造 (例如： JavaScript 或 NatVis) 从 c + + 数据模型扩展。

[调试器数据模型 C++ 概述](data-model-cpp-overview.md)

[调试器数据模型 C++ 接口](data-model-cpp-interfaces.md)

[调试器数据模型 C++ 对象](data-model-cpp-objects.md)

[调试器数据模型 C++ 的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 C++ 的概念](data-model-cpp-concepts.md)

[调试器数据模型 C++ 脚本](data-model-cpp-scripting.md)

---

## <a name="span-idoverview-overview-of-the-debugger-data-model-c-interface"></a><span id="overview"> 调试器数据模型 c + + 接口概述

调试器数据模型是一种可扩展的对象模型，它能够让新调试器扩展（包括 JavaScript、NatVis 和 C++ 中的扩展）使用来自调试器的信息并生成可从调试器及其他扩展访问的信息。 在调试器的较新 (dx) 表达式计算器以及 JavaScript 扩展或 c + + 扩展中提供了写入数据模型 Api 的构造。 

若要阐释调试器数据模型的目标，请考虑此传统的调试器命令。

```console
0: kd> !process 0 0 
PROCESS ffffe0007e6a7780
    SessionId: 1  Cid: 0f68    Peb: 7ff7cfe7a000  ParentCid: 0f34
    DirBase: 1f7fb9000  ObjectTable: ffffc001cec82780  HandleCount:  34.
    Image: echoapp.exe
...
```
调试器命令使用二进制掩码，并且仅以非标准方式提供文本输出。 文本输出难以使用、格式化或扩展，并且布局特定于此命令。

与调试器数据模型 [dx (显示调试器对象模型表达式) ](dx--display-visualizer-variables-.md) 命令。

```console
dx @$cursession.Processes.Where(p => p.Threads.Count() > 5)
```
此命令使用可在统一方式中发现、可扩展和可组合的标准数据模型。

逻辑上命名对特定对象的间距和扩展允许发现调试器扩展功能。  

> [!TIP]
> 由于数据模型 c + + 对象接口可以非常详细地实现使用完整 c + + 异常的数据模型的完整 c + + 帮助库，建议使用模板编程范例。 有关详细信息，请参阅本主题后面 [的使用 DbgModelClientEx 库](#dbgmodelclientex) 。
>

数据模型是新的 [WinDbg 预览](debugging-using-windbg-preview.md) 调试器显示大多数项目的方式。 可以查询、扩展或编写新 UI 中的许多元素，因为这些元素由数据模型提供支持。 有关详细信息，请参阅 [WinDbg 预览-数据模型](windbg-data-model-preview.md)。

![数据模型浏览显示进程和线程的窗口](images/windbgx-data-model-process-threads.png)


### <a name="data-model-architectural-view"></a>数据模型体系结构视图

下图汇总了调试器数据模型结构的主要元素。

- 向左显示 UI 元素，这些元素提供对对象的访问，并支持 LINQ 查询等功能。  
- 关系图的右侧是向调试器数据模型提供数据的组件。 这包括自定义 NatVis、JavaScript 和 c + + 调试器数据模型扩展。 

![数据模型体系结构视图在中心显示公用对象模型，右侧提供提供程序](images/data-model-simple-architectural-view.png)


### <a name="object-model"></a>对象模型

调试器数据模型的中心是统一的对象表示形式，其中一切都是 IModelObject 接口的实例。  尽管此类对象可以表示内部 (例如：整数值) 或另一个数据模型接口，但它通常表示一个动态对象-一个键/值/元组元组的字典，以及一组描述抽象行为的概念。   

此图显示了 IModelObject 如何使用密钥存储来包含提供程序可以创建、注册和操作的值。

- 它显示提供对象模型信息的*提供程序*
- 左侧显示了 *IModelObject*，它是用于操作对象的通用对象模型。
- 中心是用于存储和访问值的 *密钥存储* 。
- 下面的示例演示了支持对象的 *概念* ，这些对象的功能可以转换为可显示的字符串或进行索引。

![显示 IModelObject 作为输入和元组密钥存储的数据模型体系结构视图](images/data-model-object-model.png)


### <a name="the-data-model-a-consumer-view"></a>数据模型：使用者视图

下图显示了数据模型的使用者视图。 在示例中， [dx (显示调试器对象模型表达式) ](./dx--display-visualizer-variables-.md) 命令正用于查询信息。 

- Dx 命令通过序列化程序与对象枚举接口进行通信。 
- IDebugHost * 对象用于从调试器引擎中收集信息。 
- 表达式和语义计算器用于向调试器引擎发送请求。

![数据模型体系结构视图显示将 UI 馈送到 IDebugHost 的计算器](images/data-model-consumer-view.png)


### <a name="the-data-model-a-producer-view"></a>数据模型：制造者视图

此图显示了数据模型的生成者视图。

- NatVis 提供程序在左侧显示，其中使用定义了附加功能的 XML。
- JavaScript 提供程序可以利用 *动态提供程序概念* 来实时操作信息。
- 下图显示了可定义其他功能的本机代码提供程序。

![数据模型体系结构视图，其中显示了 Natvis、Javascript 和本机代码使用者的 IModelObject](images/data-model-producer-view.png)

### <a name="data-model-manager"></a>数据模型管理器

此图显示了数据模型管理器在对象管理中所扮演的中心角色。

- 数据模型管理器充当所有对象的中央注册器。 
- 左侧显示了如何注册标准调试器元素，如会话和进程。
- 命名空间块显示中央注册列表。
- 关系图的右侧显示了两个提供程序，一个用于顶部有一个 NatVis，另一个是 C/c + + 扩展。

![显示数据模型管理器正在查找的注册名称的数据模型体系结构视图](images/data-model-manager.png)

## <a name="span-idsummary-summary-of-debugger-data-model-interfaces"></a><span id="summary"> 调试器数据模型接口摘要

许多 c + + 接口都包含不同的数据模型部分。 若要以一致且简单的方式来实现这些接口的方法，它们按常规类别细分。 主要区域如下： 

**常规对象模型**

第一组和最重要的接口定义如何访问核心数据模型，以及如何访问和操作对象。 IModelObject 是一个接口，它表示数据模型中的每个对象， (非常类似于 c # 的对象) 。 这是对数据模型的两个使用者和制造者都感兴趣的主要接口。 其他接口是用于访问对象的不同方面的机制。 为此类别定义以下接口： 


*DbgEng 和数据模型之间的桥梁*

[IHostDataModelAccess](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-ihostdatamodelaccess) 

*主接口* 

[IModelObject](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-imodelobject) 

[IKeyStore](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-ikeystore) 

[IModelIterator](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-imodeliterator) 

[IModelPropertyAccessor](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-imodelpropertyaccessor) 

[IModelMethod](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-imodelmethod) 

[IKeyEnumerator](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-ikeyenumerator) 

[IRawEnumerator](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-irawenumerator) 

[IModelKeyReference](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-imodelkeyreference)   / [IModelKeyReference2](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-imodelkeyreference2) 

*概念接口*

[IStringDisplayableConcept](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-istringdisplayableconcept) 

[IIterableConcept](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-iiterableconcept) 

[IIndexableConcept](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-iindexableconcept) 

[IPreferredRuntimeTypeConcept](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-ipreferredruntimetypeconcept) 

[IDataModelConcept](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelconcept) 

[IDynamicKeyProviderConcept](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idynamickeyproviderconcept) 

[IDynamicConceptProviderConcept](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idynamicconceptproviderconcept) 


**数据模型和扩展性的管理**

数据模型管理器是用于管理所有扩展性的发生方式的核心组件。 它是一组表的中心存储库，它们将本机类型映射到扩展点，并将合成构造映射到扩展点。 此外，它是一个实体，负责 (将序号值或字符串转换为 IModelObject 的) 的对象的装箱。 

为此类别定义以下接口： 

*常规数据模型管理器访问* 

[IDataModelManager](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelmanager)   / [IDataModelManager2](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelmanager2) 

*脚本管理* 

[IDataModelScriptManager](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptmanager) 

[IDataModelScriptProviderEnumerator](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptproviderenumerator) 


**访问调试器的类型系统和内存空间**

详细地公开了调试器的基础类型系统和内存空间，以使扩展能够使用。 为此类别定义以下接口： 

*常规宿主 (调试器) 接口*

[IDebugHost](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughost) 

[IDebugHostStatus](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughoststatus) 

[IDebugHostContext](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostcontext) 

[IDebugHostMemory](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostmemory)   / [IDebugHostMemory2](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostmemory2) 

[IDebugHostErrorSink](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughosterrorsink) 

[IDebugHostEvaluator](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostevaluator)   / [IDebugHostEvaluator2](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostevaluator2) 

[IDebugHostExtensibility](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostextensibility) 

*宿主 (调试器) 类型系统接口* 

[IDebugHostSymbols](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostsymbols) 

[IDebugHostSymbol](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostsymbol)   / [IDebugHostSymbol2](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostsymbol2) 

[IDebugHostModule](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostmodule) 

[IDebugHostType](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughosttype)   / [IDebugHostType2](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughosttype2) 

[IDebugHostConstant](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostconstant) 

[IDebugHostField](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostfield) 

[IDebugHostData](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostdata) 

[IDebugHostBaseClass](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostbaseclass)  
[IDebugHostPublic](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostpublic) 

[IDebugHostModuleSignature](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostmodulesignature) 

[IDebugHostTypeSignature](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughosttypesignature) 

*宿主 (调试器) 对脚本的支持* 

[IDebugHostScriptHost](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idebughostscripthost) 


**创作和使用脚本**

数据模型还大致说明了脚本的概念以及如何调试。 调试器扩展完全有可能在数据模型和另一种动态语言之间定义一般的桥梁， (通常是脚本环境) 。 这组接口是如何实现的，以及调试器 UI 如何利用此类脚本。 

为此类别定义以下接口： 

*常规脚本接口* 

[IDataModelScriptProvider](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscript) 

[IDataModelScript](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscript) 

[IDataModelScriptClient](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptclient) 

[IDataModelScriptHostContext](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscripthostcontext) 

[IDataModelScriptTemplate](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscripttemplate) 

[IDataModelScriptTemplateEnumerator](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscripttemplateenumerator) 

[IDataModelNameBinder](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelnamebinder) 


*脚本调试器接口* 

[IDataModelScriptDebug](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptdebug) 

[IDataModelScriptDebugClient](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptdebugclient) 

[IDataModelScriptDebugStack](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptdebugstack) 

[IDataModelScriptDebugStackFrame](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptdebugstackframe) 

[IDataModelScriptDebugVariableSetEnumerator](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptdebugvariablesetenumerator) 

[IDataModelScriptDebugBreakpoint](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptdebugbreakpoint) 

[IDataModelScriptDebugBreakpointEnumerator](/windows-hardware/drivers/ddi/dbgmodel/nn-dbgmodel-idatamodelscriptdebugbreakpointenumerator) 


## <a name="span-iddbgmodelclientex-using-the-dbgmodelclientex-library"></a><span id="dbgmodelclientex"> 使用 DbgModelClientEx 库

**概述**

数据模型 c + + 对象接口到数据模型的接口可能非常详细，无法实现。 尽管它们允许对数据模型进行完全操作，但它们要求实现大量的小接口以扩展数据模型 (例如：) 添加的每个动态 fetchable 属性的 IModelPropertyAccessor 实现。 除此之外，基于 HRESULT 的编程模型还添加了大量用于错误检查的样板印版代码。

为了最大限度地减少其中的某些工作，使用完整的 c + + 异常和模板编程模式的数据模型有一个完整的 c + + 帮助程序库。 使用此库可以在使用或扩展数据模型时获得更简洁的代码。

帮助程序库中有两个重要的命名空间：

调试程序：:D ataModel：： ClientEx-数据模型使用的帮助程序

调试器：:D ataModel：:P roviderEx-用于扩展数据模型的帮助程序

有关使用 DbgModelClientEx 库的其他信息，请参阅 github 站点上的自述文件：

https://github.com/Microsoft/WinDbg-Libraries/tree/master/DbgModelCppLib


**HelloWorld c + + 示例**

若要查看如何使用 DbgModelClientEx 库，请查看此处的数据模型 HelloWorld c + + 示例。

https://github.com/Microsoft/WinDbg-Samples/tree/master/DataModelHelloWorld

该示例包括：

- HelloProvider-这是提供程序类的一个实现，该实现类向调试器的进程概念中添加了一个新的示例属性 "Hello"。

- SimpleIntroExtension-这是一个简单的调试器扩展，它将新的示例属性 "Hello" 添加到调试器的进程概念。 此扩展是针对数据模型 c + + 17 Helper 库编写的。  对于此库（而不是原始的 COM)  (ABI）编写扩展，这是一种很好的方法。


**JavaScript 和 COM 示例**

为了更好地了解使用数据模型编写调试器扩展的不同方法，这里提供了三种版本的数据模型 HelloWorld 扩展：

https://github.com/Microsoft/WinDbg-Samples/tree/master/DataModelHelloWorld

- JavaScript-用 JavaScript 编写的版本

- C + + 17-针对数据模型 c + + 17 客户端库编写的版本

- COM-根据原始 COM ABI 编写的版本 (仅使用 WRL for COM 帮助程序) 

---

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[调试器数据模型 C++ 接口](data-model-cpp-interfaces.md)

[调试器数据模型 C++ 对象](data-model-cpp-objects.md)

[调试器数据模型 C++ 的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型 C++ 的概念](data-model-cpp-concepts.md)

[调试器数据模型 C++ 脚本](data-model-cpp-scripting.md)