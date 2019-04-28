---
title: 线程模型
description: 线程模型
ms.assetid: 3BB0C01B-D82B-45dd-8AC8-EA2E2811CD24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 606f9b78d54a8cda3f6c02ae0eaef99967b25220
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348349"
---
# <a name="threading-models"></a>线程模型


TAEF 提供的功能用于预配置的 COM 线程模型为在其中测试的环境执行。 默认情况下，托管 ©\#) 和脚本在 STA 线程; 上运行的测试对于纯模式、 线程模型不是预配置。

"ThreadingModel"元数据属性用于请求线程模型。 此属性支持的值为：

| 属性值 | 描述                                                                               |
|----------------|-------------------------------------------------------------------------------------------|
| STA            | 单线程单元 (使用 COINIT 调用 CoInitializeEx\_APARTMENTTHREADED 标志)。 |
| MTA            | 多线程的单元 (使用 COINIT 调用 CoInitializeEx\_多线程的标志)。       |
| 无           | 未指定线程模型。                                                         |

 

## <a name="span-idconfiguringathreadingmodelspanspan-idconfiguringathreadingmodelspanspan-idconfiguringathreadingmodelspanconfiguring-a-threading-model"></a><span id="Configuring_a_threading_model"></span><span id="configuring_a_threading_model"></span><span id="CONFIGURING_A_THREADING_MODEL"></span>配置线程模型


例如：若要请求 MTA 线程模型从C++标记：

```cpp
class ThreadModelTests
{

    TEST_CLASS(ThreadModelTests);

    BEGIN_TEST_METHOD(MTAThreadingModelTest)
        TEST_METHOD_PROPERTY(L"ThreadingModel", L"STA")
    END_TEST_METHOD()
};
```

此外可以请求一个类或模块的线程处理模型属性。 例如，

```cpp
class ThreadModelTestsWithMTADefault
{

    BEGIN_TEST_CLASS(ThreadModelTestsWithMTADefault)
        TEST_CLASS_PROPERTY(L"ThreadingModel", L"Mta")
    END_TEST_CLASS()

    TEST_METHOD(DefaultWithMTASetByClass);
};
```

同样，您还可以请求托管测试的线程模型：

```cpp
[TestClass]

public class SimpleTests
{
    [TestMethod]
    [TestProperty("ThreadingModel", "MTA")]
    public void Test1()
    {
        Verify.IsTrue(true);
    }

    [TestMethod]
    [TestProperty("ThreadingModel", "STA")]
    public void Test2()
    {
        Verify.IsTrue(true);
    }

    [TestMethod]
    [TestProperty("ThreadingModel", "{STA; MTA}")]
    public void SetsOfMetadataTest()
    {
        Log.Comment("In CSharpThreadingModelExample.SetsOfMetadataTest");
        DisplayAppartmentState();
    }
}
```

请注意，在上面的最后一个测试：SetsOfMetadataTest，还有可能要使用的元数据集并运行相同的测试： 第一种使用 STA 线程模型，然后使用 MTA。

 

 





