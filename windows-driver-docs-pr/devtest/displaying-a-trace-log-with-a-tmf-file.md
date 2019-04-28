---
title: 使用 TMF 文件显示跟踪日志
description: 使用 TMF 文件显示跟踪日志
ms.assetid: 1d592ed3-44d2-4d12-9d31-19b07e6962ea
keywords:
- 跟踪消息格式文件 WDK
- TMF 文件 WDK，显示跟踪日志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dbfc7f30e1627885971841f3d0aed0652d45c75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329686"
---
# <a name="displaying-a-trace-log-with-a-tmf-file"></a>使用 TMF 文件显示跟踪日志


## <span id="ddk_using_a_tmf_file_tools"></span><span id="DDK_USING_A_TMF_FILE_TOOLS"></span>


如果还没有[PDB 符号文件](pdb-symbol-files.md)跟踪提供程序，使用以下过程显示跟踪日志的内容：

1.  [启动 TraceView](starting-and-exiting-traceview.md)。

2.  上**文件**菜单上，单击**打开现有日志文件**。

3.  在中**日志文件名称**框中，键入路径和事件跟踪日志文件 (.etl) 的名称。 或者，单击省略号按钮 (**...**) 并导航到该文件。

4.  在中**日志文件选择**对话框中，您还可以设置选择选项，以生成其他输出日志文件中的文件。 此步骤可选。 有关详细信息，请参阅[设置跟踪日志选项](setting-trace-log-options.md)。

5.  单击 **“确定”**。

6.  单击**TMF （跟踪格式） 文件**，然后单击**确定**。

7.  执行下列操作之一：
    -   若要指定一个或多个 TMF 文件，请单击**选择 TMF 文件**，单击**确定**，单击**添加**，然后浏览到并从目录中选择一个或多个 TMF 文件。 若要从另一个目录中选择 TMF 文件，请单击**添加**按钮再次。 否则，请单击**完成**。
    -   若要指示 TraceView，搜索指定目录中 TMF 文件，请单击**设置 TMF 搜索路径**，单击**确定**，浏览到的目录，然后单击**确定**。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

有关指定 TMF 文件的详细信息，请参阅选择 TMF 文件和设置 TMF 搜索路径。

 

 





