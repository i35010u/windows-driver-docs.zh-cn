---
ms.assetid: EDA6357A-D18D-439D-A0DD-050BA51E1A79
title: 为静态驱动程序验证程序创建日志文件
description: Windows Server 2012 硬件认证计划需要所有驱动程序在正当提交时提供驱动程序验证日志 (DVL)。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cada8a4664892b1f486e1a0e18e4f082af615ac
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207643"
---
# <a name="creating-a-log-file-for-static-driver-verifier"></a>为静态驱动程序验证程序创建日志文件

Windows Server 2012 [硬件认证计划](https://go.microsoft.com/fwlink/p/?linkid=227016)需要所有驱动程序在正当提交时提供驱动程序验证日志 (DVL)。 在为驱动程序创建 DVL 之前，必须先运行[静态驱动程序验证程序](../devtest/static-driver-verifier.md) (SDV)。 DVL 包含代码分析的结果和静态驱动程序验证程序日志文件的摘要。 日志文件不包含源代码信息。

为了获得最佳效果，请在运行静态驱动程序验证程序前运行代码分析工具。

**为静态驱动程序验证程序创建日志文件**

1.  在 Microsoft Visual Studio Ultimate 2012 中，选择驱动程序项目文件，然后选择并按住（或右键单击）打开项目属性。 选择“Windows 8 版本”  作为“配置”  ，并选择“x64”  作为“平台”  。
2.  如果已运行代码分析工具，请按照[运行静态驱动程序验证程序](../devtest/using-static-driver-verifier-to-find-defects-in-drivers.md#running_static_driver_verifier)中的以下说明操作。 有关使用 SDV 的详细信息，请参阅“使用静态驱动程序验证程序查找驱动程序中的缺陷”
3.  如果 SDV 发现你的驱动程序中存在缺陷，请在“结果”窗格中选择该缺陷，查看导致违反规则的代码路径的跟踪。 修复在驱动程序中找到的任何缺陷并再次运行 SDV。

静态驱动程序验证程序会将结果写入到项目的 SDV 子目录（例如 \\myDriverProject\\SDV）中的文件 SDV.DVL.xml。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


有关静态驱动程序验证程序和驱动程序验证日志的最新信息，请参阅“WDK 发行说明”。 发行说明可在 [Windows 驱动程序工具包 (WDK) 下载页](https://go.microsoft.com/fwlink/p/?linkid=254897)上找到。

**重要提示**  认证提交可以接受 DVL 文件出现超时、加宽行距和其他未成功结果。 这不会导致 HCK 中的静态工具测试失败。 对于 HCK 2.0，静态工具测试只需要 DVL 文件存在，就可证明已运行代码分析和 SDV，并不需要通过所有规则。

 

你还可以从“Visual Studio 命令提示”窗口运行静态驱动程序验证程序。 通过运行以下批处理文件之一设置环境。

```cpp
"C:\Program Files\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x64
```

-或者-

```cpp
"C:\Program Files (x86)\Microsoft Visual Studio 11.0\VC\vcvarsall.bat" x64
```

运行静态驱动程序验证程序。

```cpp
msbuild.exe <vcxprojectfile> /p:Configuration="Win8 Release" /p:Platform=x64 /target:sdv /p:inputs="/clean"
msbuild.exe <vcxprojectfile> /p:Configuration="Win8 Release" /p:Platform=x64 /target:sdv /p:inputs="/check:default.sdv"
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [创建驱动程序验证日志](creating-a-driver-verification-log.md)
* [静态驱动程序验证程序](../devtest/static-driver-verifier.md)
* [使用静态驱动程序验证程序查找驱动程序中的缺陷](../devtest/using-static-driver-verifier-to-find-defects-in-drivers.md)
* [硬件认证计划](https://go.microsoft.com/fwlink/p/?linkid=227016)
 

