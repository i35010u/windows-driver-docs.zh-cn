---
title: DeploymentItem 元数据
description: DeploymentItem 元数据
ms.assetid: 7F18CD71-F000-4231-9093-82980EB7584D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e80be6a1d97a4670de74360db4fa351a21b4e611
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373030"
---
# <a name="deploymentitem-metadata"></a>DeploymentItem 元数据


**DeploymentItem**元数据标识为的文件和文件夹使用的测试在测试所在的执行过程，以便 Taef 者将能够识别这些内容，并将其适当地复制文件和文件夹的依赖项 (例如，在[跨计算机执行方案](cross-machine-execution.md)，由标识的文件将部署 Taef **DeploymentItem**属性设置为指定的测试计算机)。

Taef DeploymentItem 实现是非常类似于[类似的功能的 VSTS](https://docs.microsoft.com/en-US/dotnet/api/microsoft.visualstudio.testtools.unittesting.deploymentitemattribute?redirectedfrom=MSDN&view=mstest-net-1.2.0)。

DeploymentItem 元数据可应用于程序集、 类或测试级别。 响应方返回 （程序集、 测试类或测试） 安装程序运行时，将部署 DeploymentItem 元数据指定的项。 如果 DeploymentItem 元数据指定的依赖项 （例如，文件） 和目标中已存在该依赖关系，TAEF 执行 CRC 比较，并仅将文件复制已更改。 如果 DeploymentItem 元数据指定无法找到依赖关系和依赖项，则记录错误，则测试将失败 （或所有相应地测试类或程序集测试）。 每个程序集、 类或测试-即，部署不会发生这种情况在每个程序集，类，或如果这些是数据驱动测试扩展后，TAEF 仅会部署文件。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


<span id="General_Usage_"></span><span id="general_usage_"></span><span id="GENERAL_USAGE_"></span>常规使用情况   

<span id="_DeploymentItem__FileOrFolderToDeploy____DestinationFolder___"></span><span id="_deploymentitem__fileorfoldertodeploy____destinationfolder___"></span><span id="_DEPLOYMENTITEM__FILEORFOLDERTODEPLOY____DESTINATIONFOLDER___"></span>\[DeploymentItem("FileOrFolderToDeploy", "DestinationFolder")\]  
（其中

<span id="FileOrFolderToDeploy"></span><span id="fileorfoldertodeploy"></span><span id="FILEORFOLDERTODEPLOY"></span>FileOrFolderToDeploy  
是一个文件或文件夹路径相对于测试 dll 的目录。 如果**FileOrFolderToDeploy**是一个文件夹中，复制其内容; 但是，不会不创建文件夹本身。 如果下文件夹中的层次结构**FileOrFolderToDeploy**，Taef 将所有这些目录以递归方式复制，维护其目录层次结构。

<span id="DestinationFolder"></span><span id="destinationfolder"></span><span id="DESTINATIONFOLDER"></span>DestinationFolder  
测试 dll 是位置和部署项将复制的位置是相对于目录的文件夹路径。 **DestinationFolder**无法使用指定路径... 表示法 （例如，..\\MyFiles)。

如果只是想要部署到测试 dll 所在的文件夹**DestinationFolder**可以省略此参数：

```cpp
[DeploymentItem("FileOrFolderToDeploy")]
```

支持多个部分的属性。 例如：

```cpp
[TestClass]
[DeploymentItem("file1.xml")]
[DeploymentItem("file2.xml")]
[DeploymentItem("file3.xml")]
public class UnitTest1
{
    ...
}
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


<span id="_deploymentitem__file1.xml___"></span><span id="_DEPLOYMENTITEM__FILE1.XML___"></span>\[DeploymentItem("file1.xml")\]  
标记 file1.xml 旁边作为依赖项的测试 dll。 此元数据可以解释为系统部署到测试 dll 目录测试 dll 旁边文件夹中名为的 file1.xml。 此配置是仅适用于跨计算机方案。

<span id="_deploymentitem__file2.xml____datafiles___"></span><span id="_DEPLOYMENTITEM__FILE2.XML____DATAFILES___"></span>\[DeploymentItem("file2.xml", "DataFiles")\]  
将部署到测试 dll 目录中创建的数据文件子目录的测试 dll 旁边位于名为的 file2.xml。

<span id="_DeploymentItem__C___MyDataFiles__MyDataFiles2_____"></span><span id="_deploymentitem__c___mydatafiles__mydatafiles2_____"></span><span id="_DEPLOYMENTITEM__C___MYDATAFILES__MYDATAFILES2_____"></span>\[DeploymentItem("C:\\\\MyDataFiles\\\\MyDataFiles2\\\\")\]  
部署的所有项和目录 c： 驱动器中找到\\\\MyDataFiles\\\\MyDataFiles2\\ \\目录。 此配置不会创建 MyDataFiles\\MyDataFiles2 目录下的部署目录。 将部署的所有文件和目录 MyDataFiles 测试 dll 目录。 若要复制整个 MyDataFiles\\MyDataFiles2 目录结构，必须指定 MyDataFiles\\MyDataFiles2 作为输出目录。

<span id="_deploymentitem___mydir__myfile.txt___"></span><span id="_DEPLOYMENTITEM___MYDIR__MYFILE.TXT___"></span>\[DeploymentItem("%myDir%\\myFile.txt")\]  
如果该文件存在于 %mydir%解析到的目录，将部署文件 myFile.txt。 如果 TAEF 无法解析环境变量，则会引发错误。

## <a name="span-idmanagedtestsspanspan-idmanagedtestsspanspan-idmanagedtestsspanmanaged-tests"></a><span id="Managed_Tests"></span><span id="managed_tests"></span><span id="MANAGED_TESTS"></span>托管的测试


**DeploymentItem** (也称为 DeploymentItemAttribute) 特性可以应用于测试方法 (由修饰\[TestMethod\]属性)，测试类 (由修饰\[TestClass\]属性) 或测试程序集。 但是，由于在程序集级别上，VSTS 不支持此属性，将此属性应用于程序集级别，必须将其应用于程序集安装程序 （由 AssemblyInitialize 特性修饰）：

```cpp
[AssemblyInitialize]
[DeploymentItem("file1.xml")]
[DeploymentItem("file2.xml")]
[DeploymentItem("file3.xml")]
public  static AssemblySetup(TestContext testContext)
{
    ...
}
```

## <a name="span-idnativetestsspanspan-idnativetestsspanspan-idnativetestsspannative-tests"></a><span id="Native_Tests"></span><span id="native_tests"></span><span id="NATIVE_TESTS"></span>本机测试


对于本机测试，属性格式是类似于托管的代码格式。 但是，本机属性只有单个值，因为该项的路径和可选目标中指定的属性值，用分隔 **'&gt;** 字符：

```cpp
BEGIN_TEST_CLASS(TestClassExample)
    TEST_CLASS_PROPERTY(L"DeploymentItem", L"C:\\Dependencies\\>Dependencies")
END_TEST_CLASS()
```

## <a name="span-idscripttestsspanspan-idscripttestsspanspan-idscripttestsspanscript-tests"></a><span id="Script_Tests"></span><span id="script_tests"></span><span id="SCRIPT_TESTS"></span>脚本的测试


脚本测试的属性格式与本机测试相同：

```cpp
<method name="TestOne">
    <TestMethodProperty name="DeploymentItem" value="C:\\Dependencies\\>Dependencies"/>
</method>
```









