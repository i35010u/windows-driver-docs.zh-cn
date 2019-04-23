---
title: 调试器数据模型C++接口概述
description: 本主题提供了调试器的数据模型的概述C++接口，以便扩展和自定义调试器的功能。
ms.date: 04/09/2019
ms.openlocfilehash: de9859083d6ede03b0f9cd6a82e0beeca961eda4
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903353"
---
# <a name="debugger-data-model-c-overview"></a>调试器数据模型 C++ 概述

本主题概述如何使用调试器数据模型的C++接口，以便扩展和自定义调试器的功能。

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

[调试器数据模型概述C++接口](#overview)

[调试器数据模型接口的摘要](#summary)

[使用 DbgModelClientEx 库](#dbgmodelclientex)


---

## <a name="span-idoverview-overview-of-the-debugger-data-model-c-interface"></a><span id="overview"> 调试器数据模型概述C++接口

调试器数据模型是一种可扩展的对象模型，它能够让新调试器扩展（包括 JavaScript、NatVis 和 C++ 中的扩展）使用来自调试器的信息并生成可从调试器及其他扩展访问的信息。 构造其写入到数据模型的 Api 是从 JavaScript 扩展调试器的较新 (dx) 表达式计算器中也可用或C++扩展。 

为了说明调试器数据模型的目标，请考虑此传统的调试器命令。

```console
0: kd> !process 0 0 
PROCESS ffffe0007e6a7780
    SessionId: 1  Cid: 0f68    Peb: 7ff7cfe7a000  ParentCid: 0f34
    DirBase: 1f7fb9000  ObjectTable: ffffc001cec82780  HandleCount:  34.
    Image: echoapp.exe
...
```
调试程序命令正在使用的二进制掩码，它提供了非标准方式仅输出的文本。 难以使用、 设置格式，或扩展的文本输出，布局是特定于此命令。

调试器数据模型相比这[dx （显示调试器对象模型表达式）](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)命令。

```console
dx @$cursession.Processes.Where(p => p.Threads.Count() > 5)
```
此命令使用标准的数据模型的可发现、 可扩展和可组合以统一的方式。

逻辑上间距内容和扩展对特定对象的名称允许调试器扩展功能的发现。  

> [!TIP]
> 因为数据模型C++对象接口可以是非常详细，以实现完整C++的数据模型，它使用完整的帮助程序库C++异常，模板编程模式建议。 有关详细信息，请参阅[使用 DbgModelClientEx 库](#dbgmodelclientex)本主题中更高版本。
>

数据模型是方法的新[WinDbg 预览](debugging-using-windbg-preview.md)调试器，显示的大多数情况。 可以查询、 扩展，或编写脚本，因为它们由数据模型驱动新的用户界面中的许多元素。 有关详细信息，请参阅[WinDbg 预览版-数据模型](windbg-data-model-preview.md)。

![数据模型浏览窗口显示进程和线程](images/windbgx-data-model-process-threads.png)


### <a name="data-model-architectural-view"></a>数据模型体系结构视图

下图总结了调试器的数据模型体系结构的主要元素。

- 到左侧和右侧，显示 UI 元素，提供对象的访问权限和支持 LINQ 查询与此类功能。  
- 在关系图的右侧是向调试器数据模型提供数据的组件。 这包括自定义 NatVis，JavaScript 和C++调试器的数据模型扩展。 

![数据模型体系结构视图](images/data-model-simple-architectural-view.png)


### <a name="object-model"></a>对象模型

调试器数据模型的中心是所有内容都是 IModelObject 接口的实例在其中一个统一的对象表示形式。  虽然此类对象可能表示内部函数 (例如： 一个整数值) 或另一个数据模型接口，它通常表示动态对象 – 元数据键/值元组的字典和一组描述抽象行为的概念。   

下图显示了 IModelObject 如何使用密钥存储包含一个提供程序可以创建、 注册和操作的值。

- 它显示*提供程序*，提供对对象模型的信息
- 它显示在左侧*IModelObject*，即通用对象模型，用于操作对象。
- 在中心非常*密钥存储*用于存储和访问值。
- 它显示在底部*概念*对象支持的功能，例如将转换为可显示字符串或要编制索引的功能。

![数据模型体系结构视图](images/data-model-object-model.png)


### <a name="the-data-model-a-consumer-view"></a>数据模型中：使用者视图

下图显示了数据模型的使用者视图。 在示例[dx （显示调试器对象模型表达式）](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)命令用于查询的信息。 

- Dx 命令通过对对象的枚举接口的序列化程序进行通信。 
- IDebugHost * 对象用于从调试器引擎中收集信息。 
- 使用表达式和语义的评估者将请求发送到调试器引擎。

![数据模型体系结构视图](images/data-model-consumer-view.png)


### <a name="the-data-model-a-producer-view"></a>数据模型中：生成者视图

此图显示了数据模型的生成者视图。

- NatVis 提供程序显示在左侧使用 XML 定义其他功能。
- JavaScript 提供程序可以充分利用*提供程序的动态概念*处理实时的信息。
- 底部显示的本机代码提供程序还可以定义其他功能。

![数据模型体系结构视图](images/data-model-producer-view.png)


### <a name="data-model-manager"></a>数据模型管理器 

下图显示了中心角色对象的管理中起着数据模型管理器。

- 数据模型管理器充当中心的注册机构的所有对象。 
- 在左侧它显示如何标准调试器元素，如注册会话和进程。
- 命名空间块显示了中央注册列表。
- 关系图的右侧会显示两个提供程序，一个用于在最前面，NatVis，C /C++在底部的扩展。

![数据模型体系结构视图](images/data-model-manager.png)


## <a name="span-idsummary-summary-of-debugger-data-model-interfaces"></a><span id="summary"> 调试器数据模型接口的摘要

有多种C++接口组成的数据模型的不同部分。 若要以一致、 简便的方式处理这些接口，它们会细分按常规类别。 此处主要方面： 

**常规对象模型**

第一个也是最重要的一组接口定义如何获取对核心数据模型的访问以及如何访问和操作的对象。 IModelObject 是表示数据模型中的每个对象的接口 (像C#的对象)。 这是感兴趣的使用者和生成者到数据模型的主要接口。 其他接口是用于访问对象的不同方面的机制。 为此类别定义以下接口： 


*DbgEng 和数据模型之间的桥梁*

[IHostDataModelAccess](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ihostdatamodelaccess) 

*主要接口* 

[IModelObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelobject) 

[IKeyStore](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ikeystore) 

[IModelIterator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodeliterator) 

[IModelPropertyAccessor](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelpropertyaccessor) 

[IModelMethod](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelmethod) 

[IKeyEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ikeyenumerator) 

[IRawEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-irawenumerator) 

[IModelKeyReference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelkeyreference)  / [IModelKeyReference2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-imodelkeyreference2) 

*概念接口*

[IStringDisplayableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-istringdisplayableconcept) 

[IIterableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-iiterableconcept) 

[IIndexableConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-iindexableconcept) 

[IPreferredRuntimeTypeConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-ipreferredruntimetypeconcept) 

[IDataModelConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelconcept) 

[IDynamicKeyProviderConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idynamickeyproviderconcept) 

[IDynamicConceptProviderConcept](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idynamicconceptproviderconcept) 


**管理数据模型和可扩展性**

数据模型管理器是用于管理的核心组件如何发生的所有可扩展性。 它是一组表映射到扩展点，以及对扩展点的综合构造这两种本机类型的中央存储库。 此外，它是负责对象 （的序号值或字符串到 IModelObject 的转换） 的装箱的实体。 

为此类别定义以下接口： 

*常规数据模型管理器访问* 

[IDataModelManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelmanager)  / [IDataModelManager2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelmanager2) 

*脚本管理* 

[IDataModelScriptManager](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptmanager) 

[IDataModelScriptProviderEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptproviderenumerator) 


**对调试器的类型系统和内存空间的访问**

调试器的基础类型系统和内存空间中的扩展插件能够做出详细信息公开的使用。 为此类别定义以下接口： 

*常规主机 （调试器） 接口*

[IDebugHost](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughost) 

[IDebugHostStatus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughoststatus) 

[IDebugHostContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostcontext) 

[IDebugHostMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmemory)  / [IDebugHostMemory2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmemory2) 

[IDebugHostErrorSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosterrorsink) 

[IDebugHostEvaluator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostevaluator)  / [IDebugHostEvaluator2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostevaluator2) 

[IDebugHostExtensibility](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostextensibility) 

*主机 （调试器） 类型系统接口* 

[IDebugHostSymbols](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostsymbols) 

[IDebugHostSymbol](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostsymbol)  / [IDebugHostSymbol2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostsymbol2) 

[IDebugHostModule](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmodule) 

[IDebugHostType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosttype)  / [IDebugHostType2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosttype2) 

[IDebugHostConstant](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostconstant) 

[IDebugHostField](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostfield) 

[IDebugHostData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostdata) 

[IDebugHostBaseClass](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostbaseclass) 
[IDebugHostPublic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostpublic) 

[IDebugHostModuleSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostmodulesignature) 

[IDebugHostTypeSignature](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughosttypesignature) 

*对脚本的主机 （调试器） 支持* 

[IDebugHostScriptHost](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idebughostscripthost) 


**创作和使用脚本**

数据模型还具有哪些脚本，以及如何调试一个一般概念。 它是完全有可能的调试器扩展出现并定义数据模型和另一种动态语言 （通常是一个脚本编写环境） 之间的常规桥梁。 此组接口是如何完成此操作以及如何调试程序 UI 可使用此类脚本。 

为此类别定义以下接口： 

*常规脚本接口* 

[IDataModelScriptProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscript) 

[IDataModelScript](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscript) 

[IDataModelScriptClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptclient) 

[IDataModelScriptHostContext](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripthostcontext) 

[IDataModelScriptTemplate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripttemplate) 

[IDataModelScriptTemplateEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscripttemplateenumerator) 

[IDataModelNameBinder](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelnamebinder) 


*脚本调试器接口* 

[IDataModelScriptDebug](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebug) 

[IDataModelScriptDebugClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugclient) 

[IDataModelScriptDebugStack](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugstack) 

[IDataModelScriptDebugStackFrame](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugstackframe) 

[IDataModelScriptDebugVariableSetEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugvariablesetenumerator) 

[IDataModelScriptDebugBreakpoint](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugbreakpoint) 

[IDataModelScriptDebugBreakpointEnumerator](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/nn-dbgmodel-idatamodelscriptdebugbreakpointenumerator) 


## <a name="span-iddbgmodelclientex-using-the-dbgmodelclientex-library"></a><span id="dbgmodelclientex"> 使用 DbgModelClientEx 库

**概述**

数据模型C++对象的接口连接到数据模型可以变得非常冗长，来实现。 虽然它们允许数据模型的完整操作，它们需要实现的多个较小接口来扩展数据模型 (例如： 为每个动态 fetchable 属性添加 IModelPropertyAccessor 实现)。 除此之外，HRESULT 基于编程模型将添加大量的模板代码，用于错误检查。

为了尽量减少此工作的一部分，是一个完整的C++的数据模型，它使用完整的帮助程序库C++的异常和模板编程模式。 当使用或扩展数据模型时，可更简洁的代码，建议使用此库的使用。

帮助程序库中有两个重要的命名空间：

Debugger::DataModel::ClientEx-消耗的数据模型的帮助程序

Debugger::DataModel::ProviderEx-数据模型的扩展的帮助程序

有关使用 DbgModelClientEx 库的其他信息，请参阅此 github 站点上的自述文件：

https://github.com/Microsoft/WinDbg-Libraries/tree/master/DbgModelCppLib


**HelloWorldC++示例**

若要了解可以如何使用 DbgModelClientEx 库，查看数据模型 HelloWorldC++此处的示例。

https://github.com/Microsoft/WinDbg-Samples/tree/master/DataModelHelloWorld

示例包括：

- HelloProvider.cpp-这是进程的添加新的示例属性"Hello"到调试器的这一概念的提供程序类的实现。

- SimpleIntroExtension.cpp-这是进程的一个简单的调试器扩展，也就是进程的添加一个新的示例属性"Hello"到调试器的这一概念。 此扩展是针对的数据模型 C + + 17 帮助程序库编写的。  目前，最好编写针对此库而不是原始 COM ABI 由于粘附代码所需的卷 （和复杂性） 扩展。


**JavaScript 和 COM 示例**

为了更好地了解写入调试器扩展与数据模型的不同方法，有三个版本的数据模型 HelloWorld 扩展可用此处：

https://github.com/Microsoft/WinDbg-Samples/tree/master/DataModelHelloWorld

- JavaScript-以 JavaScript 编写的版本

- C + + 17-编写针对数据模型中 C + + 17 的客户端库的版本

- COM-编写对原始 COM ABI （仅使用 WRL 适用于 COM 帮助程序） 的版本

---

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[调试器数据模型C++概述](data-model-cpp-overview.md)

[调试器数据模型C++接口](data-model-cpp-interfaces.md)

[调试器数据模型C++对象](data-model-cpp-objects.md)

[调试器数据模型C++的其他接口](data-model-cpp-additional-interfaces.md)

[调试器数据模型C++概念](data-model-cpp-concepts.md)

[调试器数据模型C++脚本](data-model-cpp-scripting.md)
