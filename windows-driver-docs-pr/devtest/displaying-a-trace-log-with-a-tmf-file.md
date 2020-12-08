---
title: 使用 TMF 文件显示跟踪日志
description: 使用 TMF 文件显示跟踪日志
keywords:
- 跟踪消息格式化文件 WDK
- TMF 文件 WDK，显示跟踪日志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ad63d9020b523520aff72a9fa1c66b5b2b2516f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839019"
---
# <a name="displaying-a-trace-log-with-a-tmf-file"></a>使用 TMF 文件显示跟踪日志


## <span id="ddk_using_a_tmf_file_tools"></span><span id="DDK_USING_A_TMF_FILE_TOOLS"></span>


如果没有跟踪提供程序的 [PDB 符号文件](pdb-symbol-files.md) ，请使用以下过程来显示跟踪日志的内容：

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  在 " **文件** " 菜单上，单击 " **打开现有日志文件**"。

3.  在 " **日志文件名称** " 框中，键入 ( .etl) 的事件跟踪日志文件的路径和名称。 或者，单击省略号 **按钮 ()** 并导航到该文件。

4.  在 " **日志文件选择** " 对话框中，您还可以设置 "选择选项" 以从日志文件生成其他输出文件。 此步骤是可选的。 有关详细信息，请参阅 [设置跟踪日志选项](setting-trace-log-options.md)。

5.  单击 **“确定”** 。

6.  单击 " **TMF (跟踪格式) 文件** "，然后单击 **"确定"**。

7.  执行下列操作之一：
    -   若要指定一个或多个 TMF 文件，请单击 " **选择 TMF 文件**"，单击 **"确定**"，再单击 " **添加**"，然后浏览到并从目录中选择一个或多个 TMF 文件。 若要从其他目录中选择 TMF 文件，请再次单击 " **添加** " 按钮。 否则，单击 " **完成**"。
    -   若要指示 TraceView 在指定目录中搜索 TMF 文件，请单击 " **设置 TMF 搜索路径**"，单击 **"确定**"，浏览到该目录，然后单击 **"确定"**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

有关指定 TMF 文件的详细信息，请参阅选择 TMF 文件和设置 TMF 搜索路径。

 

 





