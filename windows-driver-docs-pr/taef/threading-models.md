---
title: 线程模型
description: 线程模型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a820f46c59bbb98f978512a43dfa514926e5d227
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816465"
---
# <a name="threading-models"></a>线程模型


TAEF 提供了为执行测试的环境预先配置 COM 线程模型的功能。 默认情况下， \# 在 STA 线程上运行的托管©) 和脚本测试; 对于本机模式，线程模型未预配置。

"ThreadingModel" 元数据属性用于请求线程模型。 此属性支持的值包括：

| 属性值 | 描述                                                                               |
|----------------|-------------------------------------------------------------------------------------------|
| STA            | Single-Threaded 单元 (CoInitializeEx 是通过 COINIT \_ APARTMENTTHREADED 标志) 调用的。 |
| MTA            | 多线程单元 (CoInitializeEx 是通过 COINIT \_ 多线程标记) 来调用的。       |
| 无           | 未指定线程模型。                                                         |

 

## <a name="span-idconfiguring_a_threading_modelspanspan-idconfiguring_a_threading_modelspanspan-idconfiguring_a_threading_modelspanconfiguring-a-threading-model"></a><span id="Configuring_a_threading_model"></span><span id="configuring_a_threading_model"></span><span id="CONFIGURING_A_THREADING_MODEL"></span>配置线程模型


示例：从 c + + 标记请求 MTA 线程模型：

```cpp
class ThreadModelTests
{

    TEST_CLASS(ThreadModelTests);

    BEGIN_TEST_METHOD(MTAThreadingModelTest)
        TEST_METHOD_PROPERTY(L"ThreadingModel", L"STA")
    END_TEST_METHOD()
};
```

您还可以为类或模块请求线程模型属性。 例如，

```cpp
class ThreadModelTestsWithMTADefault
{

    BEGIN_TEST_CLASS(ThreadModelTestsWithMTADefault)
        TEST_CLASS_PROPERTY(L"ThreadingModel", L"Mta")
    END_TEST_CLASS()

    TEST_METHOD(DefaultWithMTASetByClass);
};
```

同样，您也可以请求托管测试的线程处理模型：

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

请注意，在上一次测试中： SetsOfMetadataTest，还可以使用元数据集并运行相同的测试：首先使用 STA 线程模型，然后使用 MTA。

 

 





