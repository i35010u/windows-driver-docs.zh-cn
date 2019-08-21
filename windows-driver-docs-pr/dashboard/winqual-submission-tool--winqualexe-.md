---
title: Winqual 提交工具 (winqual.exe)
description: Winqual 提交工具 (winqual.exe)
ms.assetid: f7a34ee3-0532-465b-acb0-1ff80e2d4cb8
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7273640dd6d764bd79efbdf39d6584ae62dad092
ms.sourcegitcommit: ebf7371cb1b70330b9251bc2d2703d2b6de6fad1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68917854"
---
# <a name="winqual-submission-tool-winqualexe"></a>Winqual 提交工具 (winqual.exe)


Winqual 提交工具 (Winqual.exe) 可帮助你创建一个提交程序包以进行 Microsoft Windows 硬件认证。 该工具收集有关所准备提交的类型信息，并收集提交所需的所有日志、驱动程序和符号。

此外，Winqual.exe 的使用仅适用于 WLK。

## <a name="installing-the-winqual-submission-tool"></a>安装 Winqual 提交工具


1.  使用你的 Microsoft 帐户登录到仪表板。

2.  在左侧导航菜单上，单击“驱动程序”  。 在页面底部的“获取软件包”  部分，单击“Winqual 提交工具(WST)”  。

3.  在“文件下载 - 安全警告”  对话框中，单击“运行”  。

4.  在“Internet Explorer - 安全警告”  对话框中，单击“运行”  。

5.  在“欢迎使用”  屏幕上，单击“下一步”  。

6.  在“许可协议”  屏幕上，选择“我同意”  ，然后单击“下一步”  。

7.  在“选择安装文件夹”  屏幕上，单击“下一步”  。

8.  在“确认安装”  屏幕上，单击“下一步”  。

9.  单击“关闭”  退出安装过程。

## <a name="span-idhow_to_use_wstspanspan-idhow_to_use_wstspanspan-idhow_to_use_wstspanhow-to-use-wst"></a><span id="How_to_use_WST"></span><span id="how_to_use_wst"></span><span id="HOW_TO_USE_WST"></span>如何使用 WST


若要使用 Windows 提交工具 (WST)：

1.  打开此工具时，将显示“欢迎使用”  屏幕。 通过选中“不再显示此消息”  ，你可以选择在下次打开此工具时不再显示此对话框。 若要重新启用此对话框，请单击“工具”  、单击“选项”  ，然后选中“启动时显示‘欢迎使用’屏幕”  复选框。

2.  显示主屏幕，可在其中添加测试结果和驱动程序，以便创建提交包。

3.  如果新版本的 WST 可用，则系统将提醒你安装新版本。

4.  如果版本检查失败，你将收到警告消息，可通过选中“不再显示此消息”  复选框禁用此消息。

    **注意**  若要重新启用此对话框，请单击“工具”  、单击“选项”  ，然后选中“在更新检查失败时发出警告”  复选框。

     

5.  将测试结果添加到提交程序包，并选择保存列表以供以后使用。 将使用所有提交信息创建一个 **.xml** 文件（你将在稍后用它来创建提交）。

6.  通过使用“另存为”  菜单项或工具栏按钮，可以使用不同的文件名保存该文件。

7.  保存的文件将会添加到“最近使用的文件”  菜单中。

你也可以在 WST 中执行以下其他操作：

-   你可以通过单击“新建”  菜单项或工具栏按钮，开始一个新提交。

-   可以使用“打开”  菜单项或工具栏按钮打开之前保存的文件。 也可以通过单击该菜单项打开“最近使用的文件”  中的文件。

-   可以通过单击“删除”  按钮逐个删除列表中的条目，也可以通过单击“全部删除”  一次删除所有条目。

-   可以在提交程序包中放置一个可选的自述文件（ **.docx**、 **.doc** 或 **.txt**）。

## <a name="span-idhow_to_create_a_systems_submission_packagespanspan-idhow_to_create_a_systems_submission_packagespanspan-idhow_to_create_a_systems_submission_packagespanhow-to-create-a-systems-submission-package"></a><span id="How_to_create_a_systems_submission_package"></span><span id="how_to_create_a_systems_submission_package"></span><span id="HOW_TO_CREATE_A_SYSTEMS_SUBMISSION_PACKAGE"></span>如何创建系统提交程序包


1.  在主屏幕上，单击“添加”  按钮。

2.  浏览到 **.cpk** 文件（WLK 测试结果）并单击“加载”  。

3.  添加测试结果后，关闭“添加 DTM 结果”  对话框以向主屏幕中添加信息。

4.  可通过单击“编辑”  按钮编辑创建的条目。 这将打开已预填充所有信息的“编辑 DTM 结果”  对话框。

5.  添加所有条目后，可通过单击“创建提交”  按钮创建提交程序包。

6.  该工具可能会在打包时找到错误。 如果遇到错误，将停止打包。 含有错误的条目将以红色突出显示。 若要再次查看错误，请单击主窗口上的“查看错误”  按钮。 在创建包之前，必须修复所有错误。 可通过编辑条目和更新驱动程序或测试结果来修复这些错误。

7.  在修复所有错误后，便可以创建提交包。 将使用与 .xml 文件相同的名称，在相同位置创建提交包。

## <a name="span-idhow_to_create_a_device_submission_packagespanspan-idhow_to_create_a_device_submission_packagespanspan-idhow_to_create_a_device_submission_packagespanhow-to-create-a-device-submission-package"></a><span id="How_to_create_a_device_submission_package"></span><span id="how_to_create_a_device_submission_package"></span><span id="HOW_TO_CREATE_A_DEVICE_SUBMISSION_PACKAGE"></span>如何创建设备提交程序包


1.  在主屏幕上，单击“添加”  按钮。

2.  浏览到 **.cpk** 文件（WLK 测试结果）并单击“加载”  。

3.  如果设备不是内置设备，系统将要求你添加驱动程序、区域设置和（可选）符号。

4.  添加测试结果后，关闭“添加 DTM 结果”  对话框以向主屏幕中添加信息。

5.  可通过单击“编辑”  按钮编辑创建的条目。 这将打开已预填充所有信息的“编辑 DTM 结果”  对话框。

6.  添加所有条目后，可通过单击“创建程序包”  按钮创建提交程序包。

7.  该工具可能会在打包时找到错误。 如果遇到错误，将停止打包。 含有错误的条目将以红色突出显示。 若要再次查看错误，请单击主窗口上的“查看错误”  按钮。 在创建包之前，必须修复所有错误。 可通过编辑条目和更新驱动程序或测试结果来修复这些错误。

8.  在修复所有错误后，便可以创建提交程序包。 将使用与 **.xml** 文件相同的名称，在相同位置创建提交程序包。

 

 





