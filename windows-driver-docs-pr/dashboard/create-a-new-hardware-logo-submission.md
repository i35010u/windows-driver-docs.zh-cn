---
title: 创建新的 WLK 设备认证提交
description: 创建新的 WLK 设备认证提交
ms.assetid: e812eee1-768d-42d6-918e-c716b5c29ea2
ms.author: EliotSeattle
ms.topic: article
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9a195461504d55aad971d02e00283d7a0b7ff4ac
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337287"
---
# <a name="create-a-new-wlk-device-certification-submission"></a>创建新的 WLK 设备认证提交


若要准备要认证的 Windows Server 2008（及更低版本）硬件，必须创建并提交 **WQReady.xml** 文件。 提交此文件，即表示允许仪表板测试你的设备并返回有关其性能的报告。 该报告包含设备与 Windows 标准进行比较的方式的详细列表。

# <a name="creating-a-wqreadyxml-file"></a>创建 WQReady.xml 文件

1.  下载 [Windows 徽标工具包 (WLK)](https://go.microsoft.com/fwlink/p/?LinkId=219237)。 请确保在要认证的每个操作系统上，使用相应认证工具包测试驱动程序。

2.  打开 Winqual 提交工具 (WST) 并单击“添加”  。

3.  浏览到 **.cpk** 文件（WLK 测试结果）并单击“加载”  。

4.  如果设备不是内置设备，请输入“驱动程序包”  、“驱动程序区域设置”  和“符号(可选)”  。

5.  关闭“添加 DTM 结果”  对话框。

6.  你可以通过选择新条目并单击“编辑”  来编辑该条目。

7.  添加所有条目后，通过单击“创建包”  创建 **.cab** 提交包。

8.  如果工具发现错误，将停止打包，并以红色突出显示含有错误的条目。 要查看错误，请单击“查看错误”  。 通过单击“编辑”  并更新驱动程序或测试结果，来修复这些错误。 必须先修复所有错误，然后才能创建程序包。

9.  工具将生成要提交的 **WQReady.xml** 文件。

    **注意**  
    **WQReady.xml** 是默认文件名，但是你可以重命名该文件。

## <a name="submitting-your-file"></a>提交文件

1. 登录到合作伙伴中心，然后选择“提交新硬件”  。 这将加载提交创建向导。

2. 在“程序包和签名属性”  部分，为你的驱动程序提交选择一个名称。 该名称可用于搜索和组织你的驱动程序提交。

3. 拖放或浏览到使用 Winqual 提交工具创建的要提交的 **.cab** 文件。 将开始上传该文件。

![显示 WLK cab 文件上传和 WQReadyXML 上传控件的屏幕截图](images/upload-wlk.png)

4. 现在拖放或浏览到要提交的 **WQReady.xml** 文件。 这将完成上传

5. 从[创建新硬件提交](create-a-new-hardware-submission.md)中的步骤 6 开始继续完成提交。
